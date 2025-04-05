---
title: Javascript学习笔记
date: 2025-04-05 22:47:57
description: Javascript 基础知识
categories: 前端基础
tags: [Javascript]
---

这是我学习 Javascript 的笔记，记录了一些基础内容，包括了 JavaScript 基础、进阶、Web Api，以及 ES6 语法等内容。

<!-- more -->

# Javascript 基础

---

### Javascript 介绍

##### 定义

- 一种运行在客户端的编程语言，实现人机交互效果
- 作用
  - 网页特效
  - 表单验证
  - 数据交互
  - 服务端程序（node.js）
- 组成
  - ECMAScript：Javascript 语言基础
  - Web APIs
    - DOM：页面文档对象模型
    - BOM：浏览器对象模型

##### 书写位置

- 内部 Javascript：直接写在 HTML 文件里，用`<script>`标签包住
- 外部 Javascript：通过`src`属性引入
- 内联 Javascript：写在标签内部

##### 输入输出语法

- 输出
  - `document.write('要输出的内容')`：向 body 内输出内容，可以输出标签，会解析成网页元素
  - `alert('内容')`：页面弹出警示框
  - `console.log('调试内容')`：控制台输出
- 输入
  - `prompt('提示语')`：显示一个对话框，包含提示语和输入框，默认返回 string 类型

### 变量

##### 基本使用

- 声明变量：`let 标识符`

##### 命名规则

- 不能用关键字
- 只能由下划线、字母、数字、$组成，且数字不能开头
- 字母区分大小写

##### 数组

- Array：是一种可以按顺序保存数据的数据类型
  - 声明：`let 数组名 = [数据1, 数据2, ..., 数据N]`，`let 数组名 = new Array(数据1, 数据2, ..., 数据N)`
  - 操作
    - `arr.push(content)`：在数组尾部添加 content，返回数组长度
    - `arr.unshift(content)`：在数组头部添加 content，返回数组长度
    - `arr.pop()`：删除数组尾部元素，返回被删除的元素
    - `arr.shift()`：删除数组头部元素，返回被删除的元素
    - `arr.slice(start, end)`：返回一个新的数组对象，这一对象是一个由 `start` 和 `end` 决定的原数组的浅拷贝（包括 `start`，不包括 `end`），其中 `start` 和 `end` 代表了数组元素的索引。原始数组不会被改变。
    - `arr.splice(index, count)`：从 index 索引位置开始，删除 count 个元素（count 省略就删到最后）
    - `const newArr = arr.map((item, index) => { //函数体 })`：创建一个新数组，这个新数组由原数组中的每个元素都调用一次提供的函数后的返回值组成
    - `const newStr = arr.join('分隔符')`：将数组中的所有元素转换为一个字符串并返回
    - `arr.forEach((item, index) => { // 回调函数体 })`：对数组的每个元素执行一次给定的回调函数，只遍历不返回，也不会修改原数组
    - `const filteredArr = arr.filter((item) => { // 函数体 })`：创建给定数组一部分的浅拷贝，其包含通过所提供函数实现的测试的所有元素。

##### 常量

- 声明：`const 标识符`，不可改变，声明时必须初始化

### 数据类型

##### 基本数据类型

- `number`：数字型
- `string`：字符串型，`""`，`''`，或反引号模板字符串
  - 模板字符串：反引号包裹，`${标识符}`引用变量
- `boolean`：布尔型
- `undefined`：未定义型，只声明变量，不赋值时就是未定义型
- `null`：空类型，以赋值，内容为空
- 检测数据类型：`typeof 标识符`

##### 引用数据类型

- 变量中存储的是地址，new 创建，存放在堆，不主动释放由垃圾回收机制回收
- `Object`：对象
- `Array`：数组
- `Date`：日期

##### 数据类型转换

- 隐式转换：某些运算符被执行时，系统内部自动将数据类型进行转换
  - `+`两边只要有一个是字符串，都会把另一个转成字符串
  - 算术运算符（除了`+`）都会把 shu'ju 转换成数字类型
- 显式转换
  - `Number()`：转换为数字类型
  - `parseInt()`：只保留整数部分
  - `parseFloat()`：可保留小数部分
  - `Boolean()`：转换为布尔型

### 运算符

##### 赋值运算符

- 对变量进行赋值：`=`，`+=`，`-=`，`*=`，`/=`，`%=`

##### 一元运算符

- 自增：`++a`，`a++`
- 自减：`--a`，`a--`

##### 比较运算符

- `>`，`<`，`>=`，`<=`，`==`（值是否相等），`===`（类型和值是否相等），`!==`
- `NaN`不等于任何东西

##### 逻辑运算符

- `&&`，`||`，`！`

##### 运算符优先级

- `小括号` -> `一元运算符` -> `算术运算符` -> `关系运算符` -> `相等运算符` -> `逻辑运算符` -> `赋值运算符` -> `逗号运算符`

### 语句

##### 分支语句

```javascript
// if分支语句
if (条件) {
  // 执行代码
} else if (条件) {
  // 执行代码
} else {
  // 不符合所有情况的执行代码
}

// 三元运算符
条件 ? 为真执行的代码 : 为假执行的代码;

// switch语句
switch (情况选择器) {
  case 情况1:
    // 要执行的内容
    break;
  case 情况2:
    // 要执行的内容
    break;
  default:
  // 不符合所有情况的默认执行内容
}
```

