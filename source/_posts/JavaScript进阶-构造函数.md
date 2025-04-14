---
title: JavaScript进阶-构造函数
tags: [JavaScript]
comments: true
date: 2025-04-14 15:22:50
categories: JavaScript进阶
---

本章将会介绍JavaScript中的构造函数，包含构造函数的基础知识以及一些内置构造函数的常用方法。

<!-- more -->

## 深入对象

在介绍构造函数之前，我们来复习一下创建对象相关的知识。
### 创建对象的方式
在之前的基础篇的学习中，我们知道对象的可以通过`{}`的形式创建：
```javascript
const obj = {
  key: value,
}
```
当然，除了这种创建方式以外，还有另外一些创建对象的方式：
```javascript
// new Object() 创建对象
const obj = new Object()
// 可以通过obj.key = value的形式添加属性
obj.name = 'Tom'
obj.age = 18

// 构造函数创建
function Person(name, age) {
  this.name = name
  this.age = age
}
const person = new Person('Tom', 18)
console.log(person.name) // Tom
console.log(person.age) // 18
```

## 构造函数
在刚才的创建对象方式的介绍中，我们提到了构造函数创建对象，那么什么是构造函数呢？

构造函数是一种特殊的函数，用来初始化对象，需要注意的是：它的首字母必须大写；只能通过`new`关键字来调用构造函数，创建对象。

### 构造函数的执行过程
当使用`new`关键字调用构造函数时，会经历以下步骤：
1. 创建一个空对象
2. 将构造函数的`this`指向这个空对象，并执行构造函数的代码
3. 返回这个对象

### 内置构造函数
JavaScript中内置了一些构造函数，这些构造函数提供了一些统一的常用方法，下面将对常见构造函数进行介绍。

>引用类型
- `Object`：创建一个对象
  - `const keyArr = Object.keys(obj)`：获取obj中所有的键
  - `const valueArr = Object.values(obj)`：获取obj中所有的键值
  - `Object.assign(toObject, fromObj)`：将fromObj拷贝给toObj，也可由于向对象中添加新的键值对
- `Array`：创建一个数组
  - `forEach`：遍历数组，不返回数组，经常用于查找遍历数组元素
  - `filter`：过滤数组，返回新数组，返回的是筛选满足条件的数组元素
  - `map`：迭代数组，返回新数组，返回的是处理后的数组元素，
  - `reduce`：累计器，返回累计处理的结果，经常用于求和，`const result = arr.reduce((prev, current) => { // 函数体 }, initial)`，没有初始值则将第一个元素作为上一次值，当前值为第二个元素
  - `join`：数组元素拼接为字符串，返回字符串
    - `join(separator)`：指定一个字符串来分隔数组的每个元素；如果需要，将分隔符转换为字符串；如果省略，数组元素用逗号`,`分隔；如果 separator 是空字符串`""`，则所有元素之间都没有任何字符
  - `find`：查找元素，返回符合测试条件的第一个数组元素值，如果没有符合条件的就返回undefined
  - `every`：检测数组所有元素是否都符合指定条件，如果所有元素都通过检测则返回true，否则返回false
  - `some`：检测数组中的元素是否满足条件，如果有至少一个元素满足条件，则返回true，否则返回false
  - `concat`：合并两个数组，返回生成新数组
  - `sort`：对原数组单元值排序
  - `splice`：删除或替换原数组单元，`arr.splice(start, deleteCount, item1, item2, ..., itemN)`
    - `start >= arr.length`：添加所提供的元素
    - `deleteCount`：省略或大于start到数组末尾的长度，删除start之后的所有元素；0或负数，不会移除元素，应至少指定一个新元素
  - `reverse`：反转数组
  - `findIndex`：查找元素的索引值
  - `Array.from()`：数组静态方法，伪数组转换为真数组
- `RegExp`：创建一个正则表达式
- `Date`：创建一个日期对象

>基本包装类型
为什么叫基本包装类型呢？因为它们都是用来包装基本数据类型的，比如字符串、数字、布尔值等。这些包装类型的构造函数可以给基本数据类型提供一些通用的方法，方便我们对基本数据类型进行操作。
- `String`：创建一个字符串
  - `str.length`：获取字符串长度
  - `const arr = str.split('分隔符')`：将字符串拆分成数组
  - `const subStr = str.substring(start, end)`：截取字符串
  - `str.startsWith(targetStr, index)`：检测是否以某字符串开头
  - `str.includes(targetStr, index)`：判断一个字符串是否包含在另一个字符串中
  - `str.toUpperCase()`
  - `str.toLowerCase()`
  - `str.indexOf(targetChar)`
  - `str.endsWith(targetStr)`
  - `str.replace(pattern, replacement)`：返回一个新字符串，其中一个、多个或所有匹配的 pattern 被替换为 replacement，pattern 可以是字符串或 RegExp，如果 pattern 是字符串，则只会替换第一个匹配项；不改变原始字符串
  - `str.match(regexp)`：检索字符串与正则表达式进行匹配的结果
  - `str.trim()`：去除字符串左右两侧的空格，并返回一个新的字符串
- `Number`：创建一个数字
  - `toFixed(digitCount)`：设置保留小数位的长度
- `Boolean`：创建一个布尔值

## 总结
本章介绍了JavaScript中的构造函数，包括构造函数的基础知识以及一些内置构造函数的常用方法。具体的方法以及使用方式可以参考[MDN文档](https://developer.mozilla.org/zh-CN/)，笔者在这里只是列举了一些常用的方法，方便读者了解。在下一章中，我们将深入面向对象编程思想，介绍JavaScript中的面向对象编程。