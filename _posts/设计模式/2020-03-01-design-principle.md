---
layout: post
title: '设计原则'
subtitle: '设计原则'
date: 2020-03-02
categories: 技术
cover: 'http://on2171g4d.bkt.clouddn.com/jekyll-theme-h2o-postcover.jpg'
tags: 设计模式﻿
---

# 设计模式原则

------
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

## 七大设计原则

#### 1.单一职责原则

对类来说，即一个类只负责一项职责

#### 2.接口隔离原则
客户端不应该依赖它不需要的接口，即一个类对另一个类的依赖应该建立在最小的接口上，将接口进行拆分。

#### 3.依赖倒转原则

 高层依赖抽象 细节依赖抽象 面向接口编程

#### 4.里氏替换原则

没有继承关系能不继承就别继承，必须继承子类尽量不要重写父类的方法，通过中间基本抽象借助类的聚合、组合、依赖解决问题。

#### 5.开闭原则

对扩展开放（提供方），对修改封闭闭（使用方），增加新的功能尽量通过代码的扩展而不是代码的修改，通过多态进行扩展，而不修改使用方原来的代码。

#### 6.迪米特法则（最少知道原则）
一个类应该对其他类保持最少的了解，把方法代码封装在自己类里面，而不要把自己的实现写到别人类里面去。只与自己的直接朋友通信，即别的类只出现在成员变量、方法参数、方法返回值，不出现在局部变量。

#### 7.合成复用原则
能使用聚合和合成的方式就不使用继承，传递对象的引用或者对象实例进行调用



## 九大设计分类

#### 组件协作

- 模板方法
- 策略模式
- 观察者模式

#### 单一职责

- 装饰器模式
- 桥接模式

#### 对象创建

- 工厂模式
- 抽象工厂
- 原型模式
- 建造者模式

#### 对象性能

- 单例模式
- 享元模式

#### 接口隔离

- 外观模式
- 代理模式
- 适配器模式
- 中介者模式

#### 状态变化

- 备忘录模式
- 状态模式

#### 行为变化

- 命令模式
- 访问者模式

#### 数据结构

- 组合模式
- 迭代器模式
- 责任链模式

#### 领域问题

- 解释器模式





### 文稿发布和分享

在您使用 Cmd Markdown 记录，创作，整理，阅读文稿的同时，我们不仅希望它是一个有力的工具，更希望您的思想和知识通过这个平台，连同优质的阅读体验，将他们分享给有相同志趣的人，进而鼓励更多的人来到这里记录分享他们的思想和知识，尝试点击 <i class="icon-share"></i> (Ctrl+Alt+P) 发布这份文档给好友吧！

------

再一次感谢您花费时间阅读这份欢迎稿，点击 <i class="icon-file"></i> (Ctrl+Alt+N) 开始撰写新的文稿吧！祝您在这里记录、阅读、分享愉快！

作者 [@kh-1997][3]     
2020 年 03月21日    