##### 循环语句

```javascript
// while循环
while (循环条件) {
  // 循环体
}

// for循环
for (变量起始值; 终止条件; 变量变化量) {
  // 循环体
}

// for...of遍历可迭代对象
for (let tmp of arr) {
  // 利用tmp进行各种操作
}

// for...in遍历对象的可枚举属性
for (let key in object) {
  // key为键, object[key]为对应的值
}
```

- 循环退出
  - `continue`：结束本轮循环，进入下一次循环
  - `break`：结束循环

### 函数

##### 函数声明、调用、参数列表和返回值

```javascript
// 声明
function 函数名(形参列表 = 参数默认值) {
  // 函数体
  return 返回值;
}
// 调用，接收返回值
let returnContent = 函数名(实参列表);
```

##### 作用域

- 全局作用域，全局变量
- 局部作用域，局部变量

##### 匿名函数

- 函数表达式：将匿名函数赋值给一个变量，并且通过变量名称进行调用
  ```javascript
  let fun = function () {
    // 函数体
  };
  ```
- 立即执行函数：无需调用，立即执行

  ```javascript
  // 方式一
  (function (形参列表) {
    console.log("Hello,World");
  })(实参列表)(
    // 方式二
    function (形参列表) {
      console.log("Hello,World");
    }
  )(实参列表);
  ```

### 对象

##### 使用

- 声明语法
  ```javascript
  let object = {
    属性名: 属性值
    方法名: function () {
      // 方法体
    }
  }
  ```

##### 操作

- 查：`object.key`, `object['key']`
- 改：`object.key = newValue`
- 增：`object.newKey = newValue`
- 删：`delete object.key`
- 遍历：`for...in`

##### 内置对象

- Math
  - `Math.random`：生成 0-1 之间的随机数
  - `Math.ceil`：向上取整
  - `Math.floor`：向下取整
  - `Math.max`：取最大值
  - `Math.min`：取最小值
  - `Math.pow`：幂运算
  - `Math.abs`：绝对值

# Javascript 进阶

---

### 作用域&解构&箭头函数

##### 作用域

- 局部作用域
  - 函数作用域
  - 块作用域
- 全局作用域
- 作用域链：本质上是底层的变量查找机制
  - 在函数被执行时，会优先查找当前函数作用域中的变量
  - 如果当前作用域中没有，则逐级查找父级作用域直到全局作用域
- 垃圾回收机制
  - 内存的生命周期：分配 -> 使用 -> 回收
  - 全局变量一般不回收；局部变量不使用了就自动回收
  - 内存泄漏：程序中分配的内存未被释放或无法释放
  - 回收算法
    - 引用计数：看对象是否还有指向它的引用，没有了就回收对象
    - 标记清除：从根部（全局对象）出发定时扫描内存中的对象，凡是能从根部到达的对象，都是还要使用的， 无法由根部出发到达的对象被标记为不再使用，会被回收
    - JS 垃圾回收
      - 增量垃圾回收：将垃圾回收工作分为多个小步骤，分散在程序的执行过程中，避免长时间卡顿。
      - 分代回收：将对象分为**新生代**（Scavenge 算法：From 中存活的复制到 To，清除 From，翻转 From 和 To）和**老生代**（标记清除），新创建的对象被放置在新生代中，如果这些对象能够长期存活，则被移动到老生代。垃圾回收器会更加频繁地清理新生代中的对象，而老生代的对象因为生命周期较长，则不需要频繁清理。
- 闭包
  - 定义：一个函数对周围状态的引用捆绑在一起，内层函数中访问到其外层函数的作用域
  - 闭包=内层函数+外层函数的变量
  - 应用：实现数据的私有
  ```javascript
  function outer() {
    // 闭包
    const a = 0;
    function inner() {
      console.log(a);
    }
    return inner;
  }
  // 调用闭包
  const fun = outer(); // 全局作用域，从根开始可以达到局部作用域中的a，所以a不会被清除
  // 外部函数使用outer内部的变量
  fun();
  ```
- 变量提升（var）：把所有 var 声明的变量提升到当前作用域的最前面，只提升声明，不提升赋值

##### 函数进阶

- 函数提升：会把所有函数声明提升到当前作用域的最前面，只提升声明，不提升调用
- 函数参数
  - 动态参数：只存在于函数内部的伪数组`arguments`
  - 剩余参数：通过`...`接收多余形参列表数量的参数为一个真数组
  - 展开运算符`...`：可以进行数组的展开操作，`arr = [1, 2, 3]`，通过展开运算符可得到`...arr === 1, 2, 3`
- 箭头函数
  - 基本语法
  ```javascript
  // 1. 基本形式
  const fun1 = (形参列表) => {
    // 函数体
  };
  // 2. 只有一个参数时，省略小括号
  const fun2 = (x) => {
    // 函数体
  };
  // 3. 函数体只有一行时，可以省略大括号（不论是否是return都可以省略）
  const fun3 = (x) => console.log(x);
  const fun4 = (x) => x + 10;
  // 4. 箭头函数可以直接返回一个对象
  const fun5 = (id) => ({ id: id });
  ```
  - 参数：没有动态参数，有剩余参数
  - 关于`this`：箭头函数不会创建自己的 this，只会从自己的作用域链的上一层沿用 this

##### 解构赋值

