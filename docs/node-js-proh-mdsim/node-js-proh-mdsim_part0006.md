# 第2章：设置 Node.js 项目并探索 JavaScript 基础

在本章中，我们将继续进行 Node.js 之旅，通过设置 Node.js 项目并深入探讨 JavaScript 基础知识。到本章结束时，你将具备坚实的基础，可以开始构建自己的 Node.js 应用程序。

## 2.1 初始化 Node.js 项目

要启动一个新的 Node.js 项目，我们将使用一个名为 npm（Node 包管理器）的包管理工具，它与 Node.js 一起捆绑提供。按照以下步骤初始化一个新的 Node.js 项目：

### 2.1.1 创建项目目录

首先，为你的项目创建一个新目录。打开命令提示符或终端，导航到你希望创建项目目录的位置。使用以下命令创建一个新目录：

```js

mkdir my-node-project

```

该命令将在你当前的位置创建一个名为 "my-node-project" 的目录。

### 2.1.2 进入项目目录

接下来，使用以下命令进入项目目录：

```js

cd my-node-project

```

你现在已经进入 "my-node-project" 目录。

### 2.1.3 初始化项目

要初始化项目并创建一个 "package.json" 文件，该文件将存储项目特定的元数据和依赖项，请运行以下命令：

```js

npm init

```

系统将提示你提供有关项目的信息，例如项目名称、版本、描述、入口点等。你可以填写详细信息或按 Enter 键接受每个提示的默认值。

一旦你提供了必要的信息，npm 将在你的项目目录中生成 "package.json" 文件。

## 2.2 探索 JavaScript 基础

由于 Node.js 是基于 JavaScript 构建的，因此拥有扎实的 JavaScript 基础至关重要。在本节中，我们将介绍一些基本概念，帮助你入门。

### 2.2.1 变量和数据类型

在 JavaScript 中，你可以使用 "var"、"let" 或 "const" 关键字来声明变量。JavaScript 支持多种数据类型，包括数字、字符串、布尔值、对象、数组等。以下是一个例子：

```jsjavascript

let name = "John";

const age = 25;

let isStudent = true;

```

### 2.2.2 控制流和循环

JavaScript 提供了控制流语句，如 "if-else" 和 "switch"，用于根据条件做出决策。你还可以使用 "for" 和 "while" 等循环结构来重复执行代码块。以下是一个例子：

```jsjavascript

let score = 85;

if (score >= 90) {

console.log("Excellent!");

} else if (score >= 80) {

console.log("Good job!");

} else {

console.log("Keep practicing!");

}

for (let i = 0; i < 5; i++) {

console.log(i);

}

```

### 2.2.3 函数和模块

JavaScript 中的函数允许你封装可重用的代码块。你可以使用 "function" 关键字定义函数，并根据需要调用它们。此外，你可以通过将函数组织到单独的文件中并将其作为模块导出，来实现代码的模块化。以下是一个例子：

```jsjavascript

// math.js

function add(a, b) {

return a + b;

}

function subtract(a, b) {

return a - b;

}

module.exports = {

add,

subtract

};

// app.js

const math = require("./math.js");

console.log(math.add(5, 3));

console.log(math.subtract(10, 7));

```

## 2

.3 总结

在本章中，我们学习了如何使用 npm 设置一个新的 Node.js 项目并初始化一个 "package.json" 文件。我们还探讨了 JavaScript 的一些基本概念，如变量、数据类型、控制流、循环、函数和模块。

到目前为止，你应该对如何启动一个 Node.js 项目并掌握 JavaScript 基础有了扎实的理解。在下一章，我们将深入探讨 Node.js 模块和 Node 包管理器（NPM），这将拓展你构建 Node.js 应用的能力。
