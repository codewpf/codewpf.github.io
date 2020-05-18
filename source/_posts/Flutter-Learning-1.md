---
title: Flutter Learning 1
date: 2020-05-18 23:03:33
updated : 2020-05-19 11:20:00
categories: Flutter
tags: 
- Flutter
- Dart
---

## Dart study notes

 
* All types are `Object` includes `function`
* All types default value is `null`
* `??` syntax could prevent a null object to invoke its method or property
* `this` means Object self
* Every function has return value, default is `null`
* Every line should have a `;` 
* `var name = value` or `type name = value`  
* Variable: `var` and constant: `const / final`s 
* `final` means the var will set only once, and will be initialized when accessed first time. `const` is implict final but is a compile constant
* instance variable can be final but cannot be const ( Only static fields can be declared as const)
![](Flutter-Learning-1/fl1.png)
![](Flutter-Learning-1/fl2.png)
* Support type inferring
* if condition statements need round brackets
* Each case have to end by `break` otherwise the code will be execute fallthrouh
* Dart does not have `fallthrough` keyword, but support the feature
* Dart does not have `func` key word, and define the return type at first
<!-- more -->
* function support `=>` single line syntax `type funcName(type var) => funcBody;`
* Classs property has default `getter` and `setter`
* But if the property defined a specific keyword such as `get`, then it only support getter `int get value => 2;`
* Support `.?` but do not support `int?`
* Construct function and named construct function can not be inherited defalut by subclass. Subclass must override it itself. `ClassName.name(int value) : super( name){};`
* Construct function could a simple form `ClassName(this.value1, this.value2); `
* Construct function support init property by parameters but can not use `this` keyword. `ClassName(Map value) : name = value["name"], super(vale){};`
* Inherit by `extends` keyword
* Mixin by `with` keyword. `class ClassName extends ClassName1 with Class Name2 {} `
* Any class could be used as interface by `implements` keyword 
* `abstract` class is similar with `Protocol` in Swift.
* `async await` implement asynchronism 
* The return value type is `Future` when a function modified by `async`
* The return value type is `Stream ` when a function modified by `async*`
* `throw try on catch finally` is the keywords for exception, and finally statement must be execute.
* In `'` String, `\` could modify some special mark such as `"I'm a student"` and `'I\'m a student'`
* String could be connect by `+`
* String support `$var` to connect new string and also support `${var / statement}` connect any other type such `int`
* forloop support normal form but not `...` and `..<`
* function optional parameters form is `[ type name, type name ]`。 But is the form is `{type name, type name}`, optional parameters can be invoke in disorder form. 

```
    int plus({int a = 1, int b = 2 }) {
        return a + b;
    }
    plus(b: 4, a: 9);
    plus(a: 3, b: 12)l
    // either is fine.
```

* function optional parameters could be set default value `type name = ""`, but unoptional parameters do not have default value.
* `try catch` can access stack tree value，for instance `catch(e,s)`. e means exception and s means stac tree.
* Custom Exception `class myException implements Exception { String errorMessage(){ print message };}`
* _ + varname default is private property
* `~/` truncating division operator. If any of operator number is `Double`, then `a~/b` equal `(a/b).truncate().toInt()`
* class static/class property and function default is lazy
* Clousure coud access its super scope property
* list.forEach( item { print(item); } )