- 数组解构：将数组的单元值快速批量赋值给一系列变量的简洁语法
  ```javascript
  const arr = [1, 2, 3];
  // 1. 常见情况
  const [a, b, c] = arr;
  // 2. 变量多单元值少
  const [a, b, c, d] = arr; // a:1  b:2  c:3  d:undefined
  // 3. 变量少单元值多
  const [a, b] = arr; // a:1  b:2
  // 4. 剩余参数解决变量少单元值多
  const [a, ...b] = arr; // a:1  b:[2, 3]
  // 5. 默认值防止undefined传递
  const [a = 0, b = 0] = [];
  // 6. 按需导入赋值
  const [a, , c] = arr; // a:1  c:3
  // 7. 多维数组解构
  const [a, b, [c, d]] = [1, 2, [3, 4]];
  ```
- 对象结构：将对象属性和方法快速批量赋值给一系列变量的简洁语法
  ```javascript
  const obj = {
    name: 'Tom',
    age: 18,
    sayHi: () => console.log(`${name} ${age}`)
  }
  // 1. 基本语法
  const {name, age, sayHi} = obj
  // 2. 解构时改名
  const {name: uname, age, sayHi} = obj
  // 3. 数组对象的解构
  const arrObj = [
    {
      uname: 'Tom',
      age: 18
    },
    {
      uname: 'John',
      age: 20
    }
  ]
  const [{uanme, age}, {uname: _uname, age: _age}] = arrObj
  // 4. 多级对象结构
  const multiObj = {
    uname: 'Tom'
    age: 18
    family: {
      mother: 'Lura'
      father: 'John'
    }
  }
  const {uname, age, family: {mother, father}} = multiObj
  ```

### 构造函数&数据常用函数

##### 深入对象

- 创建对象的方式
  - 对象字面量创建：`const obj = {key: value}`
  - `new Object()`创建
  - 构造函数
    - 命名以大写字母开头；只能由`new`操作符操作
    ```javascript
    function Person(name, age) {
      this.name = name;
      this.age = age;
    }
    const person = new Person("Tom", 18);
    ```
    - `new`的过程：创建新对象；this 指向新创建的空对象；向空对象中添加属性；返回新创建的对象
- 实例成员&静态成员
  - 实例成员：实例对象上的属性和方法
  - 静态成员：构造函数的属性和方法

##### 内置构造函数

- 引用类型
  - Object
    - `const keyArr = Object.keys(obj)`：获取 obj 中所有的键
    - `const valueArr = Object.values(obj)`：获取 obj 中所有的键值
    - `Object.assign(toObject, fromObj)`：将 fromObj 拷贝给 toObj，也可由于向对象中添加新的键值对
  - Array
    - `forEach`：遍历数组，不返回数组，经常用于查找遍历数组元素
    - `filter`：过滤数组，返回新数组，返回的是筛选满足条件的数组元素
    - `map`：迭代数组，返回新数组，返回的是处理后的数组元素，
    - `reduce`：累计器，返回累计处理的结果，经常用于求和，`const result = arr.reduce((prev, current) => { // 函数体 }, initial)`，没有初始值则将第一个元素作为上一次值，当前值为第二个元素
    - `join`：数组元素拼接为字符串，返回字符串
      - `join(separator)`：指定一个字符串来分隔数组的每个元素；如果需要，将分隔符转换为字符串；如果省略，数组元素用逗号`,`分隔；如果 separator 是空字符串`""`，则所有元素之间都没有任何字符
    - `find`：查找元素，返回符合测试条件的第一个数组元素值，如果没有符合条件的就返回 undefined
    - `every`：检测数组所有元素是否都符合指定条件，如果所有元素都通过检测则返回 true，否则返回 false
    - `some`：检测数组中的元素是否满足条件，如果有至少一个元素满足条件，则返回 true，否则返回 false
    - `concat`：合并两个数组，返回生成新数组
    - `sort`：对原数组单元值排序
    - `splice`：删除或替换原数组单元，`arr.splice(start, deleteCount, item1, item2, ..., itemN)`
      - `start >= arr.length`：添加所提供的元素
      - `deleteCount`：省略或大于 start 到数组末尾的长度，删除 start 之后的所有元素；0 或负数，不会移除元素，应至少指定一个新元素
    - `reverse`：反转数组
    - `findIndex`：查找元素的索引值
    - `Array.from()`：数组静态方法，伪数组转换为真数组
  - RegExp
  - Date
- 包装类型
  - String
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
  - Number
    - `toFixed(digitCount)`：设置保留小数位的长度
  - Boolean

### 深入面向对象

##### 编程思想

- 面向过程
- 面向对象

##### 原型

- 构造函数通过原型分配的函数是所有对象共享的；Javascript 规定，每一个构造函数都有一个 prototype 属性，指向另一个对象，称为原型对象；这个对象可以挂载函数，对象实例化不会多次创建原型上的函数，节约内存；对于不变的方法，可以直接定义在原型对象上，所有的对象实例就可以共享这些方法；构造函数和原型对象中的 this 都指向实例化的对象
  - 挂载新函数时不可以使用箭头函数的原因：箭头函数没有自己的 this，会导致一系列的问题
  ```javascript
  function Star(uname, age) {
    this.uname = uname;
    this.age = age;
  }
  Star.prototype.sing = function () {
    console.log("sing");
  };
  ```

##### constructor 属性

