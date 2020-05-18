---
title: Method boundingRectWithSize get wrong height
date: 2020-04-17 01:07:07
categories: iOS
tags: 
- Swift
---

The calculation for the height of a label in Swift is different with OC. 
Here are some reasons may lead a wrong result of the method boundingRectWithSize.

```swift
open func boundingRect(with size: CGSize, options: NSStringDrawingOptions = [], attributes: [NSAttributedString.Key : Any]? = nil, context: NSStringDrawingContext?) -> CGRect

```

1. let options: NSStringDrawingOptions = [.usesLineFragmentOrigin, .usesFontLeading]

   Set the options paramater to a multiple value

2. Get the final value by the method of  *ceilf* in Swfit

3. Replace the \n and \t. Or add an extra height such as Height + [\n, \t].count * lineHeight


<!-- more -->


Below are two extensions for String and UILabel respectively

```swift
extension String {
    func height(with size: CGSize, font: UIFont) -> CGFloat {
        let nsstring = NSString(string: self)
        let options: NSStringDrawingOptions = [.usesLineFragmentOrigin,.usesFontLeading]
        return CGFloat(ceilf(Float(nsstring.boundingRect(with: size, options: options, attributes: [.font: font], context: nil).size.height)))
    }
}

extension UILabel {
    func textHeight(with width: CGFloat) -> CGFloat {
        if let txt = self.text {
            return txt.height(with: CGSize(width: width, height: CGFloat(MAXFLOAT)), font: self.font)
        } else {
            return 0
        }
    }
}
```

