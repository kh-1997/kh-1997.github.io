---
layout: post
title: 'ReentrantLock'
subtitle: 'ReentrantLock'
date: 2020-04-18
categories: program
cover: 'http://on2171g4d.bkt.clouddn.com/jekyll-theme-h2o-postcover.jpg'
tags: 高并发
---

# JAVA高并发

------

# ReentrantLock

我们理解您需要更便捷更高效的工具记录思想，整理笔记、知识，并将其中承载的价值传播给他人，**Cmd Markdown** 是我们给出的答案 —— 我们为记录思想和分享知识提供更专业的工具。 您可以使用 Cmd Markdown：

> * 整理知识，学习笔记
> * 发布日记，杂文，所见所想
> * 撰写发布技术文稿（代码支持）
> * 撰写发布学术论文（LaTeX 公式支持）

![cmd-markdown-logo](https://www.zybuluo.com/static/img/logo.png)



# ReentrantLock底层语义原理

（1）Lock和ReadWriteLock是两大锁的根接口，Lock代表实现类是ReentrantLock（可重入锁），ReadWriteLock（读写锁）的代表实现类是ReentrantReadWriteLock。Lock 接口支持那些语义不同（重入、公平等）的锁规则，可以在非阻塞式结构的上下文（包括 hand-over-hand 和锁重排算法）中使用这些规则。主要的实现是 ReentrantLock。ReadWriteLock 接口以类似方式定义了一些读取者可以共享而写入者独占的锁。此包只提供了一个实现，即 ReentrantReadWriteLock，因为它适用于大部分的标准用法上下文。但程序员可以创建自己的、适用于非标准要求的实现。

（2）Condition 接口描述了可能会与锁有关联的条件变量。这些变量在用法上与使用 Object.wait 访问的隐式监视器类似，但提供了更强大的功能。需要特别指出的是，单个 Lock 可能与多个 Condition 对象关联。为了避免兼容性问题，Condition 方法的名称与对应的 Object 版本中的不同。



**二：synchronized的缺陷**

　　synchronized是java中的一个关键字，也就是说是Java语言内置的特性。那么为什么会出现Lock呢？

　　1）Lock不是Java语言内置的，synchronized是Java语言的关键字，因此是内置特性。Lock是一个类，通过这个类可以实现同步访问；

　　2）Lock和synchronized有一点非常大的不同，采用synchronized不需要用户去手动释放锁，当synchronized方法或者synchronized代码块执行完之后，系统会自动让线程释放对锁的占用；而Lock则必须要用户去手动释放锁，如果没有主动释放锁，就有可能导致出现死锁现象。

**synchronized 的局限性 与 Lock 的优点**　

　　如果一个代码块被synchronized关键字修饰，当一个线程获取了对应的锁，并执行该代码块时，其他线程便只能一直等待直至占有锁的线程释放锁。事实上，占有锁的线程释放锁一般会是以下三种情况之一：

　　1：占有锁的线程执行完了该代码块，然后释放对锁的占有；

　　2：占有锁线程执行发生异常，此时JVM会让线程自动释放锁；

　　3：占有锁线程进入 WAITING 状态从而释放锁，例如在该线程中调用wait()方法等。

　　试考虑以下三种情况：　

Case 1 ： 响应中断

　　在使用synchronized关键字的情形下，假如占有锁的线程由于要等待IO或者其他原因（比如调用sleep方法）被阻塞了，但是又没有释放锁，那么其他线程就只能一直等待，别无他法。这会极大影响程序执行效率。因此，就需要有一种机制可以不让等待的线程一直无期限地等待下去（比如只等待一定的时间 (解决方案：tryLock(long time, TimeUnit unit)) 或者 能够响应中断 (解决方案：lockInterruptibly())），这种情况可以通过 Lock 解决。

Case 2 ：不能同时读

　　我们知道，当多个线程读写文件时，读操作和写操作会发生冲突现象，写操作和写操作也会发生冲突现象，但是读操作和读操作不会发生冲突现象。但是如果采用synchronized关键字实现同步的话，就会导致一个问题，即当多个线程都只是进行读操作时，也只有一个线程在可以进行读操作，其他线程只能等待锁的释放而无法进行读操作。因此，需要一种机制来使得当多个线程都只是进行读操作时，线程之间不会发生冲突。同样地，Lock也可以解决这种情况 (解决方案：ReentrantReadWriteLock) 。

Case 3 ：获取所得情况

　　我们可以通过Lock得知线程有没有成功获取到锁 (解决方案：ReentrantLock) ，但这个是synchronized无法办到的。

上面提到的三种情形，我们都可以通过Lock来解决，但 synchronized 关键字却无能为力。事实上，Lock 是 java.util.concurrent.locks包 下的接口，Lock 实现提供了比 synchronized 关键字 更广泛的锁操作，它能以更优雅的方式处理线程同步问题。也就是说，Lock提供了比synchronized更多的功能。

当一个线程获取了锁之后，是不会被interrupt()方法中断的。因为interrupt()方法只能中断阻塞过程中的线程而不能中断正在运行过程中的线程。因此，当通过lockInterruptibly()方法获取某个锁时，如果不能获取到，那么只有进行等待的情况下，才可以响应中断的。与 synchronized 相比，当一个线程处于等待某个锁的状态，是无法被中断的，只有一直等待下去。



1）synchronized是Java语言的关键字，因此是内置特性，Lock不是Java语言内置的，Lock是一个接口，通过实现类可以实现同步访问。

2）synchronized是在JVM层面上实现的，不但可以通过一些监控工具监控synchronized的锁定，而且在代码执行时出现异常，JVM会自动释放锁定，但是使用Lock则不行，lock是通过代码实现的，要保证锁定一定会被释放，就必须将unLock()放到finally{}中

3）在资源竞争不是很激烈的情况下，Synchronized的性能要优于ReetrantLock，但是在资源竞争很激烈的情况下，Synchronized的性能会下降几十倍，但是ReetrantLock的性能能维持常态。



1、可重入锁
　　如果锁具备可重入性，则称作为 可重入锁 。像 synchronized和ReentrantLock都是可重入锁，可重入性在我看来实际上表明了 锁的分配机制：基于线程的分配，而不是基于方法调用的分配。举个简单的例子，当一个线程执行到某个synchronized方法时，比如说method1，而在method1中会调用另外一个synchronized方法method2，此时线程不必重新去申请锁，而是可以直接执行方法method2。

```
class MyClass {
    public synchronized void method1() {
        method2();
    }

    public synchronized void method2() {

    }
}
```

上述代码中的两个方法method1和method2都用synchronized修饰了。假如某一时刻，线程A执行到了method1，此时线程A获取了这个对象的锁，而由于method2也是synchronized方法，假如synchronized不具备可重入性，此时线程A需要重新申请锁。但是，这就会造成死锁，因为线程A已经持有了该对象的锁，而又在申请获取该对象的锁，这样就会线程A一直等待永远不会获取到的锁。而由于synchronized和Lock都具备可重入性，所以不会发生上述现象。

2、可中断锁

　　顾名思义，可中断锁就是可以响应中断的锁。在Java中，synchronized就不是可中断锁，而Lock是可中断锁。
　　如果某一线程A正在执行锁中的代码，另一线程B正在等待获取该锁，可能由于等待时间过长，线程B不想等待了，想先处理其他事情，我们可以让它中断自己或者在别的线程中中断它，这种就是可中断锁。在前面演示tryLock(long time, TimeUnit unit)和lockInterruptibly()的用法时已经体现了Lock的可中断性。

3、公平锁

　　公平锁即 尽量 以请求锁的顺序来获取锁。比如，同是有多个线程在等待一个锁，当这个锁被释放时，等待时间最久的线程（最先请求的线程）会获得该所，这种就是公平锁。而非公平锁则无法保证锁的获取是按照请求锁的顺序进行的，这样就可能导致某个或者一些线程永远获取不到锁。在Java中，synchronized就是非公平锁，它无法保证等待的线程获取锁的顺序。而对于ReentrantLock 和 ReentrantReadWriteLock，它默认情况下是非公平锁，但是可以设置为公平锁。

4、ReentrantLock的实现依赖硬件支持CAS操作
 Compare and swap
 原始值，目标值，期望值
 当目标值 = 期望值时，认为修改成功。
 当目标值 ！=  期望值时，肯定是别的操作已经修改了。放弃

jdk下的并发包Atomic目录下的类就是封装了原子的操作类

AQS内部抽象类
 AbstractQueuedSynchronizer
 主要的成员变量
 state volitile修饰表示锁被抢占的状态，对它的修改都是用的cas操作
 一个双向链表，其中每个Node节点信息：
 waitstatus四个状态值singal cancel 初始化 condition 独占模式还是共享模式
 线程的信息
 前序节点 后序节点

加锁的过程
 公平锁，直接放到队列尾
 非公平锁，先尝试加锁，没有抢到放到队尾
 查看status是否为0，是的线程抢占到锁。
 不为0，则addWaiter操作，在双向链表的尾部添加node节点。这步操作也是CAS操作，保证多线程的安全。
 之后进入死循环，检查前序节点是否为head节点。
 前序节点是head的话，抢占锁。如果不是head节点的话，线程进入阻塞状态。

解锁的过程
 解锁后，status-1。当status为0时。
 通知head节点的下一个节点，唤醒状态。从而进入上述的死循环。



而我们知道**Java中AtomicInteger类可以直接将读和写封装在一个原子操作中实现原子化的i++等操作，那它们是怎么实现的呢？**我们接下来进行探讨。

## **3 硬件CAS操作**

Java中AtomicInteger类便可以将读和写封装在一个原子操作中。那它是怎么实现的呢？

它使用的是CAS操作。**CAS是compare and swap的缩写，中文可以翻译成：比较并交换。**CAS操作来源于底层硬件领域。因为CAS能够极大地提高并发效率，因此在硬件设计领域，CAS这种操作就是存在的。例如在intel的CPU中，使用cmpxchg指令就可以实现CAS操作。我们详细介绍下CAS操作的原理：

在Java初期，java是无法直接利用这些硬件操作来提升并发性能的，直到后来Java本地方法(JNI)的出现，使得Java直接调用本地方法称为可能，在Doug Lea提供的cucurenct包得以实现。

在Java中如何实现呢？其实知道了CAS操作的原理，一下就变得简单起来。我们还是以i++操作为例，介绍CAS整个过程：



1. 读取内存位置V的原值R
2. 因为进行的是i++操作，因此CAS操作的预期原值A=R、新值B=R+1，进行CAS。
3. 获取V的原值R

- 如果R等于A，更改成功，操作结束
- 如果R不等于A，则没有更改。但是获取当前时刻V的原值，将R重新设置为该值。则预期原值A=R、新值B=R+1，然后在继续进行CVS。






### 文稿发布和分享

在您使用 Cmd Markdown 记录，创作，整理，阅读文稿的同时，我们不仅希望它是一个有力的工具，更希望您的思想和知识通过这个平台，连同优质的阅读体验，将他们分享给有相同志趣的人，进而鼓励更多的人来到这里记录分享他们的思想和知识，尝试点击 <i class="icon-share"></i> (Ctrl+Alt+P) 发布这份文档给好友吧！

------

再一次感谢您花费时间阅读这份欢迎稿，点击 <i class="icon-file"></i> (Ctrl+Alt+N) 开始撰写新的文稿吧！祝您在这里记录、阅读、分享愉快！

作者 [@kh-1997][3]     
2020 年 03月08日    