- 每个原型对象里都有一个 constructor 属性，该属性指向该原型对象的构造函数
- 应用场景：当需要添加多个方法到原型对象时，可以给原型对象赋值，但是这样会覆盖构造函数原型对象原来的内容，这样修改之后，原型对象的 constructor 就不再指向当前构造函数了，此时我们可以在修改后的原型对象中，添加一个 constructor 指向原来的构造函数
  ```javascript
  function Star(uname, age) {
    this.uname = uname;
    this.age = age;
  }
  Star.prototype = {
    constructor: Star,
    say: function () {
      console.log("hello " + this.uname);
    },
    sing: function () {
      console.log("lalala");
    },
  };
  ```

##### 对象原型

- 每个对象都有一个属性`__proto__`，这个属性指向构造函数的 prototype 原型对象，因此，每一个实例对象都可以使用构造函数原型对象的属性和方法

##### 原型继承

- 通过构造函数把公共的部分提取为父级，子级通过给原型对象赋值为父级构造函数创造的实例化对象完成继承
  ```javascript
  function Person() {
    this.eyes = 2;
    this.head = 1;
  }
  function Woman() {}
  Woman.prototype = new Person();
  Woman.prototype.constructor = Woman;
  ```

##### 原型链

- 基于原型对象的继承使得不同构造函数的原型对象关联在一起，并且这种关联的关系是一种链状的结构，这种链状结构关系称为原型链
- 原型链实际上是一种**查找规则**：当访问一个对象的属性/方法时，先查找对象自身有没有，如果没有就通过对象原型查找它的原型对象，如果还没有就依此类推继续往上查找，直到 Object 为止
- `instanceof`：用于检测构造函数的 prototype 属性是否出现在某个实例对象的原型链上

  ```javascript
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

### 高阶技巧

##### 深浅拷贝（只针对引用类型）

- 浅拷贝：只拷贝地址，即基本类型的属性/元素拷贝值，引用类型的属性/元素拷贝地址
  - 拷贝对象：`Object.assign()`/展开运算符
  - 拷贝数组：`Array.prototype.concat()`/展开运算符
- 深拷贝：拷贝的是对象

  - 递归实现

  ```javascript
  const person = {
    uname: "张三",
    age: 18,
    hobby: ["唱", "跳", "rap", "篮球"],
    info: {
      tel: "13888888888",
      address: "北京市昌平区",
    },
  };

  function deepCopy(newObj, oldObj) {
    for (let key in oldObj) {
      if (oldObj[key] instanceof Array) {
        newObj[key] = [];
        deepCopy(newObj[key], oldObj[key]);
      } else if (oldObj[key] instanceof Object) {
        newObj[key] = {};
        deepCopy(newObj[key], oldObj[key]);
      } else {
        newObj[key] = oldObj[key];
      }
    }
  }

  const newPerson = {};
  deepCopy(newPerson, person);

  newPerson.hobby.push("music");
  newPerson.info.tel = "13999999999";
  console.log(person);
  console.log(newPerson);
  ```

  - lodash 的 cloneDeep 方法：引入 lodash 库，`_.cloneDeep(obj)`
  - `JSON.stringify()`实现：`const newObj = JSON.parse(JSON.stringify(obj))`

##### 异常处理

- `throw`抛异常：`throw new Error('错误信息')`
- `try`/`catch`捕获异常：`try`中书写可能出现错误的代码；`catch`捕获对应`try`块中发生的异常并处理；`finally`是无论是否发生异常、`catch`有没有返回，都会执行的代码
- `debugger`关键字：相当于断点

##### 处理 this

- this 指向
  - 普通函数 this 指向：谁调用 this 就指向谁
  - 箭头函数 this 指向：函数内没有 this，沿用上一级的 this
- 改变 this 指向
  - `fun.call(thisArg, arg1, arg2, ..., argN)`：使用 call 方法调用函数，同时`thisArg`指定 this 指向
  - `fun.apply(thisArg, [argsArr])`：使用 apply 方法调用函数，`thisArg`指定 this 指向，参数传递必须以数组形式传递
    - 应用场景：求数组最大值`Math.max.apply(Math, arr)`
  - `fun.bind(thisArg, arg1, arg2, ...)`：不会调用函数，能改变函数内 this 指向，返回由指定的 this 值和初始化参数改造的原函数拷贝
    - 使用场景：只想改变 this 指向，不想调用函数时

##### 性能优化

- 防抖：单位时间内，频繁触发事件，只执行最后一次
  - 使用场景：搜索框输入；手机号、邮箱输入验证
  - `lodash`实现：`_.debounce(func, 毫秒)`
  - 手写实现：利用定时器`setTimeout`，声明一个定时器变量，每当事件触发都先判断是否有定时器，如果有就清除以前的定时器，如果没有就开启定时器存入变量，在定时器里调用要执行的函数
  ```javascript
  function debounce(func, time) {
    // 通过闭包访问debounce的作用域，使得关键变量 timer 持久化，且闭包环境独立，保证每次debounce之间的timer不会互相干扰
    let timer;
    return function () {
      if (timer) clearTimeout(timer);
      timer = setTimeout(function () {
        func();
      }, time);
    };
  }
  ```
- 节流：单位时间内频繁触发事件，只执行一次
  - 使用场景：鼠标移动`mousemove`，页面尺寸缩放`resize`，滚动条滚动`scroll`
  - `lodash`实现：`_.throttle(func, 毫秒)`
  - 手写实现：利用定时器实现，声明一个定时器变量，每当事件触发都先判断是否有定时器，如果有则不开启新定时器，如果没有定时器则开启定时器并存入变量（定时器里调用执行的函数，定时器结束时要清空定时器）
  ```javascript
  function throttle(func, time) {
    let timer = null;
    return function () {
      if (!timer) {
        timer = setTimeout(function () {
          func();
          timer = null; // 定时器运作期间无法通过clearTimeout清除定时器
        }, time);
      }
    };
  }
  ```

# Web APIs

---

##### Web API 基本认识

- 变量尽量用`const`声明
- 作用和分类
  - 使用 JS 去操作 HTML 和浏览器
  - 分类：DOM（文档对象模型）、BOM（浏览器对象模型）
- 什么是 DOM
  - 文档对象模型，是用来呈现以及与任意 HTML 或 XML 文档交互的 API
- DOM 树
  - 将 HTML 文档以梳妆结构直观的表现出来
  - 作用：直观体现了标签与标签之间的关系
- DOM 对象
  - 浏览器根据 HTML 标签生成的 JS 对象，所有的标签属性都可以再这个对象上面找到，修改这个对象的属性会自动映射到标签身上
  - DOM 核心思想：把网页内容当作对象来处理
  - `document`对象：DOM 提供的一个对象，他的属性和方法都是用来访问何操作网页内容的，网页的所有内容都在`document`里面

##### 获取 DOM 对象

- 根据 CSS 选择器来获取 DOM 元素
  - `document.querySelector('CSS选择器')`：返回匹配的第一个元素的对象
  - `document.querySelectorAll('CSS选择器')`：返回匹配的所有的元素的对象的 NodeList 伪数组（有长度有索引号，没有数组方法）
  - 不常用方法：`document.getElementById()`, `document.getElementsByTagName()`, `document.getElementsByClassName()`

##### 操作元素内容

- `.innerText`属性：元素的内部文本，纯文本不解析标签
- `.innerHTML`属性：会解析 HTML 标签

##### 操作元素属性

- 修改常见属性：`对象.属性 = 值`
- 操作元素样式属性：`对象.style.属性值 = '值'`，css 属性中出现`-`的，用小驼峰命名，例如 background-color => backgroundColor
- 通过类名操作样式：`对象.className = '类名'`
- 通过 classList 操作类：`对象.classList.add('类名')`追加一个类，`对象.classList.remove('类名')`删除一个类，`对象.classList.toggle('类名')`切换一个类（有就删，无就加）
- 操作表单元素属性
  - `表单.value`：获取表单输入元素值
  - `表单.type`：获取表单输入类型
  - 表单的`disabled`、`checked`、`seelcted`等属性只能接收布尔值
- 自定义属性：`data-自定义属性`
  - 获取：`对象.dataset`获取元素上的所有自定义属性，`对象.dataset.自定义属性`可以拿到指定的自定义属性

##### 定时器-间歇函数

- 开启定时器：`setInterval(函数名, 间隔时间ms)`，返回定时器的 id 号
- 关闭定时器：`clearInterval(id)`

##### DOM 事件基础

- 事件监听：`元素对象.addEventListener('事件类型', 要执行的函数)`
  - 三要素
    - 事件源：被事件触发的 DOM 元素
    - 事件类型：触发事件的方式
    - 时间调用的函数：触发事件后要做的事情
- 事件类型
  - 鼠标事件
    - `click`：点击
    - `mouseenter`：鼠标进入
    - `mouseleave`：鼠标离开
  - 焦点事件
    - `focus`：获得焦点
    - `blur`：失去焦点
  - 键盘事件
    - `keydown`：按键按下
    - `keyup`：按键抬起
  - 文本事件
    - `input`
- 事件对象：包含事件触发时的相关信息的对象
  - 事件绑定的回调函数的第一个参数就是事件对象
  - 常用属性
    - `type`：获取当前的事件类型
    - `clientX`/`clientY`：获取光标相对于浏览器可见窗口左上角的位置
    - `offsetX`/`offsetY`：获取光标相对于当前 DOM 元素左上角的位置
    - `key`：用户按下键盘的值
- 环境对象：函数内部的特殊变量 this，代表当前函数运行时所处的环境
- 回调函数：当一个函数作为参数传递给另一个函数时，这个作为参数的函数就被称为回调函数

##### DOM 事件进阶

- 事件流：事件完整执行过程中的流动路径
  - 捕获阶段：父元素到子元素，从根元素开始执行对应的事件
    - `DOM.addEventListener(事件类型, 事件处理函数, 是否使用捕获机制)`
  - 冒泡阶段：子元素到父元素，当一个元素触发事件后，会依次向上调用所有父级元素的同名事件
    - `事件对象.stopPropagation()`阻断事件流动传播
  - 事件解绑：`DOM.removeEventListener('事件类型', 函数名)`
- 事件委托：利用事件流的特征解决开发需求的技巧
  - `事件对象.target.tagName`可以获得真正触发事件的元素
- 阻止元素默认行为：`事件对象.preventDefault()`
- 其他事件
  - 页面加载事件
    - `window.addEventListener('load', function (){})`，页面加载外部资源完毕时触发的事件
    - `document.addEventListener('DOMContentLoaded', function (){})`，初始 HTML 文档被完全加载和解析完成之后触发的事件
  - 元素滚动事件
    - `window.addEventListener('scroll', function (){})`，监听整个页面滚动，可以通过`document.documentElement`获取到页面 HTML 元素，从而得到页面具体滚动了多少像素
    - `scrollTop`属性：滚动条向下滚动时，上部被卷去的大小，可读写
    - `scrollLeft`属性：滚动条向右滚动时，左边被卷去的大小，可读写
  - 页面尺寸事件
    - `window.addEventListener('resize', function (){})`
    - 获取元素可见部分宽高：`clientWidth`、`clientHeight`，不包含边框、margin、滚动条等
    - 获取元素自身宽高：`offsetWidth`、`offsetHeight`，包含边框、margin、滚动条
    - 获取元素距离自己带有定位的父级元素的左、上距离：`offsetLeft`、`offsetTop`，只读

##### DOM 节点操作

- 日期对象
  - 实例化：`const date = new Date()`
  - 方法
    - `getFullYear()`：获取年份
    - `getMonth()`：获取月份，取值 0~11
    - `getDate()`：获'dd'
    - `getDay()`：获取星期，取值 0~6
    - `getHours()`：获取小时
    - `getMinutes()`：获取分钟
    - `getSeconds()`：获取秒
    - `toLocaleString()`：'YYYY/MM/DD HH:mm:ss'
    - `toLocaleDateString()`：'YYYY/MM/DD'
    - `toLocaleTimeString()`：'HH:mm:ss'
  - 时间戳：指 1970 年 01 月 01 日 00 时 00 分 00 秒起至现在的**毫秒数**
    - 获取时间戳：`getTime()`, `+new Date()`, `Date.now()`
- DOM 节点：DOM 树中的每一个元素
  - 类型
    - 元素节点：所有的标签；根节点为 html
    - 属性节点：所有的属性
    - 文本节点：所有的文本
    - 其他
  - 查找节点
    - `子元素.parentNode`：最近一级的父节点，找不到则为 null
    - `父元素.childNodes`：获得所有子节点，包括文本节点、注释节点等
    - `父元素.children`：仅获得所有子元素节点，值为伪数组
    - `元素.nextElementSibling`：下一个兄弟节点
    - `元素.previousElementSibling`：上一个兄弟节点
  - 增加节点
    - `document.createElement('标签名')`：创建元素节点
    - `父元素.appendChild(要插入的元素)`：插入到父元素的最后一个子元素
    - `父元素.insertBefore(要插入的元素, 在哪个元素前面)`
    - `元素.cloneNode(布尔值)`：克隆一个跟原标签一样的元素，括号内为 true 则会包含后代节点一起克隆
  - 删除节点
    - `父元素.removeChild(要删除的元素)`：通过父节点删除
- M 端事件
  - 触屏事件
    - `touchstart`：手指触摸到一个 DOM 元素时触发
    - `touchmove`：手指在一个 DOM 元素上滑动时触发
    - `touchend`：手指从一个 DOM 元素上移开时触发
- swiper 插件：包含了移动端常用的触摸滑动插件
  - 官网：https://www.swiper.com.cn/
  - 在线演示文档：https://www.swiper.com.cn/demo/index.html
  - 基本使用流程：https://www.swiper.com.cn/usage/index.html
  - API 文档：https://www.swiper.com.cn/api/index.html

##### BOM 操作浏览器

- BOM：浏览器对象模型
  - window 对象是一个全局对象，也可以说是 JS 中的顶级对象，`document`、`alert()`、`console.log()`这些都是 window 的属性和方法，基本 BOM 的属性和方法都是 window 的
  - 所有通过 var 定义在全局作用域中的变量、函数都会变成 window 对象的属性和方法
  - window 对象下的属性和方法调用的时候可以省略 window
- 定时器-延时函数
  - 开启定时器：`setTimeout(回调函数, 等待的毫秒数)`
  - 清除定时器：`clearTimeout(定时器id)`
- JS 执行机制
  - JS 是单线程语言
  - HTML5 提出 Web Worker 标准，允许 JS 脚本创建多个线程，导致 JS 中有了同步和异步
    - 同步任务：都在主线程上执行，形成执行栈
    - 异步任务：JS 的异步通过回调函数实现，包括普通事件（click，resize）、资源加载（load，error）、定时器等，异步任务完成之后会添加到任务队列中
  - 执行机制：先执行执行栈中的同步任务，执行完毕后读取任务队列中的异步任务，如果有就拉到执行栈中执行，然后再进入任务队列读取异步任务重复前面的过程，形成**事件循环**
- `location`对象：拆分并保存了 URL 地址的各个组成部分
  - `href`：获取完整 URL 地址，常用于页面跳转
  - `search`：获取地址中携带的参数（URL 中`?`开始后面的部分）
  - `hash`：用于获取 URL 中`#`开始后面的部分
  - `reload(布尔值)`：刷新当前页面，传入 true 时表示强制刷新
