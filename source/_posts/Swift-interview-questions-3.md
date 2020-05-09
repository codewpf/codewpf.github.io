---
title: Swift interview questions 3
date: 2020-05-09 23:37:01
categories: Interviews
tags: 
- Swift
- Interview
---

## What are generics and which problem do they solve?

> Generic is a style of computer programming in which algorithms are written in terms of types to-be-specified-later that are then instantiated when needed for specific types provided as parameters - Wiki

Generics help developers to create a function or a type without assigning a specific value type which means they could be created once but used on different types, such as Array. 

```swift
@frozen public struct Array<Element>
```

<!-- more -->


### Generic function
```swift
func sum<Element>(_ a: Element, _ b: Element) {
    return a + b
}
```

### Generic type
```swift
struct Stack<Element> {
    var items = [Element]()
    mutating func push(_ item: Element) {
        items.append(item)
    }
    mutating func pop() -> Element {
        return items.removeLast()
    }
}
```

`Stack` is a generic type which means it have the ability, like Array, to create any value or reference type Stack 

### Generic type extension

```swift
extension Stack {
    var topItem: Element? {
        return items.isEmpty ? nil : items[items.count - 1]
    }
}
```

### Type constraint

Sometimes, it's useful to enforce certain type constraints on the types that can be used with generic functions and generic types. 

Syntax:

```swift
func someFunction<T: SomeClass, U: SomeProtocol>(someT: T, someU: U) {
    // function body goes here
}
```

> You can define your own type constraints when creating custom generic types, and these constraints provide much of the power of generic programming. Abstract concepts like Hashable characterize types in terms of their conceptual characteristics, rather than their concrete type. - [Swift Generics](https://docs.swift.org/swift-book/LanguageGuide/Generics.html)


### Associated Types
> When defining a protocol, it’s sometimes useful to declare one or more associated types as part of the protocol’s definition. An associated type gives a placeholder name to a type that is used as part of the protocol. The actual type to use for that associated type isn’t specified until the protocol is adopted. Associated types are specified with the associatedtype keyword - [Swift Generics](https://docs.swift.org/swift-book/LanguageGuide/Generics.html)

Example:

```swift
protocol Container { 
    associatedtype Item
    mutating func append(_ item: Item)
    var count: Int { get }
    subscript(i: Int) -> Item { get }
}
```

Associated Type also has the ability to adopt constraints, for example:

```swift
protocol Container { 
    associatedtype Item: Equatable
}
```

And more complex form is:

```swift
protocol SuffixableContainer: Container {
    associatedtype Suffix: SuffixableContainer where Suffix.Item == Item
    func suffix(_ size: Int) -> Suffix
}
```

As we can see from above, `Suffix` conform this protocol and the protocol super protocol has an associated type `Item`. 

### Generic Where Clauses
Where clauses is useful to define requirements for type constraints and associated types.

generic where clauses also can be used for an extension.

```swift
extension Stack where Element: Equatable {}
```

### Generic Subscripts
> Subscripts can be generic, and they can include generic where clauses - [Swift Generics](https://docs.swift.org/swift-book/LanguageGuide/Generics.html)


## What is the difference between a typealias and an associatedtype with a value in a protocol?

### typealias

Literally, `typealias` is an alias for an existing type. It can be useful in making your code more readable. However, it just a named alias of an existing type not a new type.

Usage:

* Reuse clousure
```swift
typealias Completion = () -> Void
```
* Conform to multiple protocols
```swift
typealias Codable = Decodable & Encodable
```

### associatedtype
As showd above, an associated type gives a placeholder name to a type that is used as part of the protocol. The actual type to use for that associated type isn’t specified until the protocol is adopted.

associatedtype can be override by a subclass or subprotocol, like:

```swift
protocol P { associatedtype A }
protocol P1: P {  // first example
    associatedtype A = Int
}  
protocol P2: P1 {
    associatedtype A = String
}
```

Reference:

* [associated type](https://forums.swift.org/t/typealias-overriding-associated-type-not-in-fact-better-expressed-as-same-type-constraint/11530/2)
* [typealias usage swift](https://www.avanderlee.com/swift/typealias-usage-swift/)
* [Swift Documents](https://docs.swift.org/swift-book/LanguageGuide/Generics.html)
