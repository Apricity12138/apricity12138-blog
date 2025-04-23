---
title: JavaScript_WEB-基本认识和基础操作
tags: [JavaScript]
comments: true
date: 2025-04-23 14:50:06
categories: JavaScript_WEB
---

各位读者老爷好久不见，笔者最近在忙一些别的事情都没有更新，今天感觉不能这样自甘堕落，所以重拾键盘，来继续我们的JavaScript之旅。今天要给大家讲解的是浏览器端JavaScript的基本认识和基础操作。

<!-- more -->

## 基础认识
首先需要明确的是，JavaScript在一开始被创建出来就是作为浏览器的脚本语言使用的，后来经过不断地发展才有了今天的规模，不过说到底，JavaScript始终是服务于浏览器的脚本语言，所以与浏览器相关的api也是JavaScript的核心内容。

### DOM和BOM
DOM是文档对象模型，是浏览器提供给JavaScript操作HTML文档的接口，通过DOM，JavaScript可以获取到HTML文档中的元素，并对其进行操作。BOM是浏览器对象模型，是浏览器提供给JavaScript操作浏览器的接口，通过BOM，JavaScript可以获取到浏览器的信息，并对其进行操作。
### DOM对象
浏览器根据HTML标签生成的JS对象`document`，所有的标签属性都可以在这个对象上面找到，修改这个对象的属性会自动映射到标签上。

## 基本操作
### 获取DOM元素
获取DOM元素的方式有很多种，下面列举几种常用的方式：
1. 通过id获取：`document.getElementById('id')`
2. 通过class获取：`document.getElementsByClassName('class')`
3. 通过标签名获取：`document.getElementsByTagName('tag')`
4. 通过CSS选择器获取：`document.querySelector('CSSselector')`，`document.querySelectorAll('CSSselector')`
### 操作DOM元素
获取到DOM元素之后，就可以对其进行操作了，下面列举几种常用的操作方式：
- `.innerText`属性：元素的内部文本，纯文本不解析标签
- `.innerHTML`属性：会解析HTML标签
- 修改常见属性：`对象.属性 = 值`
- 操作元素样式属性：`对象.style.属性值 = '值'`，css属性中出现`-`的，用小驼峰命名，例如 background-color => backgroundColor
- 通过类名操作样式：`对象.className = '类名'`
- 通过classList操作类：`对象.classList.add('类名')`追加一个类，`对象.classList.remove('类名')`删除一个类，`对象.classList.toggle('类名')`切换一个类（有就删，无就加）
- 操作表单元素属性
  - `表单.value`：获取表单输入元素值
  - `表单.type`：获取表单输入类型
  - 表单的`disabled`、`checked`、`seelcted`等属性只能接收布尔值
- 自定义属性：`data-自定义属性`
  - 获取：`对象.dataset`获取元素上的所有自定义属性，`对象.dataset.自定义属性`可以拿到指定的自定义属性
### 操作DOM节点
DOM节点就是DOM中的每一个元素，分为以下几种：
- 元素节点：标签
- 属性节点：标签的属性
- 文本节点：标签中的文本内容
- 其他
需要操作DOM节点，可以通过以下的一些方法实现：
- 查找节点
  - `子元素.parentNode`：最近一级的父节点，找不到则为null
  - `父元素.childNodes`：获得所有子节点，包括文本节点、注释节点等
  - `父元素.children`：仅获得所有子元素节点，值为伪数组
  - `元素.nextElementSibling`：下一个兄弟节点
  - `元素.previousElementSibling`：上一个兄弟节点
- 增加节点
  - `document.createElement('标签名')`：创建元素节点
  - `父元素.appendChild(要插入的元素)`：插入到父元素的最后一个子元素
  - `父元素.insertBefore(要插入的元素, 在哪个元素前面)`
  - `元素.cloneNode(布尔值)`：克隆一个跟原标签一样的元素，括号内为true则会包含后代节点一起克隆
- 删除节点
  - `父元素.removeChild(要删除的元素)`：通过父节点删除

## 总结
本章节中，我们初步了解了一些JavaScript Web API的基础知识和操作，在下一章中，我们会学习Web API中比较重要的DOM事件操作。
