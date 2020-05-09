---
title: Swift interview questions 1
date: 2020-04-20 14:39:00
categories: Interviews
tags: 
- Swift
- Interview
---

## 1 What are value type and reference type, and its differences? How to choose?

Basicly, value type usually defined as Enum, Struct, Tuple and Base value type(Int, Float, Array, String, Dictionary). One the other hand, reference type defined as Class and Clousure(Block).

> The most basic distinguishing feature of a *value type* is that copying — the effect of assignment, initialization, and argument passing — creates an *independent instance* with its own unique copy of its data.
>
> Copying a reference, on the other hand, implicitly creates a shared instance. After a copy, two variables then refer to a single instance of the data, so modifying data in the second variable also affects the original,

<!-- more -->

### Summary
The benefits of the value type is you could always get a unique and copied instance immediately and you do not need to worry about its value will be alter in multiple tasks.

However, values and references act exactly the same way when instances have no writable data.

Value type

- get individual data 
- deep copy
- When you want to change the property of a value type object, you should create a *var* variable/object. Otherwise you can not update its property value even if the property type is “var”, because “let” make the whole object to be immutable.

Reference type

- share data with a same memory address 
- shallow copy
- *Class* can be inherited by a subcalss.

### How to choose
Use a value type when:

- Comparing instance data with == makes sense
- You want copies to have independent state
- The data will be used in code across multiple threads

Use a reference type (e.g. use a class) when:

- Comparing instance identity with === makes sense
- You want to create shared, mutable state

### Extension

#### mutating
Value type method must have *mutating* prefix

```swift
struct Test {
    var value: Int = 0
    mutating func change(_ value: Int) {
        self.value = value
    }
}
```

#### nonmutating
Usyally, nonmutating always work together with set in a computed property

```swift
struct Test {
    var value: Int {
        get { return 2 }
        nonmutating set {
            /// do something with out altering self value such as:
            print(newValue)
        }
    }
}
let t = Test()
t.value = 3
```


### References

[https://developer.apple.com/swift/blog/?id=10]()



