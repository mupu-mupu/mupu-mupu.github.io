---
layout: post
title: Android 多线程
date: 2016-11-21 11:29:08 +0800
tags: [Android, ThreadPool]
---

## Java线程 ##

 - 继承Thread并重写run方法
 - 实现Runnable接口
 

 Thread本身实现了Runnable接口，通过一些状态对Thread进行管理与调度。

### 基本函数 ###

 - wait()
执行wait()方法时，线程会进入到一个和对象相关的等待池中，同时`释放了该对象的线程锁`,可以使用notify、notifyAll、指定睡眠时间来唤醒当前线程。

 - sleep()
静态函数，所以不能改变对象的线程锁，所以在`Synchronized block`中调用该方法其他线程依旧无法访问。

 - join
等待目标线程完成后再继续执行。Block the current Thread,until the receiver finishes its execution and dies.

 - yield
线程礼让。目标线程由运行状态转变为就绪状态，让其他线程优先执行。但是其他线程是否优先执行是未知的。Causes the calling thread to yield execution time to another thread that is ready to run.


----------


## Android中的线程 ##

> * AsyncTask（Android 3.0以后不支持并发）
> * HandlerThread
> * IntentService
 

### AsyncTask(重点介绍) ###

#### AsyncTask作为轻量级的异步任务类，主要用于后台执行任务并更新UI。

```java
//泛型支持
public abstract class AsyncTask<Params, ProgressType, ResultType>

//重写AsyncTask四个方法
public class MyThreadTask extends AsyncTask{Params, ProgressType, ResultType}

//执行后台任务
MyThreadTask.execute(param, param1, param2);

```
 
 - onPreExecute()
 - doInBackground  (Param...        params)
 - onProgressUpdate(ProgressType... progress)
 - onPostExecute   (Result...       result)

注：
 - AsyncTask必须在主线程中执行。
 - execute方法必须在UI线程中执行。
 - AysncTask对象只能执行一次

----------


## 线程池的管理 ##
线程池都实现了`ExecutorService`接口，该接口提供了线程池需要实现的接口，如submit，execute，shutdowm等，使用JDK提供的Executor工厂类创建对象。

 - ThreadPoolExecutor
 - ScheduleThreadPoolExecutor


### 1. 线程池的作用 ###
 - 重用存在的线程，减少对象的创建和销毁开销。
 - 可以有效的控制最大并发线程数，提高系统资源的利用率，避免过多资源竞争，避免堵塞。
 - 提供定时执行，定期执行，单线程等功能。


----------

## 同步集合 ##

### 1. 优化策略(空间换时间)

 - CopyOnWriteArrayList
 - CopyOnWriteArraySet

### 2. 提供并发效率
 - ConcurrentHashMap
HashTable通过Synchronized保证线程安全，但是在激烈的线程竞争下效率十分低下，HashMap线程不安全。为了解决这个问题，引入ConcurrentHashMap使用的`锁分段技术`。

### 3. 有效的方法

阻塞队列提供了一系列有效的特性，比如在BlokingEQueue队列满了时，再向该队列put函数添加元素时，调用线程会阻塞，直到线程不是填满状态时。

 - BlockingQueue //JDK
 - ArrayBlokingQueue
 - LinkedBlokingQueue
 - LinkedBlokingDeque


----------


## 同步锁 ##

### 1. 同步机制关键字----synchronized
synchronized关键字可作用于对象，函数，class（整个类而不是某给对象）。

 1）锁定Class中的对象
 
    //同步方法，同步块
    public synchronized void method(){}
    public void method(){
        synchronized(this){}
    }

 2）锁定Class
 
    //锁定Class对象,静态代码块
    public void method(){
        synchronized(MainActivity.class){}
    }
    public syschronized static void method(){}
    
### 2. 显示锁 ----ReentrantLock与Condition

Java 6.0之后引入的机制，相对于synchronized缺点是JVM无法获取到lock所在的线程信息，不利于调试。

 - 获取和释放的灵活性
 - 轮询锁和定时锁
 - 公平性


 | 函数        | 作用  |
| --  | :-----  |
| lock()     | 获取锁 |
| tryLock()        |  尝试获取锁   | 
| unLock()        |  释放锁   |  
| newCondition()   |    获取锁的condition    |  


[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
  

 
 
  
 
 
 