- `navigator`对象：记录了浏览器自身相关信息
  - `userAgent`：用于检测浏览器的版本以及平台
- `history`对象：管理历史记录
  - `back()`：后退
  - `forward()`：前进
  - `go(参数)`：参数为 1 则前进一个页面，参数为-1 则后退一个页面
- 本地存储：HTML5 规范提出的新解决方案，允许将数据存放在用户浏览器中
  - `localStorage`：将数据永久性存储在本地（用户浏览器），除非手动删除；可以在同域的多窗口之间共享；以键值对的形式存储使用
    - 存储数据：`localStorage.setItem('key', value)`，value 存到本地存储后会自动转为字符串
    - 获取数据：`localStorage.getItem('key')`
    - 删除数据：`localStorage.removeItem('key')`
  - `sessionStorage`：生命周期为关闭浏览器窗口；在同一个页面下数据可以共享；以键值对形式存储
    - 操作与`localStorage`相同
  - 处理复杂数据类型：将复杂数据类型转为 JSON 字符串后再存储在本地存储中
    - `localStorage.setItem('obj', JSON.stringify(obj))`，存入操作
    - `JSON.parse(localStorage.getItem('obj'))`，取出操作

##### 正则表达式

- 用于匹配字符串中字符组合的模式，在 JS 中也属于对象，通常用来查找、替换符合正则表达式的文本
  - 使用场景：验证表单、过滤敏感词、截取特定字符串
