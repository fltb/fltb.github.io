---
- title: Blog Refactoring Notes  
- date: 2025-01-01 16:23:54  
- tags:  
- Frontend  
- Blog  
- Hexo  
- Development  
- Blog Theme  
- EJS  
- Template  
- Refactoring  
- categories:
- Frontend  
---

(AI generated)

First post of 2025!  

Let me briefly share what I worked on today.

## Refactoring the Blog  

### Maintaining the Theme  

The theme used in this blog has been out of maintenance since 2022, as the original author stopped updating it. Many of the new features, like the Giscus commenting system, CC License, and Busuanzi statistics, were added by me. However, I never had the time to properly create a new repository for maintaining this theme. Instead, I awkwardly dumped the raw theme files directly into the `themes` folder, sitting alongside blog posts in the same repository. Most of these new features were implemented through rough "monkey patching" of the original files rather than following the proper Hexo theme standards to configure and expose interfaces.

This awkward setup persisted for almost two years until today, when I decided to address it. Over this time, Hexo has undergone several iterations, and many APIs have needed adjustments. For example, dependencies like `node-sass`, which included a C++ binary for Sass rendering, were replaced with `dart-sass`, introducing numerous breaking changes.

It was time to use this major update as an opportunity to refactor my blog. I pulled the theme out as a separate project and updated the APIs. All of my previous patches have now been properly exposed following Hexo's theme standards. To achieve a complete separation between the theme and the blog—allowing independent updates via submodules—I added functionality to read configurations from the root directory. While Hexo can handle this to some extent, it doesn't support reading multiple languages at once. The theme's multilingual support previously relied on several hacks to locate and read specific files, forcing me to rewrite the configuration script to adapt. Now, the theme configuration files can be read externally, which is incredibly satisfying.  

After completing these changes, I created a [new repository](https://github.com/fltb/hexo-theme-minos) and published a release. I can now officially call myself a theme maintainer (haha), even though most of the credit goes to the original author, with me just making some minor updates for compatibility with the latest version.

### Filling Blog Gaps  

The English section of my blog has always been incomplete. Initially, I added it with the intention of improving my English, along with some other odd motivations. However, I soon realized that just finding time to write blogs was hard enough, let alone rewriting them in English. The blank, untranslated English sections became a source of anxiety every time I visited my blog.  

So, I made a somewhat controversial decision: using AI to generate translations. Borrowing a Cursor from a classmate during finals week, I fed the entire project into it and generated an English version of the blog. At least now, I won't feel anxious every time I open the homepage.

As for my stance on AI, I'm not particularly enthusiastic about its use in coding—current AI tools still struggle with maintaining medium to large-scale projects over time. They also fall short when dealing with complex business logic or state management. However, I’m open to using AI for translation. After all, translation is one of NLP's oldest tasks, and for something as straightforward as blog posts, it just needs to convey the basic meaning accurately.

## What's Next  

In the coming days, I’ll try to work on my short-term winter break plans, finishing the work I left incomplete for OSPP. I hope to create something that can truly be considered a representative project.  