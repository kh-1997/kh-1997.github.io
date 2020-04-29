---

layout: post
title: '抽象工厂模式'
subtitle: '抽象工厂模式'
date: 2020-03-02
categories: 技术
cover: 'http://on2171g4d.bkt.clouddn.com/jekyll-theme-h2o-postcover.jpg'
tags: 设计模式﻿
---

# 设计模式七

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

## 抽象工厂

- 使用场景：在软件系统中，对象创建的时候经常面临着“一系列相互依赖的对象”的创建工作；同时，由于需求的变化，往往存在更多系列对象的创建工作。

- 使用原理：提供一个接口，让该接口负责创建一系列“相关或者相互依赖的对象”，无需指定它们具体的类。

- 设计原则：

- 依赖倒转原则：将变化进行隔离，使高层依赖于抽象，具体实现依赖于抽象

- 抽象类-具体类

- 抽象工厂类-具体工厂类

- 抽象类=抽象工厂类->createMethod()

  

  ![image-20200303193954664](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200303193954664.png)

  ```
  //数据库访问有关的基类
  class IDBConnection{
      
  };
  
  class IDBCommand{
      
  };
  
  class IDataReader{
      
  };
  
  //支持SQL Server
  class SqlConnection: public IDBConnection{
      
  };
  class SqlCommand: public IDBCommand{
      
  };
  class SqlDataReader: public IDataReader{
      
  };
  
  //支持Oracle
class OracleConnection: public IDBConnection{
      
  };
  
  class OracleCommand: public IDBCommand{
      
  };
  
  class OracleDataReader: public IDataReader{
      
  };
  
  ```
  
  ```
  //工厂基类
  class IDBFactory{
  public:
      virtual IDBConnection* CreateDBConnection()=0;
      virtual IDBCommand* CreateDBCommand()=0;
      virtual IDataReader* CreateDataReader()=0;
      
  };
  
  //具体工厂
  class SqlDBFactory:public IDBFactory{
  public:
      virtual IDBConnection* CreateDBConnection()=0;
      virtual IDBCommand* CreateDBCommand()=0;
      virtual IDataReader* CreateDataReader()=0;
   
  };
  
  class OracleDBFactory:public IDBFactory{
  public:
      virtual IDBConnection* CreateDBConnection()=0;
      virtual IDBCommand* CreateDBCommand()=0;
      virtual IDataReader* CreateDataReader()=0;
 
  };
  
  ```
  
  ```
  class EmployeeDAO{
      IDBFactory* dbFactory;
      
  public:
      vector<EmployeeDO> GetEmployees(){
          IDBConnection* connection = dbFactory->CreateDBConnection();
          connection->ConnectionString("...");
  
          IDBCommand* command =
              dbFactory->CreateDBCommand();
          command->CommandText("...");
          command->SetConnection(connection); //关联性
  
          IDBDataReader* reader = command->ExecuteReader(); //关联性
          while (reader->Read()){
          }
      }
  };
  
  ```

1. 如果没有应对“多系列对象构建”的需求变化，则没有必要使用 Abstract Factory模式，这时候使用简单的工厂完全可以。 
2. “系列对象”指的是在某一特定系列下的对象之间有相互依赖、 或作用的关系。不同系列的对象之间不能相互依赖。 
3. Abstract Factory模式主要在于应对“新系列”的需求变动。其缺点在于难以应对“新对象”的需求变动。

### 文稿发布和分享

在您使用 Cmd Markdown 记录，创作，整理，阅读文稿的同时，我们不仅希望它是一个有力的工具，更希望您的思想和知识通过这个平台，连同优质的阅读体验，将他们分享给有相同志趣的人，进而鼓励更多的人来到这里记录分享他们的思想和知识，尝试点击 <i class="icon-share"></i> (Ctrl+Alt+P) 发布这份文档给好友吧！

------

再一次感谢您花费时间阅读这份欢迎稿，点击 <i class="icon-file"></i> (Ctrl+Alt+N) 开始撰写新的文稿吧！祝您在这里记录、阅读、分享愉快！

作者 [@kh-1997][3]     
2020 年 03月3日    