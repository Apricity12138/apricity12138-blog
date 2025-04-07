---
title: JavaScript基础-引入方式、变量和数据类型
comments: true
date: 2025-04-07 10:35:11
tags: [JavaScript]
categories: JavaScript基础
---

本章节主要介绍了JavaScript的三种引入方式、变量的声明方式以及数据类型相关的知识。

<!-- more -->

## JavaScript引入方式

JavaScript主要有三种引用方式：
1. 内联式：在HTML标签中直接引入JavaScript代码，例如：
```html
<button onclick="alert('Hello World!')">点击我</button>
```
这里，`onclick`是一个html元素的事件属性，当按钮被点击时，会执行`alert('Hello World!')`这段代码，浏览器会弹出带有`Hello World!`信息的提示框。
2. 内嵌式：在HTML文件中创建一个`<script></script>`双标签，将JavaScript代码放在这个标签中，例如：
```html
<script>
    alert('Hello World!')
</script>
```
注意，通常我们会将JavaScript代码放在`<body>`标签的底部，这样做的原因是，html文件的解析顺序是由上至下的，将`<script>`标签放在`<body>`的底部可以确保在执行JavaScript代码时，HTML元素已经被加载完成。
3. 外部式：将JavaScript代码放在一个单独的文件中，然后在HTML文件中通过`<script>`标签的`src`属性引入这个文件，例如：
```html
<script src="script.js"></script>
```
同理，从外部引入的JavaScript文件通常也放在`<body>`标签的底部。

## JavaScript变量

JavaScript中的变量是用来存储数据的容器。

### 变量的声明
变量的声明方式主要有以下几种：
1. 使用`var`关键字声明变量，例如：
```javascript
var name = 'John'
```
这里，`var`是声明变量的关键字，`name`是变量的名称，`'John'`是变量的值。`var`声明的变量为全局作用域中的变量，可以在整个程序中的任意位置访问和修改。
**需要注意的是**，`var`关键字目前已经很少使用，各位初学的小伙伴目前可以仅作了解，实际使用时尽量使用后面两种声明方式。
2. 使用`let`关键字声明变量，例如：
```javascript
let age = 25
```
`let`关键字是ES6中引入的，与`var`关键字不同的是，`let`声明的变量只在当前作用域内有效。
3. 使用`const`关键字声明常量，例如：
```javascript
const PI = 3.14
```
`const`关键字声明的变量一旦被赋值，就不能再被修改。与`let`相同，`const`声明的变量也只在当前作用域内有效。

### 变量的命名规则
1. 变量名必须以字母、下划线或美元符号开头，后面可以跟任意数量的字母、数字、下划线或美元符号。
2. 变量名不能包含空格或特殊字符。
3. 变量名区分大小写。例如，`name`和`Name`是两个不同的变量。
4. 变量名不能是JavaScript中的保留字。例如，`var`、`let`、`const`等都是JavaScript中的保留字，不能用作变量名。

### 变量的作用域
变量的作用域是指变量在程序中的可访问范围。
根据变量的声明方式，变量的作用域可以分为以下几种：
1. 全局作用域：在全局作用域中声明的变量可以在整个程序中的任意位置访问和修改。例如：
```javascript
var globalVar = 'I am global'
function foo() {
    console.log(globalVar)
}
foo() // 输出：I am global
```
2. 局部作用域：在局部作用域中声明的变量只能在当前作用域内访问和修改。例如：
```javascript
function foo() {
  const localVar = 'I am local'
}
console.log(localVar) // 报错：localVar is not defined，因为localVar在foo函数的局部作用域中，无法在函数外部访问
```
局部作用域主要包括以下几种：
- 函数作用域：在函数内部声明的变量只能在当前函数内部访问和修改。
- 块级作用域：在ES6中引入的`let`和`const`关键字声明的变量只能在当前块级作用域内访问和修改，所有用`{}`包裹的代码块都称为块级作用域。


## JavaScript数据类型

JavaScript中的数据类型主要包括以下几种：
1. 基本数据类型：包括`number`、`string`、`boolean`、`undefined`和`null`。
2. 引用数据类型：包括`Object`、`Array`、`Function`等。

### 基本数据类型
1. `number`：表示数字类型，包括整数和浮点数。例如：
```javascript
let num1 = 10
let num2 = 3.14
```
2. `string`：表示字符串类型，使用单引号或双引号括起来。例如：
```javascript
let str1 = 'Hello'
let str2 = "World"
```
**模板字符串**：ES6中引入了模板字符串，使用反引号（``）括起来，可以在字符串中嵌入变量或表达式，例如：
```javascript
let name = 'John'
let age = 25
let message = `My name is ${name}, I am ${age} years old.` // 输出：My name is John, I am 25 years old.
```
3. `boolean`：表示布尔类型，只有两个值：`true`和`false`。例如：
```javascript
let isTrue = true
let isFalse = false
```
4. `undefined`：表示未定义类型，当一个变量被声明但未被赋值时，它的值就是`undefined`。例如：
```javascript
let x
console.log(x) // 输出：undefined
```
5. `null`：表示空类型，表示一个空对象或空值。例如：
```javascript
let obj = null
console.log(obj) // 输出：null
```

### 引用数据类型
1. `Object`：表示对象类型，可以用来存储键值对。例如：
```javascript
let person = {
    name: 'John',
    age: 25,
    gender: 'male'
}
```
2. `Array`：表示数组类型，可以用来存储一组有序的数据。例如：
```javascript
let fruits = ['apple', 'banana', 'orange']
```
3. `Function`：表示函数类型，可以用来定义和执行函数。例如：
```javascript
function sayHello(name) {
    console.log(`Hello, ${name}!`)
}
sayHello('John') // 输出：Hello, John!
```

关于引用数据类型，笔者会在后续的文章中详细介绍。

## 结语
本章节主要介绍了JavaScript的三种引入方式、变量的声明方式以及数据类型相关的知识。希望各位小伙伴能够掌握这些基础知识，为后续的学习打下坚实的基础。目前评论系统已经开启，欢迎各位读者老爷在评论区讨论文章相关内容哦~~当然也欢迎大家**Email笔者**，不管是哪种方式，笔者在看到的第一时间都会尽力解决大家的疑问🌹那么我们下期文章再见啦👋