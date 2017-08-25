---
layout: post
title: Android Serializable
date: 2017-08-23 11:29:08 +0800
tags: [Android, Serializable, Parcelable]
---


## 对象序列化

1. 序列化作用：
       - 通过Binder和Intent传输数据。
       - 将对象持久化到存储设备。
       - 通过网络传输给其他客户端。
2. 静态成员变量属于类不属于对象，所以不会参与到序列化的过程。
3. 使用transient关键字标记的成员也不会参加序列化过程。


----------


### Serializable接口

适用场景：2,3
简介：
    Serializable是java序列化的接口，使用简单但是开销大，序列化和反序列化都需要大量的IO操作。
实现：
对象的序列化需要该类实现Serializable接口并声明一个serialVersionUID即可。


```
//序列化过程
User user = new User(20255188,"mupu");
ObjectOutputSream out = new ObjectOutputSteam(new FileOutputStream("cache.text"));
out.writeObject(user);
out.close();

//反序列化
ObjectInputStream in = new ObjectInputStream(new FileInputSream("cache.text"));
User user = (User) in.readObject();
in.close();

```


----------


### Parcelable接口

适用场景：1

简介： 
Parcelable是Android的序列化接口，效率高。
实现：
系统提供了很多实现了Parcelable接口的类，他们都是可以直接序列化，比如：Intent,Bundle,Bitmap,List,Map,其中集合中的每个元素都是可序列化的。


```
public class User implements Parcelable {

    public int userId;
    public String userName;
    public Book book;

    //内容描述
    @Override
    public int describeContents() {
        return 0;
    }
    //序列化对象
    @Override
    public void writeToParcel(Parcel parcel, int i) {
        parcel.writeInt(userId);
        parcel.writeString(userName);
        parcel.writeParcelable(book);
    }
    //反序列化对象
    public static final Creator<User> CREATOR = new Creator<User>() {
        @Override
        public User createFromParcel(Parcel in) {
            return new User(in);
        }
        @Override
        public User[] newArray(int size) {
            return new User[size];
        }
    };
    //反序列化对象实例
    protected User(Parcel in) {
        userId = in.readInt();
        userName = in.readString();
        //对象反序列化需要classloader
        book = in.readParcelable(Thread.currentThread().getContextClassLoader());
    }

}
```


[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
  

 
 
  
 
 
 