- 语法
  - 定义：`const reg = /表达式/`，其中`//`是正则表达式字面量
  - 判断：`reg.test(被检测的字符串)`用于查看正则表达式与指定的字符串是否匹配，如果匹配成功返回 true，否则返回 false
  - 检索：`reg.exec(被检测的字符串)`用于在指定字符串中进行搜索匹配，如果匹配成功返回数组，否则返回 null
- 元字符
  - 边界符：用来提示字符所处的位置
    - `^文`：匹配行首的文本
    - `文$`：匹配行尾的文本
  - 量词：设定某个模式出现的次数
    - `*`：重复零次或更多次
    - `+`：重复一次或更多次
    - `?`：重复零次或一次
    - `{n}`：重复 n 次
    - `{n,}`：重复 n 次或更多次
    - `{n,m}`：重复 n 次到 m 次
  - 字符类
    - `[]`：匹配字符集合，加上`-`连字符表示范围（`[a-z]`表示 26 个小写字母，`[a-zA-Z]`表示大小写均可，`[0-9]`）
    - `[^]`：匹配除了字符集合以外的字符
    - `.`：匹配除了换行符以外的单个字符
    - 预定义：指的是某些常见模式的简写方式
      - `\d`->`[0-9]`
      - `\D`->`[^0-9]`
      - `\w`->`[a-zA-Z0-9_]`
      - `\W`->`[^a-zA-Z0-9_]`
      - `\s`->`[ \t\r\n\v\f]`
      - `\S`->`[^ \t\r\n\v\f]`
  - 修饰符：约束正则执行的某些细节行为，如是否区分大小写、是否支持多行匹配等
    - `/表达式/修饰符`
      - `i`：ignore，正则匹配不区分大小写
      - `g`：global，匹配所有满足正则表达式的结果
    - 替换：`字符串.replace(/正则表达式/, '替换的文本')`

