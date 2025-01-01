---
title: OpenStreetMap Public Transport Relation Editor Based on Modern Frontend Tech Stack - Weekly Report#3
date: 2024-09-02 16:37:32
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

Unfortunately, this report is two weeks late, so I'll be publishing two reports together (the next one is also being written).

## Project Progress

As of when this report should have been published, I had completed the React restructuring and preliminarily determined the composition of the UI editing module.

### Restructuring

Deciding to restructure after one month into the project, with half of it already written, was certainly not an easy decision. However, the original technical choices couldn't support the project's continued development—not that it was technically impossible, but it would require more time and the complexity would become unmanageable.

The original technical choice was influenced by the Rapid project, which used native ESM for development rather than popular frontend frameworks. Since my project also uses PIXI.js for map rendering, and many implementations and designs referenced Rapid, I naturally followed its technical choices initially.

However, when preparing the UI module and facing the state management logic that needed to be expanded, the project's complexity began growing exponentially. I needed to ensure that both PIXI.js components and DOM UI tracked and rendered the same data changes, making the logic very complex. This would require expanding the state management logic, as undo and redo functionality was also needed. The original Action List model wasn't sufficient for such complex requirements, and expanding it to a usable state would require significant work—the Rapid project, or the iD project, wrote thousands of lines of code just implementing the editing system and related parts, and that's just the framework. If I were to write it this way, subsequent development progress would be hard to guarantee.

At this point, I sought help from my mentor, who consulted several active frontend developers and received some state management suggestions. Additionally, more than one person questioned not using a framework, suggesting introducing modern frontend frameworks like React or Vue, saying "I think it's best to decide whether you want to reinvent the wheel or use existing wheels to implement an application—choose one or the other."

After considering various suggestions, I decided to introduce React, use Zustand for global state management, and since PIXI.js has an official React binding, this also facilitated my migration work.

The migration process went smoothly, as I'm actually more familiar with framework development. The initial choice of native JS was purely experimental. Obviously, this experiment wasn't very successful.

After restructuring, the original Action abstraction was completely abandoned, replaced by the model module implemented with Zustand, with the originally needed functionality becoming functions in the Zustand store. These functions ending with Action are probably the last traces of this module. The PIXI module used React bindings, now looking like regular React JSX. The original stateMachine was preserved, with only minor modifications to the now-deprecated ActionList interface and heavily modified PIXI module interface. Other code wasn't changed much, just migrated to TypeScript during restructuring, which is naturally stricter and more convenient than JSDoc's pure comment-based type annotations.

### UI Part

After restructuring, I began developing the UI module. For the previously planned Outline and Property pages, I wrote some simple static components as placeholders. Current testing is good, able to access and display global state. This part's development might be more like traditional frontend projects, so it should be relatively smooth.

## Update Plans

This update plan, since there hasn't been much functional progress, will continue advancing based on the goals mentioned in the previous bi-weekly report.

What needs to be added is that we'll categorize current elements in the outline view and write filters to screen data, as this editor might currently only need to display `highway=*` and public transport v2 data, so the subsequent editing interface should be much cleaner.
