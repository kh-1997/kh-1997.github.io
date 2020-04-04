---
layout: post
title: '模板模式'
subtitle: '模板模式'
date: 2020-03-01
categories: 技术
cover: 'http://on2171g4d.bkt.clouddn.com/jekyll-theme-h2o-postcover.jpg'
tags: 设计模式﻿
---

# 设计模式一

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

## Template Method

使用场景：当要完成某个过程，该过程要执行一系列步骤，这一系列步骤基本相同，但其个别步骤在实现时可能不同，通常考虑用模板方法。

使用原理：父类定义模板，子类提供步骤的实现。

![1583116914(1)](C:\Users\Administrator\Desktop\1583116914(1).png)



`//抽象类，表示豆浆

	public abstract class SoyaMilk {
	//模板方法, make , 模板方法可以做成final , 不让子类去覆盖.
	final void make() {
		
		select(); 
		if（!isPureMilk){
			addCondiments();
		}
		soak();
		beat();
		
	}
	
	//选材料
	void select() {
		System.out.println("第一步：选择好的新鲜黄豆  ");
	}
	
	//添加不同的配料， 抽象方法, 子类具体实现
	abstract void addCondiments();
	
	//浸泡
	void soak() {
		System.out.println("第三步， 黄豆和配料开始浸泡， 需要3小时 ");
	}
	 
	void beat() {
		System.out.println("第四步：黄豆和配料放到豆浆机去打碎  ");
	}
	
	boolean isPureMilk（）{
		return false；
	}
	}
`

抽象类的实现类，自定义模板的部分方法

```
public class RedBeanSoyaMilk extends SoyaMilk {

	@Override
	void addCondiments() {
		// TODO Auto-generated method stub
		System.out.println(" 加入上好的红豆 ");
	}

}

```

启动类

```
public class Client {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		//制作红豆豆浆
		
		System.out.println("----制作红豆豆浆----");
		SoyaMilk redBeanSoyaMilk = new RedBeanSoyaMilk();
		redBeanSoyaMilk.make();
		
		System.out.println("----制作花生豆浆----");
		SoyaMilk peanutSoyaMilk = new PeanutSoyaMilk();
		peanutSoyaMilk.make();
	}

}
```

模板类似于框架，我们可以在抽象类的模板方法中自定义好整个算法的执行框架，将需要用户自定义的方法曝露在子类当中，有用户根据自身的需求重写，然后调用子类中的模板方法执行。

```
public class PureMilk extends SoyaMilk{
	
	@Override
	public void addCondiments(){
	};
	
	@Override
	public void isPureMilk（）{
		return true；
	}

}
```

## Spring中的模板模式

##### spring IOC 初始化容器的时候用到

 ![image-20200302111731215](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200302111731215.png)

##### 类关系图

![image-20200302111826249](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200302111826249.png)

注意：

- 钩子方法是指在父类中定义一个空方法，不做任何事，在子类在可以视情况决定要不要实现它。

- 一般模板方法加上final，防止子类重写
- 抽象类不能实例化

### 文稿发布和分享

在您使用 Cmd Markdown 记录，创作，整理，阅读文稿的同时，我们不仅希望它是一个有力的工具，更希望您的思想和知识通过这个平台，连同优质的阅读体验，将他们分享给有相同志趣的人，进而鼓励更多的人来到这里记录分享他们的思想和知识，尝试点击 <i class="icon-share"></i> (Ctrl+Alt+P) 发布这份文档给好友吧！

------

再一次感谢您花费时间阅读这份欢迎稿，点击 <i class="icon-file"></i> (Ctrl+Alt+N) 开始撰写新的文稿吧！祝您在这里记录、阅读、分享愉快！

作者 [@kh-1997][3]     
2020 年 03月21日    