# ES6 补充内容

---

##### 类

```javascript
class Person {
  //若在类中没有显式声明属性, 但在构造函数或方法中引用了未声明的属性, 会自动将其视为实例属性
  name;
  #web; //私有属性是指仅在类内部可访问和操作的属性, 外部无法直接访问和修改

  //构造函数 用于初始化属性
  constructor(name, gender) {
    this.name = name;
    this.#gender = gender;
  }

  //使用存取器 getter 获取私有属性
  get gender() {
    return this.#gender;
  }

  //使用存取器 setter 设置私有属性
  set gender(value) {
    this.#gender = value;
  }

  info() {
    return `姓名:${this.name} 性别:${this.gender}`;
  }
}

//子类继承
class David extends Person {
  web;

  constructor(name, gender, web) {
    super(name, gender); //调用父类构造函数

    this.web = web;
  }

  eat() {
    return `${this.name} 正在吃饭...`;
  }
}
```

##### 模块化开发

- 按需导出

  - 允许一个模块导出多个值（变量、函数、类等），每个值都有一个名称。
  - 导入时需要明确指定导出的名称，并使用解构语法。

  ```javascript
  // module.js
  // 先定义，再统一导出
  const name = "Alice";
  function greet() {
    console.log("Hello!");
  }
  class Person {}

  export { name, greet, Person };

  // index.js
  import { name as fullName, greet, Person } from "./module.js"; // 支持重命名
  ```

- 默认导出

  - 一个模块只能有一个默认导出，通常用于导出模块的主要功能或值。
  - 导入时可以自定义名称，不需要解构。

  ```javascript
  // module.js
  // 默认导出一个值
  const name = "Alice";
  export default name;

  // index.js
  import myName from "./module.js";
  ```

##### Promise

