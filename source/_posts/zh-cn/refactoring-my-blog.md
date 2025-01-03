---
title: 博客重构记
date: 2025-01-01 16:23:54
tags:
- 前端
- 博客
- Hexo
- 开发
- 博客主题
- ejs
- 模板
- 重构

categories:
- 前端
---

2025 年第一篇 post ！

大概讲下今天做了点什么吧。

## 重构博客

### 维护主题

这个博客使用的主题早在 2022 年原作者就已经停止维护了，很多新功能都是我新加进去的，比如 giscus 评论系统，CC License 和 busuanzi 数据统计。但是我一直没空去下定决心重开一个仓库来维护这个主题，而是用一种很别扭的方式直接把纯文件放在 themes 文件夹里面，和博客文章一起挤在一个仓库。毕竟这些功能我很多只是在源文件里面做了一些粗暴的 monkey patch，而没有按照 hexo 主题的标准来进行合适的配置和暴露接口。

我的博客这样尴尬的状态持续了接近两年，直到今天我决定改变这个现状，因为在此期间 hexo 经过了很多的迭代，许多的 API 都需要重新修改，包括原来的依赖包含 C++ 二进制的 node-sass 的 sass render 已经将依赖更新到 dart-sass，并进行了很多 breaking change。

是时候借这个大版本更新的机会去重构我的博客了。我把这个theme 重新拆了出来，并且更新了 API。我把自己的 patch 都按照 hexo 的 theme 标准重新暴露了接口。同时我为了实现 theme 和 blog 的彻底分离，方便 submodule 进行独立的更新，还添加了在主目录下读取 config 的功能——本来 hexo 是可以帮忙读的，但是 hexo 显然不能一次读多个语言，所以这个 theme 本身的多语言支持就使用了许多的 hack，自己去找对应的文件去读, 导致我不得不修改 theme 的 config 读取脚本来适配这个行为。现在主题的配置文件已经可以在外面阅读了，非常美妙。

做完了这些之后，我新建了一个[仓库](https://github.com/fltb/hexo-theme-minos)，并且发布了 release。现在我也算得上一个主题维护者了（哈哈），虽然大多数的工作得归功于原作者，而我只是做了一点小小的向新版本的 maintain 而已。

### 博客补缺

我的博客的英文部分是非常残缺的状态，最初设置英文部分的考量可能是有一些想学英语的念头和一些奇怪的想法杂糅在一起，但是事实证明抽出时间写博客已经不容易，再去用英语重写每篇博客更是雪上加霜。整片为翻译的空白英语部分更是让我害怕面对自己的博客。所以我做了一个违背祖宗的决定：使用 AI 翻译一份英文。正好借着期末周从同学那里借了一个 cursor, 我就把整个项目丢进去，翻译了一份英文版出来。至少我打开博客主页的时候不会焦虑了。

我本人对 AI 写代码其实态度不是特别积极——毕竟中大型项目的长线维护工作用现有的 AI 还是难以解决的。而且涉及复杂业务和状态管理的工作，我目前用过的 LLM 当中还没找到能够胜任的。不过对于 AI 翻译我持开放态度，毕竟这是 NLP 的老本行，尤其是这种普通的博客文章，只要基本准确地传达意思即可。

## What's Next

接下来的时间，我会尽量把寒假的短期计划肝出来，完成我 OSPP 还没有完全完成的工作，希望能打造一个代表作出来。