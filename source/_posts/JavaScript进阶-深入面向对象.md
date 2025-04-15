---
title: JavaScript进阶-深入面向对象
tags: [JavaScript]
comments: true
date: 2025-04-15 20:10:13
categories: JavaScript进阶
---

本章我们将重点介绍JavaScript中的面向对象编程思想，其中有非常重要的原型相关知识，是面试以及实际应用中经常需要面对的问题。

<!-- more -->

## 什么是面向对象？
面向对象编程（OOP）是一种编程范式或编程模型，它使用“对象”来设计软件和程序。面向对象编程的主要思想是将数据和操作数据的方法封装在一起，形成“对象”，通过对象之间的交互来实现程序的功能。

面向对象编程的主要特点包括：
- 封装：将数据和操作数据的方法封装在一起，形成一个“对象”。
- 继承：允许一个对象继承另一个对象的属性和方法。
- 多态：允许一个对象以不同的方式响应不同的消息。
- 抽象：将复杂的现实世界问题抽象为简单的模型。

## 原型对象
JavaScript中，每一个构造函数都有一个`prototype`属性，这个属性指向一个对象，这个对象就是原型对象。原型对象中的属性和方法可以被所有通过该构造函数创建的实例对象共享。例如：
```javascript
function Star(name, age){
  this.name = name
  this.age = age
}
Star.prototype.sing = function(){
  console.log(`${this.name}唱歌`)
}
const star1 = new Star('刘德华', 40)
const star2 = new Star('张学友', 50)
console.log(star1.sing()) // 刘德华唱歌
console.log(star2.sing()) // 张学友唱歌
```
从上面的实例可以看到，原型对象可以挂载函数，对象实例化不会多次创建原型上的函数或属性，可节约内存。这样一来，对于某些所有实例对象共用的、不变的方法，可以直接定义在原型对象上。同时，原型对象上的方法中如果使用到`this`，`this`指向的是调用这个方法的实例对象。
ps：不推荐在原型对象上挂载函数时使用箭头函数的形式，因为箭头函数没有自己的`this`，可能会造成一系列预期之外的结果。

## constructor属性
在JavaScript中，每一个原型对象都有一个`constructor`属性，这个属性指向该原型对象的构造函数。例如：
```javascript
function Star(name, age){
  this.name = name
  this.age = age
}
console.log(Star.prototype.constructor === Star) // true
```
那么我们在什么时候会需要用到`constructor`属性呢？当我们需要添加多个方法到原型对象时，可以给原型对象赋值，但是这样会覆盖构造函数原型对象原来的内容，这样修改之后，原型对象的`constructor`就不再指向当前构造函数了，此时我们可以在修改后的原型对象中，添加一个`constructor`指向原来的构造函数：
```javascript
function Star(name, age){
  this.name = name
  this.age = age
}
Star.prototype = {
  constructor: Star,
  sing: function(){
    console.log(`${this.name}唱歌`)
  },
  dance: function(){
    console.log(`${this.name}跳舞`)
  }
}
const star1 = new Star('刘德华', 40)
const star2 = new Star('张学友', 50)
console.log(star1.sing()) // 刘德华唱歌
console.log(star2.sing()) // 张学友唱歌
console.log(star1.dance()) // 刘德华跳舞
```

## 对象原型
在JavaScript中，每个对象都有一个`__proto__`属性，这个属性指向该实例对象的构造函数的原型对象`prototype`，因为这个属性，每个实例对象都可以使用构造函数原型对象的属性和方法。例如：
```javascript
function Star(name, age){
  this.name = name
  this.age = age
}
Star.prototype.sing = function(){
  console.log(`${this.name}唱歌`)
}
const star1 = new Star('刘德华', 40)
console.log(star1.__proto__ === Star.prototype) // true
```

## 原型继承
首先我们通过一个例子来说明什么是继承。例如，我们有一个`Person`构造函数，它有一个`say`方法，还有一个`Student`构造函数，它继承自`Person`构造函数，并且有一个`study`方法。那么，`Student`构造函数就有了`say`方法，同时也有自己的`study`方法，这就是继承。
那么，如何实现继承呢？我们可以使用原型继承的方式来实现。具体的方法就是利用构造函数的原型对象`prototype`来服用父级构造函数的属性和方法。例如：
```javascript
function Person(){
  this.eyes = 2
  this.head = 1
}
function Student(){}
Student.prototype = new Person()
Student.prototype.constructor = Student // 修改原型对象后，原型对象的constructor属性会指向继承的父级构造函数，需要重新指向当前构造函数
```

## 原型链
基于原型对象的继承使得不同构造函数的原型对象关联在一起，并且这种关联的关系是一种链状的结构，这种链状结构关系称为原型链。
实际上，原型链可以看做是一种**查找规则**：当访问一个对象的属性/方法时，先查找对象自身有没有，如果没有就通过对象原型查找它的原型对象，如果还没有就依此类推继续往上查找，直到找到`Object`为止。

之前我们有提到过使用`typeof`是无法判断引用数据类型的具体类型的，在通过刚才的学习之后，我们就可以使用原型链来判断引用数据类型的具体类型了。在JavaScript中也提供了这样的一个方法`instanceof`：
```javascript
// instanceof 用于检测构造函数的 prototype 属性是否出现在某个实例对象的原型链上
function Car(make, model, year) {
  this.make = make;
  this.model = model;
  this.year = year;
}
const auto = new Car("Honda", "Accord", 1998);

console.log(auto instanceof Car);
// Expected output: true

console.log(auto instanceof Object);
// Expected output: true
```

## 总结
在本章中，我们学习了JavaScript的重要概念**原型**，它使得JavaScript中的对象可以共享属性和方法，从而节省内存。同时，我们也学习了如何使用原型链来实现继承，以及如何使用`instanceof`来判断引用数据类型的具体类型。这些知识对于理解JavaScript中的面向对象编程非常重要。
下一章内容中，我们将学习JavaScript中的一些常用高阶技巧，比如深浅拷贝、异常处理、this指向、性能优化等，各位读者老爷敬请期待！