```javascript
/*
  Promise 表示承诺在未来的某个时刻可能会完成并返回结果

  对于某些需要时间来处理结果的操作, 如用户登录、读取文件等, 可以使用 Promise 对象来执行异步操作
  Promise 对象有三种状态 pending(待处理)、fulfilled(已履行)、rejected(被驳回)

  当创建一个 Promise 对象时, 它的初始状态为 pending, 表示异步执行还未完成
  当异步执行成功时, 会调用 resolve 函数把 Promise 对象的状态改变为 fulfilled, 可通过 then 方法来获取异步操作的结果
  当异步执行异常时, 会调用 reject 函数把 Promise 对象的状态更改为 rejected, 可通过 catch 方法来处理错误

  注
    异步操作是指在程序执行过程中, 某个操作不会立即返回结果, 而是需要一段时间的等待
*/

/*
  let promise = new Promise((resolve, reject) => {
      
  })

  //当创建一个 Promise 对象时, 它的初始状态为 pending, 表示异步执行还未完成
  console.log("promise:", promise) //pending
*/

/*
  let promise = new Promise((resolve, reject) => {
      resolve("邮件发送成功") //异步执行成功
  })
  //当异步执行成功时, 会调用 resolve 函数把 Promise 对象的状态改变为 fulfilled, 可通过 then 方法来获取异步操作的结果
  console.log("promise:", promise) //fulfilled

  promise.then(result => {
      console.log("result:", result)
  })
*/

/*
  let promise = new Promise((resolve, reject) => {
      reject("邮件发送失败") //异步执行失败
  })
  //当异步执行失败时, 会调用 reject 函数把 Promise 对象的状态更改为 rejected, 可通过 catch 方法来处理错误
  console.log("promise:", promise) //rejected

  promise.catch(error => {
      console.log("error:", error)
  })
*/

let promise = new Promise((resolve, reject) => {
  //resolve("邮件发送成功")
  reject("邮件发送失败");
})
  .then((result) => {
    console.log("result:", result);
  })
  .catch((error) => {
    console.log("error:", error);
  })
  .finally(() => {
    console.log("异步执行结束");
  });
```

##### Fetch

```javascript
/*
  fetch 是基于 Promise 的 api, 它可以发送http请求并接收服务器返回的响应数据
  fetch 返回的是一个 Promise 对象
*/

//get请求
fetch("http://127.0.0.1/get")
  .then((response) => {
    //返回的解析后的json数据会传递给下一个 then() 方法中的回调函数作为参数,这个参数就是 data
    return response.json(); //response.json() 用于将响应数据解析为json格式的数据
  })
  .then((data) => {
    //data 解析后的json数据
    console.log("get.data:", data);
  })
  .catch((error) => {
    console.log("get.error:", error.message);
  })
  .finally(() => {
    console.log("get.finally");
  });

//post请求 post
fetch("http://127.0.0.1/post", {
  method: "POST",
  headers: {
    "Content-Type": "application/x-www-form-urlencoded",
  },
  body: new URLSearchParams({
    //URLSearchParams 用于处理键值对类型的数据,并将其编码为url查询字符串
    name: "邓瑞",
    web: "dengruicode.com",
  }),
})
  .then((response) => {
    return response.json();
  })
  .then((data) => {
    console.log("post.data:", data);
  })
  .catch((error) => {
    console.log("post.error:", error.message);
  })
  .finally(() => {
    console.log("post.finally");
  });

//post请求 postJson
fetch("http://127.0.0.1/postJson", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    //JSON.stringify 用于将对象转换为json字符串
    name: "邓瑞编程",
    web: "www.dengruicode.com",
  }),
})
  .then((response) => {
    return response.json();
  })
  .then((data) => {
    console.log("postJson.data:", data);
  })
  .catch((error) => {
    console.log("postJson.error:", error.message);
  })
  .finally(() => {
    console.log("postJson.finally");
  });
```

##### Axios

```javascript
/*
  Axios 是基于 Promise 的网络请求库, 它可以发送http请求并接收服务器返回的响应数据
  Axios 返回的是一个 Promise 对象

  Axios 不仅可以用于浏览器, 也可以用于 Node.js, 而 Fetch 主要用于浏览器
*/

//get请求
axios
  .get("http://127.0.0.1/get")
  .then((response) => {
    console.log("get.data:", response.data);
  })
  .catch((error) => {
    console.log("get.error:", error);
  })
  .finally(() => {
    console.log("get.finally");
  });

//post请求 post
let data = {
  //参数
  name: "邓瑞",
  web: "dengruicode.com",
};

axios
  .post("http://127.0.0.1/post", data, {
    headers: {
      "Content-Type": "application/x-www-form-urlencoded",
    },
  })
  .then((response) => {
    console.log("post.data:", response.data);
  })
  .catch((error) => {
    console.log("post.error:", error);
  })
  .finally(() => {
    console.log("post.finally");
  });

//post请求 postJson [axios 的默认请求头是 application/json]
axios
  .post("http://127.0.0.1/postJson", data)
  .then((response) => {
    console.log("postJson.data:", response.data);
  })
  .catch((error) => {
    console.log("postJson.error:", error);
  })
  .finally(() => {
    console.log("postJson.finally");
  });
```

##### async、await 使用同步的方式编写异步代码

```javascript
//async/await 使用同步的方式编写异步代码, 避免回调地狱
//优势 在处理多个异步操作的情况下, 可以使代码更简洁易读
const getData = async () => {
  try {
    //get请求
    const response = await axios.get("http://127.0.0.1/get");
    console.log("async.get.data:", response.data);
    if (response.data.data.web === "dengruicode.com") {
      //get请求2
      const response2 = await axios.get("http://127.0.0.1/article/get/id/1");
      console.log("async.get2.data:", response2.data);
      if (response2.data.data.name === "邓瑞") {
        //get请求3
        const response3 = await axios.get(
          "http://127.0.0.1/article/get/search/title/入门"
        );
        console.log("async.get3.data:", response3.data);
      }
    }
  } catch (error) {
    console.log("async.get.error:", error);
  } finally {
    console.log("async.get.finally");
  }
};

getData();
```
