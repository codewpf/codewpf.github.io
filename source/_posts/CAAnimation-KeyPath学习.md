---
title: CAAnimation KeyPath学习
date: 2017-02-11 20:42:45
categories: iOS
tags: 
- Swift
---

| KeyPath | 描述 | 值 |
| :----- | :----- | :----- |
| transform.scale | 比例变化 | 0 ~ 1 |
| transform.scale.x | 宽比例变化 | 0 ~ 1 |
| transform.scale.y | 宽比例变化 | 0 ~ 1 |
| transform.rotation.x |  围绕X轴旋转 | 0 ~  2*M_PI |
| transform.rotation.y |  围绕Y轴旋转 | 0 ~  2*M_PI |
| transform.rotation.z |  围绕Z轴旋转 | 0 ~  2*M_PI |
| cornerRadius | 圆角变化 | 0 ~ 2*MAX(width,height) |
| backgroundColor | 颜色变化，透明度不变 |  ***AnyColor.cgColor***[^1] |
| opacity | 透明度变化 | 0 ~ 1 |
| bounds  | 大小变化，中心不变 | CGRect |
| position  | 中心变化  | CGPoint |
| position.x  | 中心X变化  | CGFloat |
| position.y  | 中心Y变化  | CGFloat |
| contents  | 内容变化 如ImageView.image |  ***image.cgImage***[^2]|
| borderWidth | 边框宽| 0 ~ |

<!-- more -->

示例代码如下
``` swift

        let testView: UIView = UIView(frame: CGRect(x: (Screen_Width()-self.View_Width())/2, y: 100, width: self.View_Width(), height: self.View_Width()))
        testView.backgroundColor = UIColor.green
        self.view.addSubview(testView)
        
        let iv: UIImageView = UIImageView(frame: CGRect(x: 20, y: 50, width: 150, height: 200))
        iv.image = UIImage(named: "1.jpeg")
        self.view.addSubview(iv)
        
        DispatchQueue.main.asyncAfter(deadline: DispatchTime.now() + 1) {
        
            print("begin")
            let bounds: CABasicAnimation = CABasicAnimation(keyPath: "bounds")
            bounds.fromValue = testView.frame
            bounds.toValue = CGRect(x: (Screen_Width()-self.View_Width())/2, y: Screen_Height() - 300, width: 50, height: 50)
            
            let position: CABasicAnimation = CABasicAnimation(keyPath: "position.y")
            position.fromValue = testView.center.y
            position.toValue = Screen_Height() - 150
            
            let rotation: CABasicAnimation = CABasicAnimation(keyPath: "transform.rotation.x")
            rotation.fromValue = 0
            rotation.toValue = M_PI * 2
            
            let cornerRadius: CABasicAnimation = CABasicAnimation(keyPath: "cornerRadius")
            cornerRadius.fromValue = 0
            cornerRadius.toValue = 25
            
            let bgColor: CABasicAnimation = CABasicAnimation(keyPath: "backgroundColor")
            bgColor.fromValue = UIColor.green.cgColor
            bgColor.toValue = UIColor(red: 0.3, green: 0.2, blue: 0.9, alpha: 0.1)
            
            let opacity: CABasicAnimation = CABasicAnimation(keyPath: "opacity")
            opacity.fromValue = 1.0
            opacity.toValue = 0.5
            
            let borderWidth: CABasicAnimation = CABasicAnimation(keyPath: "borderWidth")
            borderWidth.fromValue = 0
            borderWidth.toValue = 2
            
            let group1: CAAnimationGroup = CAAnimationGroup()
            group1.animations = [bounds, position, cornerRadius, bgColor, opacity, borderWidth]
            group1.fillMode = kCAFillModeForwards
            group1.isRemovedOnCompletion = false
            group1.duration = 2
            testView.layer.add(group1, forKey: "test")
            
            
            
            let contents: CABasicAnimation = CABasicAnimation(keyPath: "contents")
            contents.fromValue = iv.image?.cgImage
            contents.toValue = UIImage(named: "2.jpeg")?.cgImage
            
            let group2: CAAnimationGroup = CAAnimationGroup()
            group2.animations = [contents, borderWidth]
            group2.fillMode = kCAFillModeForwards
            group2.isRemovedOnCompletion = false
            group2.duration = 2
            iv.layer.add(group2, forKey: "iv")
            
        }

```

CAAnimation中 当isRemovedOnCompletion = false 时 fillMode = kCAFillModeForwards 才会生效

[官方参考](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/CoreAnimation_guide/AnimatableProperties/AnimatableProperties.html#//apple_ref/doc/uid/TP40004514-CH11-SW2)


[^1]: 添加在Layer上，所以要用cgColor
[^2]: 添加在Layer上，所以要用cgImage



