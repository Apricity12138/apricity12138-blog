---
title: JavaScript基础-引用数据类型
tags: [JavaScript]
comments: true
date: 2025-04-09 22:44:07
categories: JavaScript基础
---

本章主要介绍JavaScript中的引用数据类型，包括对象、数组等。

<!-- more -->

## 数组
数组是存储一组数据的有序集合，数组中的每个数据称为元素，元素可以是任意类型的数据。数组使用方括号表示，元素之间使用逗号分隔。下面是数组的基本使用方法：
```javascript
// 定义一个数组
const arr = [1, 2, 3, 4, 5]
// 访问数组中的元素
console.log(arr[0]) // 1
console.log(arr[1]) // 2
// 修改数组中的元素
arr[0] = 10
console.log(arr[0]) // 10
// 向数组末尾添加一个元素
arr.push(6)
console.log(arr[5]) // 6
// 删除数组中的最后一个元素
arr.pop()
console.log(arr[4]) // 5
```
除了基本的增删改查的操作之外，数组还提供了一些常用的方法，如`concat()`、`join()`、`reverse()`、`slice()`、`splice()`、`sort()`、`toString()`、`valueOf()`等。具体的使用方法可以等待后续文章的讲解。

## 对象

对象是实际开发中最为常用的数据类型之一，它可以将多个**键值对**作为一个逻辑整体存储，在便于操作的同时还可以增加代码的可读性。下面是对象的基本使用方法：
```javascript
// 定义一个对象
const person = {
  name: '张三',
  age: 18,
  gender: '男',
  sayHello: function() {
    console.log('你好，我是' + this.name);
  }
}
// 访问对象的属性
console.log(person.name) // 张三
console.log(person['age']) // 18
person.sayHello() // 你好，我是张三
```
如上示例，对象中的元素是由一个个键值对构成的，键值对之间使用逗号分隔，键值对中的键和值之间使用冒号分隔。键值对中的键是对象的属性，值是属性的值。访问对象的属性有两种方式，一种是使用点运算符，另一种是使用方括号运算符。点运算符后面跟的是对象的属性名，方括号运算符后面跟的是对象的属性名对应的字符串。
如果需要对对象的属性进行增删改操作，可以使用以下方式：
```javascript
// 这里拿上面定义好的person对象继续举例
// 增加属性
person.hobby = ['篮球', '足球', '乒乓球']
// 删除属性
delete person.gender
// 修改属性
person.age = 20

console.log(person) // { name: '张三', age: 20, hobby: [ '篮球', '足球', '乒乓球' ] }
```

## 关于引用数据类型，你应该知道的细节
>存储在内存中的什么地方？
JavaScript中的数据类型分为两大类：基本数据类型和引用数据类型。基本数据类型存储在栈内存中；引用数据类型的真实数据存储在堆内存中，变量中保存的是指向堆内存的地址。
由于这个原因，引用数据类型在赋值时，传递的是地址，而不是值，所以会出现下面这种情况：
```javascript
const obj1 = { name: '张三' }
const obj2 = obj1
obj2.name = '李四'
console.log(obj1.name) // 李四
```
由于obj1和obj2指向的是同一片堆内存空间，所以修改obj2的name属性，obj1的name属性也会跟着改变。
同样的当引用数据类型作为函数参数传递时，在函数内部对传入参数的修改也会影响到函数外部的引用数据类型。
另外，引用数据类型进行比较是，比较的是地址，而不是值，所以会出现下面这种情况：
```javascript
const obj1 = { name: '张三' }
const obj2 = { name: '张三' }
console.log(obj1 === obj2) // false
```
由于obj1和obj2指向的是不同的堆内存空间，所以比较结果为false。

>如何判断数据类型？
在JavaScript中，想要判断数据的类型，可以通过`typeof`关键字实现，如：
```javascript
let num = 10
console.log(typeof num) // number
```
但是`typeof`关键字对于引用数据类型来说，只能判断出是对象，无法判断出具体的对象类型，如：
```javascript
let arr = [1, 2, 3]
console.log(typeof arr) // object
```
如上述情况表现的，`typeof`不能直接判断出`arr`是一个数组，因为在JavaScript中，数组也是对象的一种。所以，想要判断引用数据类型的具体类型，在后续我们学习完更深的知识之后，就可以使用`instanceof`关键字进行判断了，这里我们先卖个关子~~

## 结语
在本篇章中，我们学习了数组和对象这两个引用数据类型的基本使用方法，以及一些关于引用数据类型的细节。至此，JavaScript中的基础知识就学习完毕了，相信大家在阅读完前几篇章之后，对于JavaScript已经有了基本的认识。接下来，就跟着笔者一起，开始学习更深层次的JavaScript知识吧！
