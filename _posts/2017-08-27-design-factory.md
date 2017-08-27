---
layout: post
title: 设计模式 Factory Pattern
date: 2017-08-26 11:29:08 +0800
tags: [Observer Pattern]
---

## 工厂模式

定义一个用于创建对象的接口，让子类决定实例化哪个类。

![工厂模式UML](https://raw.githubusercontent.com/mupu-mupu/mupu-mupu.github.io/master/image-data/design_pattern/factory.png)


----------


### 使用反射的方式获取对象。

```
public class ConcreteFactory extend Factory{
     public <T extend Product> T createProduct(Class<T> mClsss){
          Product p = null;
              try{
                   p = (Product) Class.forName(mClass.getName()).newInstance(); 
               }catch(Exception e){
                    e.printStackTrace();
               }
          return (T)p;
     }
}
```

[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/