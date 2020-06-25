---
title: Flutter Learning 2
date: 2020-06-26 08:11:22
categories: Flutter
tags: 
- Flutter
- Dart
---

## Dart study notes - Chinese

   * 1 保存在变量里的都是对象，有对应类
   * 2 支持泛型 
   * 3 有 `dynamic` 类型 - 动态类型
   * 4 支持 函数 嵌套 函数
   * 5 权限控制，没有public private 添加 _ 前缀的变量默认为 private, 函数加 _ 变成私有函数
   * 6 在生产环境代码中 `assert()` 函数会被忽略，不会被调用。
   * 7 const 类似 swift let, 编译时常量；类常量 static const
   * 8 final 类似 swift const，只能修改一次。可以先定义，再之后实例化或者其他函数中赋值, 12中有例子
   * 9 try, on Exception name,  catch(e), finally
   * 10 const constructor 常量构造函数，得到的对象是相同的 - 单例？
   * 11 所有实例变量都生成隐式 getter 方法。
   <!-- more -->
   * 12 构造函数
   	* 默认构造函数没有参数并会调用父类的无参构造函数。
   	* 子类不会继承父类的构造函数。
   	* 使用命名构造函数可为一个类实现多个构造函数，例如 `Person.fromJson(String str)`
   	* 继承 `class Employee extends Person`
   	* 子类的构造函数调用了父类的命名构造函数，会先执行父类命名构造函数的内容 ↓ 例如
   	* `Employee.fromJson(Map data) : super.fromJson(data)` ↓可以继续拓展，x=,y= 可以和 super并存，但无法访问this
   	* `Employee.fromJson(Map data) : x = data['x'], y = data['y'], super.fromJson(data)` 
   	* `Point.withAssert(this.x, this.y) : assert(x >= 0)` 开发期间可以验证输入的初始化列表 
   	*    `class Point { 
   	        final num x;
   	        final num y;
   	        Point(x, y): x = x, y = y;
   	      }`
   	* 重定向构造函数 `Point.alongXAxis(num x) : this(x, 0);`  `this(x, 0)` 指的是 `Point(this.x, this.y);`
   	* 常量构造函数 类似 swift 类函数的构造函数，所以调用之后得到的是同一个对象
   	* 工厂构造函数 有待学习 ！https://www.dartcn.com/guides/language/language-tour#%E6%96%B9%E6%B3%95 往上翻
   * 13 assert 生产环境不执行
   * 14 geter setter
   * `num get right => left + width;
          set right(num value) => left = value - width; `
     类似 swift get{} set {newvalue}
   * 15 abstract 抽象类 中的抽象方法 类似 swift protocol, 但是没有 extension 中的默认实现
   * 16 抽象方法 只 存在于抽象类
   * 17 implements 专门实现多继承
   * 18 extends 单继承
   * 19 @override 在函数上一行添加实现 重写方法
   * 20 可以重写 noSuchMethod 方法处理 不存在的方法或实例变量，相当于主动 catch
   * 21 enum 相当于非swift的枚举，没有任何特性
   * 22 static 实现静态变量和静态方法
   * 23 通过 extends 限制 泛型类型，类似 swift 泛型的 : 和 where
   * 24 库可以，重命名；也可以只导入一部分
   	* `import 'package:lib2/lib2.dart' as lib2;`
   	* `import 'package:lib1/lib1.dart' show foo;` 只导入 foo
   	* `import 'package:lib2/lib2.dart' hide foo;` 除了 foo 都导入
   * 25 deferred as 可以用来延迟加载库
   * 26 异步 - Future 对象
   	* 使用 async 和 await 关键字实现异步编程
   	* Future functionName() async { ... await ... } 要使用 await ，代码必须在使用 async 标记的异步函数中
   	* 在一个异步函数中可以多次使用 await
   * 27 stream 类似 rxswfit
   * 28 `typedef Compare = int Function(Object a, Object b);`
   	* 目前，typedefs 只能使用在函数类型上， 我们希望将来这种情况有所改变。
   	* 使用泛型 `typedef Compare<T> = int Function(T a, T b); `
   * 29 使用 @todo 注解的示例： `@Todo('seth', 'make this do something')` 放在函数的上一行
   * 30 注释与 swift 完全相同