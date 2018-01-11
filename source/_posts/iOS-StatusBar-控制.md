---
title: iOS StatusBar 控制
date: 2018-01-11 11:02:54
categories: 学习总结
---


# 本文只提供一种方法，总共三个步骤
*只讨论 iOS Version >= 7.0*

### 1、info.plist 设置
open as sources code

```
<key>UIViewControllerBasedStatusBarAppearance</key>
<true/>
```
或者

open as property list

```
View controller-based status bar appearance  YES
```

<!-- more -->

### 2、ViewController containers add Extension/SubClass
一般我们用UINavigationController或者UITabBarController来做Container，当存在 UINavigationController或者UITabBarController 时，系统只会调用Container的方法，而忽略ViewController 的方法。 所以我们需要为Container添加Extension，或者子类。

```
open override var childViewControllerForStatusBarStyle: UIViewController? {
    return self.topViewController
}
open override var childViewControllerForStatusBarHidden: UIViewController? {
    return self.topViewController
}
```

### 3、ViewControllers add setting method
三个分别设置 style hidden animation 的方法


```
override var preferredStatusBarStyle: UIStatusBarStyle {
    return .default // .lightContent
}

override var prefersStatusBarHidden: Bool {
    return true // false
}

override var preferredStatusBarUpdateAnimation: UIStatusBarAnimation {
    return .fade // .none .slide
}
```

### 4、Update statusBar when vc has appeared
当控制器已经出现的时候需要修改时，调用下面的方法即可。


```
func updateStatusBarStyle() {
    self.setNeedsStatusBarAppearanceUpdate()
}

override var preferredStatusBarStyle: UIStatusBarStyle {
     return self.statusBarStyle
}
```
