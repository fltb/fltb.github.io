---
title: OpenStreetMap Public Transport Relation Editor Based on Modern Frontend Tech Stack - Weekly Report#1
date: 2024-07-18 09:25:21
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

Two weeks of development have passed quickly, and it's time to write a bi-weekly report.

## Project Progress

The project is still in early development stages. While there isn't a usable prototype yet, we can already render some test data.

The rendering implementation has been largely determined, and testing shows we can render points and paths.

However, some features haven't been implemented yet since other module interfaces aren't fully defined. For example, highlighting path segments individually rather than selecting the entire path as in the iD editor. Polygon rendering also hasn't been implemented yet as it requires the editing module interface.

## Update Plans

Over the next two weeks, we'll focus on developing the editing module, creating a well-functioning prototype for refinement. Once stable, we can communicate with OSM-standard APIs and submit results. Hopefully we won't get blacklisted for introducing malicious bugs! 😂

Currently working on the state management module, hoping to provide stable support for editing.

## Demo Effects

Our code can't perform any editing operations yet, nor can it directly render XML or JSON from the OSM website. Therefore, I manually constructed a few points for basic rendering tests. Background tile functionality was also tested and is working well.

Please excuse the poor color choices - I'll refine them later. Since the chosen coordinates happened to have no roads (not surprising, as 71% of Earth is ocean and most land is uninhabited, and I unfortunately picked random coordinates), the OSM tiles have no identifiable content. However, tiles are being properly requested and rendered, as can be seen in the image requests in the developer tools.

![img](/weekly-post-busfensi-1/2024-07-18/screenshot.png)
