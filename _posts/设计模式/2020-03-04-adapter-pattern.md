---

layout: post
title: '适配器模式'
subtitle: 适配器模式'
date: 2020-03-04
categories: 技术
cover: 'http://on2171g4d.bkt.clouddn.com/jekyll-theme-h2o-postcover.jpg'
tags: 设计模式﻿
---

# 设计模式十四

------

# 接口隔离

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

## 适配器模式

- 使用场景：希望复用一些现存的类，但是接口又与复用环境要求不一致的情况，在遗留代码复用，类库迁移方面非常有用。

- 
  定义：将一个类的接口转化成客户希望的另一个接口。Adapter模式使得原本由于接口不兼容而不能再一起工作的那些类可以一起工作。


- 原理：通过适配器，**组合旧的接口，继承新的接口**，利用旧的接口实现新的接口中包含的新的方法。

![image-20200304192347915](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200304192347915.png)

##### Springmvc中的适配器模式

![image-20200304195248996](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200304195248996.png)

1. spring定义了一个适配接口，使得每一种Controller都有一中对应的适配器实现类，
2. 由适配器代替controller执行相应的方法，
3. 扩展controller时，只需要增加一个适配器类就完成了springmvc的扩展。

![image-20200304195541411](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200304195541411.png)

### 文稿发布和分享

在您使用 Cmd Markdown 记录，创作，整理，阅读文稿的同时，我们不仅希望它是一个有力的工具，更希望您的思想和知识通过这个平台，连同优质的阅读体验，将他们分享给有相同志趣的人，进而鼓励更多的人来到这里记录分享他们的思想和知识，尝试点击 <i class="icon-share"></i> (Ctrl+Alt+P) 发布这份文档给好友吧！

------

再一次感谢您花费时间阅读这份欢迎稿，点击 <i class="icon-file"></i> (Ctrl+Alt+N) 开始撰写新的文稿吧！祝您在这里记录、阅读、分享愉快！

作者 [@kh-1997][3]     
2020 年 03月4日    