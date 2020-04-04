---

layout: post
title: '工厂模式'
subtitle: '工厂模式'
date: 2020-03-02
categories: 技术
cover: 'http://on2171g4d.bkt.clouddn.com/jekyll-theme-h2o-postcover.jpg'
tags: 设计模式﻿
---

# 设计模式六

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

## 工厂模式

- 使用场景：对象创建的时候，接口的右侧的仍然需要new一个具体的对象，编译时会依赖，**spring创建bean对象的通过BeanFactory创建。**

- 使用原理：定义一个创建对象的接口，让子类决定实例化哪一个类，Factor有、使得一个类的实例化（通过多态）延迟到子类。

- 设计原则：

- 依赖倒转原则：将变化进行隔离，使高层依赖于抽象，具体实现依赖于抽象

  

  ![image-20200303190015652](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200303190015652.png)

  ```
  //抽象类
  class ISplitter{
  public:
      virtual void split()=0;
      virtual ~ISplitter(){}
  };
  
  //具体类
  class BinarySplitter : public ISplitter{
      
  };
  
  class TxtSplitter: public ISplitter{
      
  };
  
  class PictureSplitter: public ISplitter{
      
  };
  
  class VideoSplitter: public ISplitter{
      
  };
  
  ```

  ```
  //工厂基类
  class SplitterFactory{
  public:
      virtual ISplitter* CreateSplitter()=0;
      virtual ~SplitterFactory(){}
  };
  
  //具体工厂
  class BinarySplitterFactory: public SplitterFactory{
  public:
      virtual ISplitter* CreateSplitter(){
          return new BinarySplitter();
      }
  };
  
  class TxtSplitterFactory: public SplitterFactory{
  public:
      virtual ISplitter* CreateSplitter(){
          return new TxtSplitter();
      }
  };
  
  class PictureSplitterFactory: public SplitterFactory{
  public:
      virtual ISplitter* CreateSplitter(){
          return new PictureSplitter();
      }
  };
  
  class VideoSplitterFactory: public SplitterFactory{
  public:
      virtual ISplitter* CreateSplitter(){
          return new VideoSplitter();
      }
  };
  ```

  ```
  class MainForm : public Form
  {
      SplitterFactory*  factory;//工厂
  public:
      MainForm(SplitterFactory*  factory){
          this->factory=factory;
      }
  	void Button1_Click(){
  		ISplitter * splitter=factory->CreateSplitter(); //多态new
          splitter->split();
  
  	}
  };
  ```

1. Factory Method模式用于隔离类对象的使用者和具体类型之间的 耦合关系。面对一个经常变化的具体类型，紧耦合关系(new)会导 致软件的脆弱。
2. Factory Method模式通过面向对象的手法，将所要创建的具体对 象工作延迟到子类，从而实现一种扩展（而非更改）的策略，较好 地解决了这种紧耦合关系。 
3. Factory Method模式解决“单个对象”的需求变化。缺点在于要 求创建方法/参数相同。

### 文稿发布和分享

在您使用 Cmd Markdown 记录，创作，整理，阅读文稿的同时，我们不仅希望它是一个有力的工具，更希望您的思想和知识通过这个平台，连同优质的阅读体验，将他们分享给有相同志趣的人，进而鼓励更多的人来到这里记录分享他们的思想和知识，尝试点击 <i class="icon-share"></i> (Ctrl+Alt+P) 发布这份文档给好友吧！

------

再一次感谢您花费时间阅读这份欢迎稿，点击 <i class="icon-file"></i> (Ctrl+Alt+N) 开始撰写新的文稿吧！祝您在这里记录、阅读、分享愉快！

作者 [@kh-1997][3]     
2020 年 03月21日    