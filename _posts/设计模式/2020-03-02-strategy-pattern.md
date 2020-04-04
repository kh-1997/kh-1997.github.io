---
layout: post
title: '策略模式'
subtitle: '策略模式'
date: 2020-03-02
categories: 技术
cover: 'http://on2171g4d.bkt.clouddn.com/jekyll-theme-h2o-postcover.jpg'
tags: 设计模式﻿
---

# 设计模式三

------

# 组件协作

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

## Strategy Method

1. 使用场景：Strategy模式提供了用条件判断语句以外的另一种选择，消除条件判断语句，就是在解耦合。含有许多条件判断语句的代码，并且if的情况变化不能确定的时候通常都需要Strategy模式

2. 使用原理：一方定义策略，将策略基类聚合到另一方类中，在另一方的具体实现类中进行不同策略调用。
3. 设计原则：

- 合成复用原则：多用组合、聚合，少用继承
- 依赖倒转原则：将变化进行隔离，使高层依赖于不变化的低层接口，具体实现依赖于接口
- 开闭原则：增加新的功能，在已有代码上进行扩展，而不修改原来的if...else代码块

![image-20200302124355109](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200302124355109.png)

分别封装策略接口，实现算法族，超类里面放策略接口对象，在子类里面设定行为对象。原则就是分离变化部分，封装接口，基于接口编程，让策略的变化独立于算法的使用者。

## JDK-Arrays中的策略模式

##### JDK的Arrays的Comparator使用了策略模式

 ![image-20200302124802484](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200302124802484.png)

##### 

### 文稿发布和分享

在您使用 Cmd Markdown 记录，创作，整理，阅读文稿的同时，我们不仅希望它是一个有力的工具，更希望您的思想和知识通过这个平台，连同优质的阅读体验，将他们分享给有相同志趣的人，进而鼓励更多的人来到这里记录分享他们的思想和知识，尝试点击 <i class="icon-share"></i> (Ctrl+Alt+P) 发布这份文档给好友吧！

------

再一次感谢您花费时间阅读这份欢迎稿，点击 <i class="icon-file"></i> (Ctrl+Alt+N) 开始撰写新的文稿吧！祝您在这里记录、阅读、分享愉快！

作者 [@kh-1997][3]     
2020 年 03月21日    