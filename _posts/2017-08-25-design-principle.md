---
layout: post
title: 设计模式 六大原则
date: 2017-08-26 11:29:08 +0800
tags: [Java, 反射机制]
---
## 设计模式原则

面向对象的六大原则：
> * Single Responsibility Principle
> * Open Close Principle
> * Liskov Substitution Principle
> * Dependence Inversion Principle
> * Interface Segregation Principle
> * Law of Demeter

### 单一职责原则：
一个类中应该是一组相关性很高的函数。

### 开闭原则：
对扩展开放，对修改关闭。


### 依赖倒置：

- 高层模块不应该依赖底层模块，两者应该依赖抽象。
- 抽象不应该依赖细节。
- 细节应该依赖抽象。

注：java中抽象为：接口或抽象类，细节：实现类。

举个栗子，ImageLoad依赖于ImageCache抽象，而不是其具体实现类，即面向接口编程，这就是依赖倒置。

### 接口隔离原则：
客户端不应该依赖它不需要的接口。或者：类间的依赖关系应该建立在最小的接口上。
接口隔离原则的目的是系统解开耦合，从而容易重构，更改和重新部署。

1.对最小接口操作。
2.隐藏具体实现的方法。

```
private static final IPolicy sPolicy;
Class policyClass = Class.fromName(POLICY_IMPL_CLASS_NAME);
sPolicy = (IPolicy) policy.newInstance();
```


### 里氏替换原则:
低耦合，高内聚

### 迪米特法则：
在使用基类的的地方可以任意使用其子类，能保证子类完美替换基类。


[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
  

 
 
  
 
 
 
