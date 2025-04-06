---
title: JavaScript基础-JS初体验
date: 2025-04-06 11:32:14
tags: [JavaScript]
categories: JavaScript基础
comments: true
---

JavaScript 基础系列第二章，通过一个“猜数字”游戏的案例，带领初学者们体验 JavaScript 的魅力。
**PS：如果是有经验的开发者，可以直接跳过本章内容。**

<!-- more -->

## 引言

在本章中，我们将一起完成一个简单的“猜数字”网页小游戏，体验一下 JavaScript 开发的基本流程。如果对于本章中的代码有任何疑惑，不要紧，各位初学 JS 的小伙伴只需要按照笔者的代码，一步步抄下来即可，在学习完后续的内容之后，你将解开所有的疑惑。

## 准备工作

相信观看本学习笔记的读者老爷都已经有过 HTML 和 CSS 的学习经历，但笔者还是想在这里多啰嗦几句。

> 代码编辑器

首先，任何编程相关的工作都需要一个合适的代码编辑器。前端程序员常用的代码编辑器为 VS Code ，没有下载安装的读者老爷可以[点击](https://code.visualstudio.com/Download)跳转到官网进行下载，记得选择对应的操作系统哦~

下载完 VS Code 之后，各位读者老爷可以在扩展商店中搜索并安装自己喜欢的插件：
{% img /images/js初体验/扩展安装指引.jpg '"扩展商店位置" "扩展安装指引"' %}
笔者在这里推荐几个前端开发常用到的插件，可以大大提升开发体验和效率，更多的好用插件推荐会单独写一篇文章来详细讲讲。

1. **Chinese (Simplified) Language Pack for Visual Studio Code**：中文语言包，将 VS Code 的界面翻译成中文，方便初学者阅读。
   {% img /images/js初体验/Chinese.jpg '"中文语言包" "中文语言包"' %}
2. **Error Lens**：错误提示插件，将错误提示信息显示在代码行号旁边，方便快速定位错误。
   {% img /images/js初体验/ErrorLens.jpg '"错误提示插件" "错误提示插件"' %}
3. **Live Server**：实时预览插件，在开发过程中可以实时预览网页效果，保存代码即刷新页面，非常方便。
   {% img /images/js初体验/LiveServer.jpg '"实时预览插件" "实时预览插件"' %}

安装插件过后，可能会需要按照指引重启 VS Code ，重启之后插件才会生效。

> 编写代码

在准备好 VS Code 和相关插件后，我们可以正式进入代码编辑阶段，**请确保你的输入法处于英文状态，避免出现输入错误**。

- 在一个容易找到的位置新建一个文件夹，然后在 VS Code 中打开该文件夹。
- 在文件夹中新建一个名为 `index.html` 的文件，键入`!`选择代码提示的第一个然后回车，并补充一行代码：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <script src="./index.js"></script>
    <!-- 新增的行 -->
  </body>
</html>
```

- 在文件夹下新建一个名为 `index.js` 的文件，键入以下代码：

```js
console.log("Hello, JavaScript!");
```

- 回到`index.html`代码中，右键代码编辑区域，选择`Open with Live Server`。
- 在浏览器中右键选择检查或 F12 打开开发者工具，选择控制台，如果一切顺利，你应该看到如下内容：
  {% image /images/js初体验/控制台输出.jpg '"控制台输出" "控制台输出"' %}

## 编写游戏

在完成准备工作之后，我们终于可以开始实现我们的“猜数字”游戏了。游戏的具体规则如下：

- 随机生成一个 0~100 之间的整数，玩家需要在输入框中输入一个数字，并点击提交按钮；
- 如果提交的数字等于随机生成的数字，则提示“恭喜你，猜对了！”；
- 如果提交的数字小于随机生成的数字，则提示“猜小了！”；
- 如果提交的数字大于随机生成的数字，则提示“猜大了！”；
- 如果提交的数字不在 0\~100 之间，则提示“请输入 0\~100 之间的数字！”。

有一定基础的读者可以自行思考实现这样一个“猜数字”游戏的思路，笔者将在这里给出一个参考实现，各位读者老爷可以对照着代码进行体验，具体涉及的所有语法知识都将在后面的章节讲解。

> HTML 部分

```html index.html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <div class="container">
    <div class="rules">猜数字游戏：请输入一个0~100之间的整数</div>
    <form action="">
      <input type="text" id="number" />
      <button type="button">提交</button><br>
      <div id="result"></div>
    </form>
  </div>
    </form>
  </div>
  <script src="./index.js"></script>
</body>
</html>
```

> JavaScript 部分

```js index.js
// 设置答案
const answer = Math.floor(Math.random() * 100);
// 添加点击事件
const button = document.querySelector("button");
button.addEventListener("click", () => {
  // 点击提交时获取用户输入的数字
  const input = document.querySelector("#number");
  const guess = parseInt(input.value);
  // 判断用户输入的数字与答案的大小
  const result = document.querySelector("#result");
  if (guess === answer) {
    result.textContent = "恭喜你猜对了！";
    result.style = "color: green";
  } else if (guess < answer) {
    result.textContent = "猜小了！";
    result.style = "color: red";
  } else {
    result.textContent = "猜大了！";
    result.style = "color: red";
  }
});
```

在完成两部分代码后，回到`index.html`文件，用 Live Server 打开，并打开浏览器开发者工具，如果一切顺利，你应该可以看到如下效果：
{% image /images/js初体验/游戏界面.jpg '"游戏界面" "游戏界面"' %}

各位读者老爷可以根据参考代码自行体验小游戏，不知道各位有没有成功猜到答案呢~

## 结语

在本章中，我们通过一个“猜数字”游戏，体验了 JavaScript 开发的基本流程，各位读者老爷如果对代码有任何疑惑，可以继续阅读后续章节，相信大家在不断的学习过程中，一定可以解决现在的问题！如果对文章内容有任何疑问，可以在评论区留言，笔者会在看到的第一时间回复各位，也欢迎大家对笔者的写作内容提出建议（360° 螺旋鞠躬/）。

在接下来的章节中，我们将正式进入 JavaScript 语法的学习，敬请期待！
