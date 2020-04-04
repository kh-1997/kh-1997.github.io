---

layout: post
title: '访问者模式'
subtitle: '访问者模式'
date: 2020-03-04
categories: 技术
cover: 'http://on2171g4d.bkt.clouddn.com/jekyll-theme-h2o-postcover.jpg'
tags: 设计模式﻿
---

# 设计模式二十一

------

# 行为变化

我们理解您需要更便捷更高效的工具记录思想，整理笔记、知识，并将其中承载的价值传播给他人，**Cmd Markdown** 是我们给出的答案 —— 我们为记录思想和分享知识提供更专业的工具。 您可以使用 Cmd Markdown：

> * 整理知识，学习笔记
> * 发布日记，杂文，所见所想
> * 撰写发布技术文稿（代码支持）
> * 撰写发布学术论文（LaTeX 公式支持）

![cmd-markdown-logo](https://www.zybuluo.com/static/img/logo.png)

除了您现在看到的这个 Cmd Markdown 在线版本，您还可以前往以下网址下载：

### [Windows/Mac/Linux 全平台客户端](https://www.zybuluo.com/cmd/)

> 请保留此份 Cmd Markdown 的欢迎稿兼使用说明，如需撰写新稿件，点击顶部工具栏右侧的 <i class="icon-file"></i> **新文稿** 或者使用快捷键 `Ctrl+Alt+N`。

------

## 访问者模式

- 使用场景：由于需求的变化，某些类层次结构中常常需要增加新的行为，如果直接在基类中做这样的修改，将会给子类带来黑繁重的变更负担，甚至破坏原有设计。

- 使用原理：在不更改类层次结构的前提下，在运行时根据需要透明的为各个类动态添加新的操作。

  ![image-20200305184159055](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200305184159055.png)

1. Visitor模式通过双重分发，两次动态绑定为各个类添加新的操作
2. 第一个为accept方法的多态辨析，第二个是visitElementX方法的多态辨析
3. visitor模式的最大缺点在于扩展类层次结构（添加新的Element子类）会导致visitor类的改变，因此该模式适用于Element类层次结构稳定，而其中的操作却经常面临频繁改动。

### 文稿发布和分享

在您使用 Cmd Markdown 记录，创作，整理，阅读文稿的同时，我们不仅希望它是一个有力的工具，更希望您的思想和知识通过这个平台，连同优质的阅读体验，将他们分享给有相同志趣的人，进而鼓励更多的人来到这里记录分享他们的思想和知识，尝试点击 <i class="icon-share"></i> (Ctrl+Alt+P) 发布这份文档给好友吧！

------

再一次感谢您花费时间阅读这份欢迎稿，点击 <i class="icon-file"></i> (Ctrl+Alt+N) 开始撰写新的文稿吧！祝您在这里记录、阅读、分享愉快！

作者 [@kh-1997][3]     
2020 年 03月4日    