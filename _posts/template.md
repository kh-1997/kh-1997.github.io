---
layout:     post
title:      "线程池原理讲解"
subtitle:   " \"线程池\""
date:       2020-03-29 12:00:00
author:     "KH"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - 多线程
    - Meta
---

> “Yeah It's on. ”

[跳过废话，直接看技术实现 ](#build) 

2020 年，kh 总算有个地方可以好好写点东西了。

------

# 线程池原理详解

### [Windows/Mac/Linux 全平台客户端]

> JAVA帮助开发者封装了一些现成的线程池调用，但是每种线程池都有自己的使用场景，如果不了解里面的原理，那么很容易掉进坑里，线程池原理也是面试的重灾区，因此本问将完整分析线程池的原理。

## 一、new thread弊端

从学习java多线程开始，我们就学习了用`new thread`来创建线程。但是他有一定的弊端：

- 每次`new Thread`新建对象，性能差
- 线程缺乏统一管理，可能无限制的新建线程，相互竞争，有可能占用过多系统资源导致死机或OOM
- 缺少更多功能，如更多执行、定期执行、线程中断

## 二、线程池好处

- 重用存在的线程，减少对象创建、消亡的开销，性能佳
- 可有效控制最大并发线程数，提高系统资源利用率，同时可以避免过多资源竞争，避免阻塞
- 提供定时执行、定期执行、单线程、并发数控制等功能

## 三、线程池相关参数

```
public ThreadPoolExecutor(int corePoolSize,
                          int maximumPoolSize,
                          long keepAliveTime,
                          TimeUnit unit,
                          BlockingQueue<Runnable> workQueue,
                          ThreadFactory threadFactory,
                          RejectedExecutionHandler handler)
```

- `corePoolSize`:核心线程数量

> 默认情况下，在创建了线程池后，线程池中的线程数为0，
> （除非调用`prestartAllCoreThreads()`和`prestartCoreThread()`方法，从方法名字可以看出，是预创建线程的意思，即在没有任务到来之前，就创建`corePoolSize`个线程或1个线程）当有任务来之后，就会创建一个线程去执行任务，当线程池中的线程数目达到`corePoolSize`后，就会把到达的任务放到缓存队列当中；
>
> 当提交一个任务到线程池时，线程池会创建一个线程来执行任务，即使其他空闲的基本线程能够执行新任务也会创建线程，等到需要执行的任务数大于线程池基本大小时就不再创建。

- `maximumPoolSize`:线程最大线程数

> 线程池中的最大线程数，表示线程池中最多能创建多少个线程。
>
> 超过就执行`reject`策略:如果队列满了,并且已创建的线程数小于最大线程数，则线程池会再创建新的线程执行任务

- `workQueue`:阻塞队列，存储等待执行的任务，很重要，会对线程池运行过程产生重大影响，一般有以下几种选择：

> `ArrayBlockingQueue`：是一个基于数组结构的有界阻塞队列，此队列按 `FIFO`（先进先出）原则对元素进行排序；
>
> `LinkedBlockingQueue`：一个基于链表结构的阻塞队列，此队列按FIFO （先进先出） 排序元素，吞吐量通常要高于`ArrayBlockingQueue`。静态工厂方法`Executors.newFixedThreadPool()`使用了这个队列；
>
> `SynchronousQueue`：一个不存储元素的阻塞队列。每个插入操作必须等到另一个线程调用移除操作，否则插入操作一直处于阻塞状态，吞吐量通常要高于`LinkedBlockingQueue`，静态工厂方法`Executors.newCachedThreadPool`使用了这个队列；
>
> `PriorityBlockingQueue`：一个具有优先级的无限阻塞队列；底层用`DelayedWorkQueue`实现。

- `keepAliveTime`：线程没有任务执行时最多保持多久时间终止
- `unit`:`keepAliveTime`的时间单位

> 当线程池中的线程数大于`corePoolSize`时，如果一个线程空闲的时间达到`keepAliveTime`，则会终止，直到线程池中的线程数不超过`corePoolSize`。（但是如果调用了`allowCoreThreadTimeOut(boolean value)`方法，在线程池中的线程数不大于`corePoolSize`时，`keepAliveTime`参数也会起作用，直到线程池中的线程数为0；）

- `threadFactory`：线程工厂，用来创建线程

> `threadFactory`用于设置创建线程的工厂，可以通过线程工厂给每个创建出来的线程设置更有意义的名字

- `handler`:饱和策略

> 当队列和线程池都满了，说明线程池处于饱和状态，那么必须采取一种策略处理提交的新任务。这个策略默认情况下是`AbortPolicy`，表示无法处理新任务时抛出异常。

这些参数全部传给`ThreadPoolExecutor`之后，`ThreadPoolExecutor`就可以为我们提供一个线程池，我们可以对这个线程池提交以及终止线程任务。

## 四、拒绝策略

当线程池中已经到了完全没有办法再接收新的线程进来的时候，就会启动饱和策略。

```
java.util.concurrent.ThreadPoolExecutor.AbortPolicy
java.util.concurrent.ThreadPoolExecutor.CallerRunsPolicy
java.util.concurrent.ThreadPoolExecutor.DiscardOldestPolicy
java.util.concurrent.ThreadPoolExecutor.DiscardPolicy
```

1. `AbortPolicy`：丢弃任务并抛出`RejectedExecutionException`异常（默认）
2. `CallerRunsPolicy`：只用调用所在的线程运行任务
3. `DiscardOldestPolicy`：丢弃队列最前面的任务，然后重新尝试执行任务（重复此过程）
4. `DiscardPolicy`：不处理，丢弃掉,不抛出异常。

# **配置线程池的大小**

一般需要根据任务的类型来配置线程池大小：

 如果是CPU密集型任务，就需要尽量压榨CPU，参考值可以设为 NCPU+1；

 如果是IO密集型任务，参考值可以设置为2*NCPU。

当然，这只是一个参考值，具体的设置还需要根据实际情况进行调整，比如可以先将线程池大小设置为参考值，再观察任务运行情况和系统负载、资源利用率来进行适当调整。

Ncpu为CPU的数量，Ucpu为CPU的利用率，W/C为任务的等待时间 / 任务的计算时间。在这种情况下，一般线程池的最优大小: 

​															N=Ncpu\*Ucpu\*（1+W/C）

# **是否使用线程池就一定比使用单线程高效呢？**

**答案是否定的**，比如Redis就是单线程的，但它却非常高效，基本操作都能达到十万量级/s。从线程这个角度来看，部分原因在于：多线程带来线程上下文切换开销，单线程就没有这种开销 。

当然“Redis很快”更本质的原因在于：Redis基本都是内存操作，这种情况下单线程可以很高效地利用CPU。而多线程适用场景一般是：存在相当比例的IO和网络操作。

**线程数量要点**：

 如果运行线程的数量**少于**核心线程数量，则**创建新**的线程处理请求

 如果运行线程的数量**大于**核心线程数量，**小于**最大线程数量，则当**队列满的时候才创建新**的线程

 如果核心线程数量**等于**最大线程数量，那么将**创建固定大小**的连接池

 如果设置了最大线程数量为**无穷**，那么允许线程池适合**任意**的并发数量

**线程空闲时间要点：**

 当前线程数**大于**核心线程数，如果空闲时间已经超过了，那该线程会**销毁**。

**排队策略要点**：

 同步移交：**不会放到队列中，而是等待线程执行它**。如果当前线程没有执行，很可能会**新开**一个线程执行。

 无界限策略：**如果核心线程都在工作，该线程会放到队列中**。所以线程数不会超过核心线程数

 有界限策略：**可以避免资源耗尽**，但是一定程度上减低了吞吐量

当线程关闭或者线程数量满了和队列饱和了，就有拒绝任务的情况了：

**拒绝任务策略：**

 直接抛出异常

 使用调用者的线程来处理

 直接丢掉这个任务

 丢掉最老的任务

# 线程池结构

![img](https://images2018.cnblogs.com/blog/588112/201806/588112-20180628163840819-364098536.png)

# **线程生命周期**

 ![img](https://images2018.cnblogs.com/blog/588112/201806/588112-20180628163919685-2055436585.png)

在线程的生命周期中，它要经过新建(New)、就绪（Runnable）、运行（Running）、阻塞(Blocked)和死亡(Dead)5种状态。

Thread通过new来新建一个线程，这个过程是是初始化一些线程信息，如线程名，id,线程所属group等，可以认为只是个普通的对象。调用Thread的start()后Java虚拟机会为其创建方法调用栈和程序计数器，同时将hasBeenStarted为true,之后调用start方法就会有异常。

处于这个状态中的线程并没有开始运行，只是表示该线程可以运行了。至于该线程何时开始运行，取决于JVM里线程调度器的调度。当线程获取cpu后，run()方法会被调用。不要自己去调用Thread的run()方法。之后根据CPU的调度在就绪——运行——阻塞间切换，直到run()方法结束或其他方式停止线程，进入dead状态。

## 线程池的源码解读

##### ThreadPoolExecutor重要方法

所以，用于`execute()`或者`submit()`的线程任务都是被封装成`worker`去执行的。下面来看看`execute()`和`submit()`等核心方法。

在`ThreadPoolExecutor`类中有几个非常重要的方法：

- `execute()`

> `execute()`方法实际上是`Executor`中声明的方法，在`ThreadPoolExecutor`进行了具体的实现，这个方法是`ThreadPoolExecutor`的核心方法，通过这个方法可以向线程池提交一个任务，交由线程池去执行。

- `submit()`

> `submit()`方法是在`ExecutorService`中声明的方法,这个方法也是用来向线程池提交任务的，但是它和`execute()`方法不同，它能够返回任务执行的结果，去看`submit()`方法的实现，会发现它实际上还是调用的`execute()`方法，只不过它利用了`Future`来获取任务执行结果。

- `shutdown()`
  将线程池状态置为`SHUTDOWN`,并不会立即停止：

> 停止接收外部`submit`的任务内部正在跑的任务和队列里等待的任务，会执行完等到第二步完成后，才真正停止

- `shutdownNow()`
  将线程池状态置为`STOP`。企图立即停止，事实上不一定：

> 跟`shutdown()`一样，先停止接收外部提交的任务忽略队列里等待的任务尝试将正在跑的任务`interrupt`中断返回未执行的任务列表
>
> 它试图终止线程的方法是通过调用`Thread.interrupt()`方法来实现的，但是大家知道，这种方法的作用有限，如果线程中没有`sleep` 、`wait`、`Condition`、定时锁等应用, `interrupt()`方法是无法中断当前的线程的。所以，`ShutdownNow()`并不代表线程池就一定立即就能退出，它也可能必须要等待所有正在执行的任务都执行完成了才能退出。但是大多数时候是能立即退出的

- `awaitTermination(long timeOut, TimeUnit unit)`

> 接收`timeout`和`TimeUnit`两个参数，用于设定超时时间及单位。当等待超过设定时间时，会监测`ExecutorService`是否已经关闭，若关闭则返回`true`，否则返回`false`。一般情况下会和`shutdown`方法组合使用。

##### Executors生成线程池

要配置一个线程池是比较复杂的，尤其是对于线程池的原理不是很清楚的情况下，很有可能配置的线程池不是较优的，因此在`Executors`类里面提供了一些静态工厂，生成一些常用的线程池。这个就涉及上面我们反复提及的核心类：`ThreadPoolExecutor`。

⭐其实都是通过调用`ThreadPoolExecutor`来完成的，最后可以返回`ExecutorService`对象，其实说白了都是`Excutor`对象。

下面来分别看看比较常用的线程池。

- `newSingleThreadExecutor`

> 创建一个单线程的线程池。这个线程池只有一个线程在工作，也就是相当于单线程串行执行所有任务。如果这个唯一的线程因为异常结束，那么会有一个新的线程来替代它。此线程池保证所有任务的执行顺序按照任务的提交顺序执行。

- `newFixedThreadPool`

> 创建固定大小的线程池。每次提交一个任务就创建一个线程，直到线程达到线程池的最大大小。线程池的大小一旦达到最大值就会保持不变，如果某个线程因为执行异常而结束，那么线程池会补充一个新线程。

- `newCachedThreadPool`

> 创建一个可缓存的线程池。如果线程池的大小超过了处理任务所需要的线程，那么就会回收部分空闲（60秒不执行任务）的线程，当任务数增加时，此线程池又可以智能的添加新线程来处理任务。此线程池不会对线程池大小做限制，线程池大小完全依赖于操作系统（或者说JVM）能够创建的最大线程大小。

- `newSingleThreadScheduledExecutor`

> 创建一个单线程的线程池。此线程池支持定时以及周期性执行任务的需求。

### 文稿发布和分享

在您使用 Cmd Markdown 记录，创作，整理，阅读文稿的同时，我们不仅希望它是一个有力的工具，更希望您的思想和知识通过这个平台，连同优质的阅读体验，将他们分享给有相同志趣的人，进而鼓励更多的人来到这里记录分享他们的思想和知识，尝试点击 <i class="icon-share"></i> (Ctrl+Alt+P) 发布这份文档给好友吧！

------

再一次感谢您花费时间阅读这份欢迎稿，点击 <i class="icon-file"></i> (Ctrl+Alt+N) 开始撰写新的文稿吧！祝您在这里记录、阅读、分享愉快！

作者 [@kh-1997][3]     
2020 年 03月08日    