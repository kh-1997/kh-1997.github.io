---

layout: post
title: '建造者模式'
subtitle: '建造者模式'
date: 2020-03-04
categories: 技术
cover: 'http://on2171g4d.bkt.clouddn.com/jekyll-theme-h2o-postcover.jpg'
tags: 设计模式﻿
---

# 设计模式九

------

# 对象创建

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

## 建造者模式

- 使用场景：将产品的创建过程与产品本身解耦，对象的创建流程比较复杂。

- 使用原理：将对象的属性与对象的创建过程分离，将创建过程抽象到builder类里面，具体的对象由具体的builder重写build类的方法进行创建，然后返回。在Director里面设置具体的builder创建步骤进行build。

- ![image-20200304113020323](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200304113020323.png)

  ![image-20200304112538641](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200304112538641.png)

  ![image-20200304112503789](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200304112503789.png)


抽象工厂vs建造者模式

建造者模式强调分步骤构建一个复杂的对象，抽象工厂强调按照某些要求一块创建多个不同对象。









### 文稿发布和分享

在您使用 Cmd Markdown 记录，创作，整理，阅读文稿的同时，我们不仅希望它是一个有力的工具，更希望您的思想和知识通过这个平台，连同优质的阅读体验，将他们分享给有相同志趣的人，进而鼓励更多的人来到这里记录分享他们的思想和知识，尝试点击 <i class="icon-share"></i> (Ctrl+Alt+P) 发布这份文档给好友吧！

------

再一次感谢您花费时间阅读这份欢迎稿，点击 <i class="icon-file"></i> (Ctrl+Alt+N) 开始撰写新的文稿吧！祝您在这里记录、阅读、分享愉快！

作者 [@kh-1997][3]     
2020 年 03月4日    