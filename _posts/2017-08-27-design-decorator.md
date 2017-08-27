---
layout: post
title: 设计模式 Decorator Pattern
date: 2017-08-26 11:29:08 +0800
tags: [Decorator Pattern]
---
## 装饰器模式

动态地给一个对象添加一些额外的责则。用于需要透明且动态地扩展类的功能。

![装饰器模式UML](https://raw.githubusercontent.com/mupu-mupu/mupu-mupu.github.io/master/image-data/design_pattern/decorator.png)


----------


### UML类图分析
- Component:抽象组件
     可以是一个接口或是抽象类，作为最原始的装饰对象。  
- ConcreteConponent：组件具体实现类
     该类是Conponent类的基本实现，也是被装饰的具体对象。
- Decorator:抽象装饰者
     提供公共的装饰者。
- ConcreteDecoratorA：装饰者具体实现类。

```
//代码栗子
Component component = new ConcreteConponent();
Decorator decorateor = new ConcreteDecoratorA(component);
decorator.operate();
```
 
[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/