---
title: Swift interview questions 2
date: 2020-04-21 00:04:42
categories: Interviews
tags: 
- Swift
- Interview
---

## What is the difference between let and var
The difference is does a variable value can be changed after initiation or not. Obviously let can not altered.

## What are the differences between OC const and Swift let?
*let* has the same effet with *const* on a varable.

<!-- more -->

## What is Optional and which problem does optional solve?

Optional is an unwrapped variable type which has two conditions - nil and a value. It provides an option if we do not want assign a variable immediately.

And in some cases, you can't avoid getting optional values. For examples:

- convert a variable to another value type such Int(string)
- try catch error
- initialize an instance
- solve the strong reference cycle problem by weak


## How many ways to unwrap an optional value?

1. optional binding, safe
     - guard
     - let
     - while
     - as?
2. force unwrap, but not safe
3. != nil, but code consumption
3. nil coalescing operator *??*

## What are the difference between nil and .none?
- Nil just means nothing or none value
- .none is one of a value of an enum


## Explain how they differ between a static and a class member?
- static can be used in Class, Struct and Enum
- class can be overridden by a subClass
- the class modifier only can be used for methods and computed properties(kind of method)
