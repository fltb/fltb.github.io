---
title: 基于现代前端技术栈的 OpenStreeMap 公共交通关系编辑器 —— 周报#4
date: 2024-09-15 20:22:38
tags:
- 前端
- WebGL
- 地图
- 开发
- Openstreep Map
- OSM
- 公交
- OSPP

categories:
- 前端
---

这次的周报又多拖了两个星期。其实按照实际进度来说项目已经接近完成了。不过我会吧进度同步到这份周报该发布的时间。

## 项目进度

### Filter and Collection

完成 filter 部分，将原始请求的 osm bbox 数据进行筛选，分为 public transport 和 highway 等 collection。

考虑到编辑器主要服务于公共交通，所以不需要过多关注建筑物等信息的编辑。主要关注 highway 和 public transport.在参考了 OSM wiki 之后编写了 filter, 利用 tag 信息来过滤数据，进行分类。

对于筛选后需要展示和编辑的数据，建立了 feature tree 的树形结构，维护 OSM 数据的树形关系，便于展示和编辑。

### Sidebar

在地图的右侧新增了 sidebar, 包括 outline view 和 property editor。

在 outline view 中，使用树形 list 展示数据，并且允许选择数据。

在 property editor 中 展示现有 OSM feature 的 property, 并且允许编辑其中的 tag. 成员的顺序更改引入的 dnd-kit 来拖拽变化顺序。同时允许将一些选中的 feature 插入其中作为成员。

### Fix

relation 的 member 也可以是 relation, 之前的 type 定义中忘记了。

移除了一些 console.log 调试语句。

其他一些小的 bug 修正。

## 更新计划

下阶段的更新将会进行一些收尾性质的功能，主要包括未完成的功能，需要优化的逻辑，UI 上的问题等等。

具体的 TODO 已经更新在项目仓库。