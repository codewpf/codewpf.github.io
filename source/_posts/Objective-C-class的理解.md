---
title: Objective-C class的理解
date: 2017-03-30 23:41:58
categories: 学习总结
---

以下是学习总结了Objc一些底层的知识，大部分都来源于runtime中。
[Objc 源码](https://opensource.apple.com/source/objc4/objc4-493.9/runtime/) 
[源码 下载链接](http://opensource.apple.com/tarballs/objc4/objc4-493.9.tar.gz)


# object 和 class
以上两段是来源于objc中的两个文件的源码，我们可以找到 object 和 class 的定义。

``` Objective-C
// 来源: objc/objc.h
#if !OBJC_TYPES_DEFINED
/// An opaque type that represents an Objective-C class.
typedef struct objc_class *Class;

/// Represents an instance of a class.
struct objc_object {
Class isa  OBJC_ISA_AVAILABILITY;
};

/// A pointer to an instance of a class.
typedef struct objc_object *id;
#endif
```

``` Objective-C
// 来源: objc/runtime.h
struct objc_class {
Class isa  OBJC_ISA_AVAILABILITY;

#if !__OBJC2__
Class super_class                                        OBJC2_UNAVAILABLE;
const char *name                                         OBJC2_UNAVAILABLE;
long version                                             OBJC2_UNAVAILABLE;
long info                                                OBJC2_UNAVAILABLE;
long instance_size                                       OBJC2_UNAVAILABLE;
struct objc_ivar_list *ivars                             OBJC2_UNAVAILABLE;
struct objc_method_list **methodLists                    OBJC2_UNAVAILABLE;
struct objc_cache *cache                                 OBJC2_UNAVAILABLE;
struct objc_protocol_list *protocols                     OBJC2_UNAVAILABLE;
#endif

} OBJC2_UNAVAILABLE;
/* Use `Class` instead of `struct objc_class *` */
```
从上面两段代码可以得知：  
1-1、```Class``` 是 ```objc_class``` 结构体类型的指针；  
1-2、```objc_object``` 结构体只包含一个Class定义的 ```isa``` 变量，```isa``` 又是一个 ```objc_class``` 结构体类型；  
1-3、```id``` 是 ```objc_object``` 结构体类型的指针。  
2-1、```objc_class``` 结构体包含一个Class定义的``` isa``` 变量，同上。

<!-- more -->

总结一下 可以得出：  
1、```class``` 是 ```struct```  
2、```objc_class``` 和 ```objc_object``` 几乎一样。那么我们就可以这么认为： *```id```可以认为是 ```objc_class``` 的结构体指针*，*```class``` 也可以认为是 ```objc_object``` 的结构体指针*。最后总结 ***```class```也是对象***，那我们就能说，```object```是```object```，```class```也是```object```。

作为区分，我们分别称之为“实例对象(instance object)”、“类对象(class object)”。实例对象结构体中的isa指针指向所属的类对象，类对象结构体中的isa指针指向指向的也是其所属的类对象，它的名字叫做元类(metaclass)。根据文章[What is a meta-class in Objective-C?](http://www.cocoawithlove.com/2010/01/what-is-meta-class-in-objective-c.html)中的例子与解释，我们可以看到在调用runtime中的objc_allocateClassPair方法时，生成了一对```class```，分别是 ```class``` 和 ```metaclass```。  
3、```objc_class``` 中包含了 ```ivar``` ```method``` 的列表，所以我们可以理解为 ```class``` 中存储了实例变量 和 实例方法，```metaclass``` 中存储了类变量 和 类方法。  
4、```objc_class```中有一个```super_class```的变量，它则指向自己的父类，根类的super则指向NULL。

# metaclass
从上面可以看出，```metaclass```也是一个对象，它的isa指针指向的是什么呢？通过文章[What is a meta-class in Objective-C?](http://www.cocoawithlove.com/2010/01/what-is-meta-class-in-objective-c.html)中的例子，我们能了解到```metaclass```的isa指向的是它的根```metaclass```。根```metaclass```的isa则指向它自己。

# Conclusion
以上说的比较混乱，下面贴上一个流传甚广的一张解释图。

![](http://upload-images.jianshu.io/upload_images/2181684-c5a2771145784fed.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



以上
