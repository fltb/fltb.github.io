---
title: OpenStreetMap Public Transport Relation Editor Based on Modern Frontend Tech Stack - Weekly Report#4
date: 2024-09-15 20:22:38
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
This report is also two weeks late. Actually, in terms of real progress, the project is nearly complete. However, I'll sync the progress to when this report should have been published.

## Project Progress

### Filter and Collection

Completed the filter part, filtering the originally requested OSM bbox data into collections such as public transport and highway.

Considering that the editor primarily serves public transport, there's no need to focus too much on editing building information and other data. The main focus is on highway and public transport. After referencing the OSM wiki, I wrote filters that use tag information to filter and categorize data.

For filtered data that needs to be displayed and edited, established a feature tree structure to maintain the tree relationships of OSM data, facilitating display and editing.

### Sidebar

Added a sidebar on the right side of the map, including outline view and property editor.

In the outline view, data is displayed using a tree-like list, allowing data selection.

In the property editor, existing OSM feature properties are displayed and their tags can be edited. Member order changes introduced dnd-kit for drag-and-drop order changes. It also allows inserting selected features as members.

### Fixes

Relations' members can also be relations, which was forgotten in the previous type definitions.

Removed some console.log debugging statements.

Various other small bug fixes.

## Update Plans

The next phase of updates will involve some finishing touches, mainly including incomplete features, logic that needs optimization, UI issues, etc.

Specific TODOs have been updated in the project repository.
