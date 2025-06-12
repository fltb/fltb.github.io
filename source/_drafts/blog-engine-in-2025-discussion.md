---
title: 2025 年的带 CMS 博客——怎么还是你 WordPress ？聊聊
date: 2025-06-12 21:56:00
tags:
- 博客
- 前端
- 感想
- 开发
- WordPress
- CMS
categories:
- 前端
---

## 为什么要 CMS

如果一个不是程序员的建站者，想要在 2025 年选择尽可能简单的方式来创建一个博客网站。一般来说会有以下诉求：

- （但是我是程序员，所以等下整理）

然后，环顾四周，竟然有项目能满足这个要求，而且就是大名鼎鼎的：WordPress！

很难想象作为一个“专业前端”的笔者，竟然会推荐比自己年纪还大的项目了，是说我们现代框架没人了么？可是站点生成器明明是前端的大热门，Github 的 [#ssg topic](https://github.com/topics/ssg) 上有接近两万个 repo。就连笔者自己的这个博客也是用 Hexo 来部署的。这是要打自己的脸么？

欲知后事如何？且看下节分解。
  
## 现代框架在干什么

很显然的是，现代 SSG 框架，无论理念，原理和实现，基本上都不约而同地抛弃了内置 CMS 面板的做法。

现代框架的一个演进思路之一，就是在把静态网站的开发流程，从 WordPress 那样的靠近终端产品的思路，变成了向普通前端项目的开发流程靠拢。现在都什么年代了，还在玩 CMS ，来写代码嘛！又不难，试试看嘛。这里我们选取一些有代表性的框架。

### Jekyll

Jekyll 作为第一代流行起来的 SSG，引出了整个静态站点生成的思想。在 [2014 年的一次 README 更新中](https://github.com/jekyll/jekyll/commit/e5f1a400ee8a8daeef7e6263f15de43375fda915)，它进行了这样的修改：

> Think of it sort of like **a file-based CMS**, except without all the complexity. Jekyll takes your content, runs it through Markdown converters and Liquid templates, and spits out a complete, static website suitable for serving with Apache, Nginx or your favorite web server.

这里说明了它通过一些 Markdown 文件和模板来生成一个完整的网站。最重要的一点是，它提出了 *file-based CMS* 这个概念，这就意味着，它选择了基于代码和文本文件的配置，而不是使用管理面板来操作。

这一步，可以说是开创性的：仅仅靠一些文件就可以生成网站，而且网站是纯静态的文件，前者对应 CI/CD 和各种配套工具链，后者带出了各种静态部署服务。
