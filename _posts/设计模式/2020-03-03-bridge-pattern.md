---
layout: post
title: '桥接模式'
subtitle: '桥接模式'
date: 2020-03-02
categories: 技术
cover: 'http://on2171g4d.bkt.clouddn.com/jekyll-theme-h2o-postcover.jpg'
tags: 设计模式﻿
---

# 设计模式五

------

# 单一职责

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

## Bridge Method

- 使用场景：抽象和实现分离。极大地提高了系统的灵活性，让抽象部分和实现部分分离开来，有助于系统进行分层设计，产生更好的结构化系统。

- 使用原理：抽象和实现分离**，通过抽象类和接口**将聚合关联建立在抽象层**，需要正确识别出系统中两个独立变化的维度，在这两个维度上分别进行实现。
- 设计原则：

- 合成复用原则：多用组合、聚合，少用继承

- 依赖倒转原则：将变化进行隔离，使高层依赖于低层接口，具体实现依赖于接口

- 开闭原则：增加新的功能，在已有代码上进行扩展。

  ![image-20200303172818906](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200303172818906.png)

  

![image-20200303172549616](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200303172549616.png)

将抽象部分（业务功能）和实现部分（平台选择）分离。使他们可以独立的发生变化。

装饰者模式不同：需要装饰者，没有进行抽象和实现分离，抽象和实现都在一个维度变化，使用同一个业务。

### 文稿发布和分享

在您使用 Cmd Markdown 记录，创作，整理，阅读文稿的同时，我们不仅希望它是一个有力的工具，更希望您的思想和知识通过这个平台，连同优质的阅读体验，将他们分享给有相同志趣的人，进而鼓励更多的人来到这里记录分享他们的思想和知识，尝试点击 <i class="icon-share"></i> (Ctrl+Alt+P) 发布这份文档给好友吧！

------

再一次感谢您花费时间阅读这份欢迎稿，点击 <i class="icon-file"></i> (Ctrl+Alt+N) 开始撰写新的文稿吧！祝您在这里记录、阅读、分享愉快！

作者 [@kh-1997][3]     
2020 年 03月21日    