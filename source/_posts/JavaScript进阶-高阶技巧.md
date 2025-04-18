---
title: JavaScript进阶-高阶技巧
tags: [JavaScript]
comments: true
date: 2025-04-18 11:25:11
categories: JavaScript进阶
---

本章为JavaScript进阶篇的最后一章，我们会总结一些JavaScript中的常见技巧，这些技巧可以帮助我们写出更加简洁、优雅的代码。

<!-- more -->

## 深浅拷贝（引用类型）

为什么在小标题中说引用类型，因为基本类型不存在深浅拷贝的问题，他们在栈中就存储真实数据，而引用类型在栈中存储地址，在堆中存储真实数据，所以才有深浅拷贝的区分。

>浅拷贝
浅拷贝指的是只复制地址，没有产生新的对象，所以修改新对象会影响到原对象。

浅拷贝的实现方式有很多，比如：
```javascript
// 1. Object.assign
const obj1 = { a: 1, b: { c: 2 } };
const obj2 = Object.assign({}, obj1);
obj2.b.c = 3;
console.log(obj1.b.c); // 3
// 2. 展开运算符
const obj1 = { a: 1, b: { c: 2 } };
const obj2 = { ...obj1 };
obj2.b.c = 3;
console.log(obj1.b.c); // 3
```
在这里笔者不一一列举浅拷贝的实现方式，感兴趣的读者可以自行查阅资料。
>深拷贝
深拷贝指的是复制对象，产生新的对象，修改新对象不会影响到原对象。

深拷贝的实现方式也有很多，比如：
- `lodash`包的`cloneDeep`方法
- `JSON.stringify()`方法实现：`const newObj = JSON.parse(JSON.stringify(obj))`，但是这样会遇到循环引用问题。
- 递归实现：这里需要结合我们在原型章节中学到的`instanceof`方法来判断是否为对象，然后递归调用，具体实现如下：
```javascript
const person = {
  uname: '张三',
  age: 18,
  hobby: ['唱', '跳', 'rap', '篮球'],
  info: {
    tel: '13888888888',
    address: '北京市昌平区'
  }
}

function deepCopy(newObj, oldObj) {
  for (let key in oldObj) {
    if (oldObj[key] instanceof Array) {
      newObj[key] = []
      deepCopy(newObj[key], oldObj[key])
    } else if (oldObj[key] instanceof Object) {
      newObj[key] = {}
      deepCopy(newObj[key], oldObj[key])
    } else {
      newObj[key] = oldObj[key]
    }
  }
}

const newPerson = {}
deepCopy(newPerson, person)

newPerson.hobby.push('music')
newPerson.info.tel = '13999999999'
console.log(person)
console.log(newPerson)
```

## 异常处理

这个比较简单，如果有其他编程语言基础的读者一定不会陌生：
- `throw`抛异常：`throw new Error('错误信息')`。
- `try`/`catch`捕获异常：`try`中书写可能出现错误的代码；`catch`捕获对应`try`块中发生的异常并处理；`finally`是无论是否发生异常、`catch`有没有返回，都会执行的代码。
- `debugger`关键字：这是JavaScript中一个特殊的调试关键字，当代码执行到这个关键字时，会自动暂停，并进入调试模式，方便我们查看代码执行情况。

## 处理this
我们先来复习一下`this`的指向问题：
- 普通函数this指向：谁调用this就指向谁。
- 箭头函数this指向：函数内没有this，沿用上一级的this。
那么我们如果想要指定`this`的指向呢？`Function.prototype`上提供了三个方法可以指定`this`的指向：
- `fun.call(thisArg, arg1, arg2, ..., argN)`：使用call方法调用函数，同时`thisArg`指定this指向。
- `fun.apply(thisArg, [argsArr])`：使用apply方法调用函数，`thisArg`指定this指向，参数传递必须以数组形式传递。
  - 应用场景：求数组最大值`Math.max.apply(Math, arr)`。
- `fun.bind(thisArg, arg1, arg2, ...)`：不会调用函数，能改变函数内this指向，返回由指定的this值和初始化参数改造的原函数拷贝。
  - 使用场景：只想改变this指向，不想调用函数时。

## 性能优化
在实际开发场景中，我们需要非常注重性能问题，良好的性能可以提升用户的体验，下面将介绍实际开发过程中常见的两种性能优化手段：
- 防抖：单位时间内，频繁触发事件，只执行最后一次。
  - 使用场景：搜索框输入；手机号、邮箱输入验证。
  - `lodash`实现：`_.debounce(func, 毫秒)`。
  - 手写实现：利用定时器`setTimeout`，声明一个定时器变量，每当事件触发都先判断是否有定时器，如果有就清除以前的定时器，如果没有就开启定时器存入变量，在定时器里调用要执行的函数。
```javascript
function debounce(func, time){
  // 通过闭包访问debounce的作用域，使得关键变量 timer 持久化，且闭包环境独立，保证每次debounce之间的timer不会互相干扰 
  let timer
  return function () {
    if(timer) clearTimeout(timer)
    timer = setTimeout(function () {
      func()
    }, time)
  }
}
```
- 节流：单位时间内频繁触发事件，只执行一次
  - 使用场景：鼠标移动`mousemove`，页面尺寸缩放`resize`，滚动条滚动`scroll`。
  - `lodash`实现：`_.throttle(func, 毫秒)`。
  - 手写实现：利用定时器实现，声明一个定时器变量，每当事件触发都先判断是否有定时器，如果有则不开启新定时器，如果没有定时器则开启定时器并存入变量（定时器里调用执行的函数，定时器结束时要清空定时器）。
```javascript
function throttle(func, time){
  let timer = null
  return function () {
    if(!timer){
      timer = setTimeout(function (){
        func()
        timer = null  // 定时器运作期间无法通过clearTimeout清除定时器
      }, time)
    }
  }
}
```

## 总结
本章我们总结了JavaScript中的一些常见技巧，这些技巧可以帮助我们写出更加简洁、优雅的代码。至此，JavaScript进阶篇就结束了，希望读者能够有所收获。后续我们将继续学习Web API的相关操作。
