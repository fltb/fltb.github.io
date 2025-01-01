---
title: OpenStreetMap Public Transport Relation Editor Based on Modern Frontend Tech Stack - Weekly Report#2
date: 2024-08-05 15:39:19
tags:
- Frontend
- WebGL
- Maps
- Development
- OpenStreetMap
- OSM
- Public Transport
- OSPP

categories:
- Frontend
---

(AI generated)

It's been over two weeks since the last report, so it's time to sync up on current progress.

## Project Progress

The core modules have been largely finalized, allowing us to enter the latter stage of development. Future work will mainly involve adding new features within the existing framework.

First, we got the rendering part working, though some details still need polishing, such as styles and controlling rendered elements. These will be addressed alongside future functionality to ensure styles align with editing logic.

Second, I wrote an OSM API module that wraps some OSM interfaces with Promises and parses returned XML into JS Objects for easier program use.

Next is the editing module, which mainly includes operation logic and global data management.

For map editing operations, we introduced a state machine that manages the current editor state. It listens for mouse and keyboard events and performs state transitions and related data maintenance according to functions and state relationships defined in the state diagram. Events trigger behaviors and new states based on current state. The state machine provides hooks for mounting elsewhere to track events, such as mouse events in Pixi. Editing operations occur during state transitions.

Generally, state machine transitions generate a series of global data changes. To manage these changes, we provide a doubly-linked list called the action list. This list exposes undo, redo, and do interfaces. The do interface accepts and executes an action, adding it to the list tail. To avoid duplicate actions, some actions can be merged.

An action provides do, undo, and redo interfaces, with some also providing merge. Actions should maintain global data during execution, undoing, and redoing, while also maintaining other related changes like affected element UIs and layer data. This ensures all changes are centralized, reducing mental overhead for managing related changes when implementing undo/redo.

Global data is an object referenced in each action. The action list ensures correct order of actions during undo and redo, ensuring an action is undone from its post-execution state with subsequent actions already undone.

Since actual editing operations aren't complete yet, we're temporarily not considering undo and redo operations as they'll depend on unfinished code.

## Update Plans

The project has been in development for a month, and with the September end deadline approaching, time is tight. I'll prioritize core functionality, deferring non-core peripheral features to ensure successful completion (can't lose that 12K OSPP money - it's a lot! Can continue developing remaining features during National Day holiday).

Here are the roughly needed features:

### UI Aspects

Outline View: Shows all current elements, allows element selection and basic state management

Property View: Manages various properties including global settings and current selection metadata

Plus some independent components like new node creation, line segment connection, etc.

### Functional Aspects

As a public transport editor, it needs public transport editing capabilities. In OSM XML, public transport relations are relation elements with a route and tags describing specific information.

Metadata editing can use the previously mentioned property view for direct editing.

Point position editing uses the map module. Consider adding styles for highlighting to clarify current route editing.

Route relationships with points and paths need map selection functionality combined with property view.

May need route creation functionality including new points, new routes, and route property editing.

Implement route calculation based on station relationships, possibly using existing APIs

## Demo Effects

Apologies for not having time to polish - everything sharing one style doesn't look great.

However, just a few more lines of code will let us disable building rendering, which should help a lot. Will gradually adjust styles later - maybe borrow colors from the iD editor? 😂

Not demonstrating editing functionality as it's just point dragging, map panning, and zoom adjustment.

![img](/weekly-post-busfensi-2/2024-08-05/image.png)
