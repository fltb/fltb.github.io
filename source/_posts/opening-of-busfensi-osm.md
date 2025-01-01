---
title: OpenStreetMap Public Transport Relation Editor Based on Modern Frontend Tech Stack - Starting
date: 2024-07-16 21:04:54
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

In this OSPP project, I will develop an OpenStreetMap public transport relation editor based on modern frontend technology stack. I hope to make some contributions to the OSM community.

## Project Goals

The goal of this project is to develop a cross-platform editor using modern frontend technology stack. This editor should be easy to operate with intuitive interactions. During the project, we will collaborate with the OSM China community to ensure high standards in both interaction design and functionality implementation.

## Project Implementation

### Basic Project Framework

The project can be roughly divided into map rendering module, route editing module, and OSM API module.

### Map Rendering

Using the abstractions provided by the OSM API module, request map data from OSM main site based on current latitude/longitude position and required rendering range. Parse the metadata into graphic objects (such as PIXI.Graphics or PIXI.Sprite) through the Feature abstraction provided by the rendering module, and render using WebGL via Pixi.js.

Meanwhile, the map needs to be updated through user interaction. By listening to user mouse and keyboard events, dynamically request data from the server and update during movement, and control map rendering granularity during zoom in/out. When users select certain elements, highlight those elements. This logic needs to be integrated with the route editing module.

### Route Editing

Support multi-selection of route nodes and stations on the map, supporting methods like point selection, box selection, brush selection, etc. Provide route creation and editing operations through a clean UI. The page needs to be clear enough with intuitive tools for users to quickly find needed functionality.

Support automatic path calculation using only bus stop data by calling other open source routing APIs (such as GraphHopper, OSRM, OpenTripPlanner, etc.).

Support operation history persistence through state management mechanisms, satisfying basic operation needs like undo/redo. Version control concepts can also be introduced to ensure efficiency and stability of history records.

### OSM API Module

Provide abstraction for interaction with OSM API v0.6, including login authentication, data requests, data upload after editing, while following OSM interface specifications.

## Project Progress

Project progress will be updated in subsequent articles.

## License

This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/3.0/deed.en_US">CC0</a>.