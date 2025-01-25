---
title: OSM Editor Plan  
date: 2025-01-24 20:31:12  
tags:  
- Frontend  
- WebGL  
- Mapping  
- Development  
- OpenStreetMap  
- OSM  
- Public Transport  

categories:  
- BusFensi  
---

Previously, in [this post](https://github.com/fltb/blog-comments/discussions/8#discussioncomment-11817482), I mentioned that I would continue improving the modules. Here, I'll outline the overall technical plan.

### Goals and Approach

Let me summarize the general idea. Let's assume that buildings and roads are fixed for now—after all, this is a public transport editor, and I currently lack the resources to handle an all-purpose editor.

We can introduce the concept of "editing mode," starting with defining a public transport editing mode. Logically (even though the underlying implementation involves editing roads), this mode will operate on the existing paths and buildings, adding new information instead of modifying existing ones. Here's what we need to achieve:

1. **Create new public transport routes**:
    - Manually select or create some stops to form a route consisting only of stops.
    - Manually select paths in sequence to define the route. This might involve drawing operations, such as flexible selection via mouse dragging. Bidirectional routes might need additional handling.
    - Automatically generate routes based on stops. I haven't figured out how to implement this yet.
    - Modify route metadata, including names, operators, etc.

2. **Edit existing routes**:
    - Add, delete, or reorder stops.
    - Extend, shrink, delete, or reconnect paths.
    - Modify route metadata, including names, operators, etc.

3. **Delete routes**:
    - Direct deletion will suffice for now. In the future, we might consider merging routes.

The above covers single-route operations.

Additionally, we need a convenient way to retrieve route information. The current outline is decent and can be retained.

After completing the core tasks, the editor should ideally allow comprehensive OSM editing without leaving the editor. We can treat the existing functionality as a "fallback" mode. Even if it's abstract and somewhat clunky, having complete functionality is crucial. Happy Path might cover 80% of user needs, but for the remaining 20%, relying on other editors would be frustrating—and I’d likely face complaints.

The initial plan is to introduce an abstraction for "editing mode," discard the existing logic, and treat it as a fallback mode. Then, implement new, robust features in the new mode. The goal is to shed the "half-baked" label and achieve production-level capabilities—at least comparable to JOSM.

### Technical Approach

I'm not satisfied with the current implementation, so I'll list areas that need improvement.

After some thought, I've decided to overhaul the previous implementation. If it's not mentioned here, it can be assumed "optimized away." Consider this a relatively complete technical roadmap.

#### View Abstraction

This time, I’ll standardize Outline and Property as "views"—adaptive-length standardized elements with consistent functionality but flexible placement. This will simplify creating context menus with the same abstraction.

Given React's functional components, we only need to standardize the props type.

##### Context Menu

The context menu itself should be a view but can act as a modal-like component, displayed at a specified position in pixels. Callers provide it with a view as a child, making it a utility for the map view.

##### Outline View

The view should allow listing and quickly retrieving all current metadata. Requirements:
- Complete access to current data, including Relations, Ways, and Nodes.
- Ability to filter data by specific categories, such as public transport.
- Access to editing data, such as selected items.

This can be implemented with tabs, with corresponding buttons (e.g., Select) for actions.

##### Property View

Displays the active element. There can be multiple selected elements, but only one active element (a subset of selected). It should handle type-based display, with a fallback manual view for unknown types.

#### Refactor Zustand State Management

- Fix persist state issues.
- Split state: Different states require different slices. For example, zoom and lat/lon can use a URL store middleware, while editing data should use the zundo middleware. Finally, expose these middleware interfaces in a unified global store.

#### Editing Mode Abstraction

Editing mode is a new abstraction, a sub-mode of the map view.

It requires displaying data with a set of layers (Layer) in JSX, where the outermost layer is a PIXI Container. The Container will render images based on data state.

Editing functionality requires a controller to handle user inputs and manipulate data. With Zustand managing local global state, this decouples data manipulation from its presentation.

The controller's complexity warrants a state machine abstraction, managing how user actions affect data within different states.

##### State Machine Implementation

The current state machine implementation lacks modularity. While advanced abstractions like behavior trees aren't necessary, substate abstractions can support features like "press a button to draw a point."

Modularity requires runtime creation of instances to avoid conflicts between substates. Existing code needs a complete overhaul.

Data manipulation by the state machine can be viewed as an output, maintaining a unidirectional data flow. For now, this part won't change; Zustand provides sufficient flexibility for future enhancements.

#### New Business Logic for Public Transport

With the new abstraction in place, we can write new business logic.

##### Create an Empty Route

Press the "New Route" button to create an empty route and enter editing mode.

This involves creating a Relation and providing a guided metadata editor using the property view. Names and other attributes should be prompted but also allow advanced editing for adding tags.

##### Add Stops

This might be a sub-mode within the editing mode, controlled by the state machine.

Three actions are possible:
- Create a simple stop by drawing a point and automatically adding it.
- Create a larger stop (name TBD) by drawing a closed polygon and adding it.
- Select a stop, right-click to open the menu, and add it to the route.

The property view can adjust the stop order.

##### Create Routes Manually

Refer to my notes for details. The general idea is to specify control points and calculate the shortest path locally for real-time editing.

##### Create Routes Automatically

Research OSRM's API for automated routing.

#### Edit Routes

Similar requirements as above, involving an editing flow.

##### Select Route

Map the existing routes for visualization, allowing selection via right-click. Outline view should also enable this.

##### Partial Redraw

Define start and end points on an existing route and proceed with the previous logic.

##### Full Redraw

Same as above.

##### Manual Path Assignment

Coordinate with the property view. A "picker" tool, like Blender's behavior, might work here.

#### Fallback Manual Mode

Package unimplemented features into a pure manual mode.

#### Cross-View Relationships

Handle functionality like selecting from the Property View while syncing with the Map View's state to filter compatible entities. Further refinement may require redesigns.