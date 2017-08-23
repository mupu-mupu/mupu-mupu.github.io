---
layout: post
title: Android消息机制
date: 2016-11-21 11:29:08 +0800
tags: [Android, Handler，Loop，Memory Leak]
---

> * UI线程为什么不会由于Looper.loop()方法导致死循环？
> * UI线程如何在Looper.loop()循环之外监听点击事件？
> * Activity的生命周期和Handler有什么关系？

## Handler运行机制##
Android的消息机制：主要指的是Handler的运行机制，Handler的运行需要底层的MessageQueue和Looper的支撑。Looper不断获取MessageQueue中的一个Message，然后交由Handler处理。

Handler消息机制UML图：
 
![关系图](https://raw.githubusercontent.com/mupu-mupu/mupu-mupu.github.io/master/image-data/android-handler/handler.png)


 - Looper
一个线程对应的只有一个Looper，所以在线程中new Handler()获得的Looper都是同一个对象，一个Looper对应的也只有一个MessageQueue。Looper实现了循环获取MessageQueue中的Message并调用Msg.target.dispatchMessage(msg)方法使得Handler执行Msg的内容。

```
//Looper构造方法，绑定MessageQueue和Thread
private Looper(boolean quitAllowed) {
        mQueue = new MessageQueue(quitAllowed);
        mThread = Thread.currentThread();
    }

//UI 线程的prepareLooper方法
public static void prepareMainLooper() {
        prepare(false);
        synchronized (Looper.class) {
            if (sMainLooper != null) {
                throw new IllegalStateException("The main Looper has already been prepared.");
            }
            sMainLooper = myLooper();
        }
    }

//实例化Looper并绑定所在线程
private static void prepare(boolean quitAllowed) {
        if (sThreadLocal.get() != null) {
            throw new RuntimeException("Only one Looper may be created per thread");
        }
        sThreadLocal.set(new Looper(quitAllowed));
    }

//Looper()具体实现
public static void loop() {
        final Looper me = myLooper();
        for (;;) {
            Messpage msg = queue.next(); // might block
            msg.target.dispatchMessage(msg);
            msg.recycleUnchecked();
        }
    }

//通过所在的线程获取Looer，Handler也是通过此方法获取到Looper
public static @Nullable Looper myLooper() {
        return sThreadLocal.get();
    }

```

 - MessageQueue
MessaggeQueue是一个消息队列，主要有以下几个方法：

```
//元素入列
enqueueMessage(Message msg,long when)
//元素出列
next()
//删除msg
removeMessage(...)

```

 - Handler

```
//获取所在线程的Looper,Queue
public Handler(Callback callback, boolean async) {
        mLooper = Looper.myLooper();
        //所有在UI线程new Handler都会获取该线程的Loop，以及MessageQueue
        mQueue = mLooper.mQueue;
        mCallback = callback;
        mAsynchronous = async;
}

```

 - ThreadLocal
 ThreadLocal保存了一个Looper对象或者与当前线程相关的数据，每一个线程都拥有自己的Value值，ThreadLocal通过value加以区分。

 `Implements a thread-local storage, that is, a variable for which each thread has its own value. All threads share the same {@code ThreadLocal} object, but each sees a different value when accessing it, and changes made by one  thread do not affect the other threads`


[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
  

 
 
  
 
 
 
