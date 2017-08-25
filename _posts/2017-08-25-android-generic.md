---
layout: post
title: Java 泛型
date: 2017-08-25 11:29:08 +0800
tags: [Java, 泛型]
---
## 泛型

使得代码能够应用于"某种不确定类型"，而不是一个确定的类或是接口。
T  --> type
E  --> element
K  --> key
V  --> value
N  --> number

- 泛型类
     不确定类型，使用类型参数，类名 + `<T>`
- 泛型接口，用法同泛型类
- 泛型方法
public `<T>` void setParams(T t){}


----------


## Example0:
```
/*
** Simple ViewHolder
*/
public class ViewHolder {
   @SuppressWarnings("unchecked")
   public static <T extends View> T get(View view, int id) {
        SparseArray<View> viewHolder = (SparseArray<View>) view.getTag();
        if (viewHolder == null) {
            iewHolder = new SparseArray();
            view.setTag(viewHolder);
        }
        View childView = viewHolder.get(id);
        if (childView == null) {
            childView = view.findViewById(id);
            viewHolder.put(id, childView);
        }
        return (T) childView;
    }
}

@Override
public View getView (int position,View convertView,ViewGroup parent) {
    if (convertView == null) {
        convertView = LayoutInflater.from(context).inflate(R.layout.item,parent,false);
    }
    //应用实例
    Button btn = ViewHolder.get(convertView,R.id.btn);
    return convertView;
}
```


## Example1:
     
```
/*
** get View by ID
*/
public class BaseActivity extends AppCompatActivity {
    //编译器自动强制转化
    public <T extends View> T findView(@IdRes int resId){
        return (T)findViewById(resId);
    }
}
```


[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
  

 
 
  
 
 
 
