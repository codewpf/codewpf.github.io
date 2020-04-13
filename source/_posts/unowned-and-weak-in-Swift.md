---
title: unowned and weak in Swift
date: 2020-04-14 00:08:22
categories: 知识收集
tags: Swift
---

The differece between **weak** and **unowned** is does the block have an async function which will be re-invoke in future.

<!-- more -->

Here is the sample colde:

```swift
typealias IntBlock = (_ int: Int) -> ()
class AAA {
    var value: Int = 0
    let bbb: BBB
    init() {
        bbb = BBB()
        bbb.block = {/* below */ v in
            self.value = v
        }
    }
}
class BBB {
    var block:IntBlock?
    init() {
        self.weakfunc()
        self.unownedfunc()
    }
    func weakfunc() { // here! [weak self]
        DispatchQueue.main.asyncAfter(deadline: .now() + 2) {
            if let block = self.block { block(1) }
        }
    }
    func unownedfunc() { // here! [unownd self]
        if let block = self.block { block(2) }
    }
}
```

This is a simple way to understand which one is better for your code.

For more infomation:

*[Unowned 还是 Weak？生命周期和性能对比](https://swift.gg/2017/05/16/unowned-or-weak-lifetime-and-performance/)

*[How Swift Implements Unowned and Weak References](https://mjtsai.com/blog/2015/11/24/how-swift-implements-unowned-and-weak-references/)


