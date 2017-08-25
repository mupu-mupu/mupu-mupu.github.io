---
layout: post
title: Java 反射机制
date: 2017-08-25 11:29:08 +0800
tags: [Java, 反射机制]
---
## 反射机制

反射机制是Java语言的一个很重要的特征，它使得Java具体了“动态性”。

```
//object 获取Class
public final Class<?> getClass()

//Class<T>常用方法
public String getName()
public native T newInstance()
public Constructor<?>[] getConstructors( 类型.class) 
public Class<?>[] getInterfaces()
public Method[] getMethods()
public native Field[] getDeclaredFields();
```

如何获取类的实例？

    1. 类名 + .class
    2. object.getClass() 
    3. Class.forName("class_name")


如何修改类的私有属性
```
Person person = new Person("mupu0");
Class<?> c = person.getClass();
Field f = c.getDeclaredField("name");
f.setAccessible(true);
//修改属性，传入要设置的对象和值
f.set(person, "mupu");
System.out.println(p);
```

如何调用类的私有方法
```
//getMethod()方法需要传入方法名，和参数类型
Method m1 = c.getMethod("print", int.class);
//传入对象和参数
m1.invoke(person, 10);
```



[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
  

 
 
  
 
 
 
