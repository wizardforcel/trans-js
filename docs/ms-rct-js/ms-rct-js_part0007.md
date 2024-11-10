# # 第三章：创建你的第一个 React 组件

现在你的 React 开发环境已经搭建完毕，接下来是深入 React 的核心：创建组件。在本章中，我们将引导你从零开始构建你的第一个 React 组件。我们将涵盖你需要了解的一切，从理解 React 组件的结构到在你的应用中渲染它。到本章结束时，你将牢牢掌握 React 组件的工作原理，并准备好开始构建动态用户界面。

## 理解 React 组件的结构

在开始创建 React 组件之前，让我们拆解一下构成组件的基本要素。从本质上讲，React 组件是一个返回 JSX（JavaScript XML）代码的 JavaScript 函数或类。JSX 是一种语法扩展，它允许你在 JavaScript 文件中编写类似 HTML 的代码。

### 函数组件

函数组件是最简单的 React 组件类型。它们是 JavaScript 函数，接受一组可选的输入，称为“props”（属性的缩写），并返回一个 React 元素。以下是一个函数组件的基本结构：

```jsjsx

function MyComponent(props) {

return (

// JSX code goes here

);

}

```

在这个例子中，`MyComponent` 是一个函数组件，它可以接受 `props` 作为输入，并返回表示组件 UI 的 JSX 代码。函数组件非常适合用于简单的 UI 元素，是初学者的理想起点。

### 类组件

类组件是另一种 React 组件，它提供了更多高级功能和能力。它们是扩展了 `React.Component` 类的 JavaScript 类。类组件有自己的状态，并可以定义生命周期方法来处理组件事件。以下是一个类组件的基本结构：

```jsjsx

class MyComponent extends React.Component {

constructor(props) {

super(props);

this.state = {

// Initialize component state here

};

}

render() {

return (

// JSX code goes here

);

}

}

```

在这个例子中，`MyComponent`是一个类组件，可以使用`this.state`管理其状态，并定义一个`render`方法来返回 JSX 代码，用于渲染组件的 UI。类组件适用于更复杂的 UI 元素，并提供对组件行为的更大控制。

## 创建你的第一个函数式组件

让我们从创建你的第一个 React 组件开始：一个名为`HelloWorld`的函数式组件。这个组件将显示一条简单的"Hello, React!"消息。按照以下步骤创建并渲染你的组件。

### 第1步：创建一个新的组件文件

在你的 React 项目文件夹中，进入`src`目录。在这个目录下，创建一个名为`HelloWorld.js`的新文件。这个文件将包含你的`HelloWorld`组件。

### 第2步：定义函数式组件

打开`HelloWorld.js`文件，在文本编辑器或 IDE 中按如下方式定义`HelloWorld`函数式组件：

```jsjsx

import React from 'react';

function HelloWorld() {

return <h1>Hello, React!</h1>;

}

export default HelloWorld;

```

在这段代码中：

- 我们导入了`React`库，这是创建 React 组件所必需的。

- 我们定义了`HelloWorld`函数式组件，它返回一个包含`<h1>`标题的 JSX 元素，标题内容为"Hello, React!"。

- 最后，我们导出`HelloWorld`组件，使其可以在应用程序的其他部分中使用。

### 第3步：渲染组件

现在你已经定义了`HelloWorld`组件，是时候在应用程序中渲染它了。打开`src/App.js`文件，这是你创建的 React 应用项目中的主要组件。

在`src/App.js`文件中，导入`HelloWorld`组件，放在文件的顶部：

```jsjsx

import HelloWorld from './HelloWorld';

```

现在，你可以在`App`组件的`render`方法中使用`HelloWorld`组件。将`App`组件`render`方法中的现有 JSX 代码替换为以下内容：

```jsjsx

function App() {

return (

<div className="App">

<HelloWorld />

</div>

);

}

```

下面是这段代码中发生的事情：

- 我们导入了之前创建的`HelloWorld`组件。

- 在`App`组件的`render`方法中，我们包含了`HelloWorld`组件，从而在`App`组件的 UI 中渲染它。

### 步骤 4：查看你的组件

保存你对 `src/App.js` 文件所做的更改。如果开发服务器未运行，请在项目目录中的终端运行以下命令启动它：

```jsshell

npm start

```

该命令将启动开发服务器，并在 Web 浏览器中打开你的 React 应用。你应该在网页上看到 "Hello, React!" 消息。

恭喜！你已经创建并成功渲染了第一个 React 组件。你迈出了构建动态用户界面的第一步。

## 使用 Props

Props（即属性）是 React 中的一个基础概念，它允许你将数据从父组件传递到子组件。Props 使你能够通过根据外部数据自定义组件的行为和外观，来使组件变得动态。

### 将 Props 传递给组件

让我们通过传递一个 prop 来增强我们的 `HelloWorld` 组件。我们将创建一个名为 `Greet` 的新函数组件，接受一个用于问候的 `name` prop。按照以下步骤将 props 传递给组件：

### 步骤 1：创建一个新的组件文件

在 `src` 目录中，创建一个名为 `Greet.js` 的新文件。这个文件将包含你的 `Greet` 组件。

### 步骤 2：定义函数组件

打开 `Greet.js` 文件，并按如下方式定义 `Greet` 函数组件：

```jsjsx

import React from 'react';

function Greet(props) {

return <h1>Hello, {props.name}!</h1>;

}

export default Greet;

```

在这段代码中：

- 我们定义了 `Greet` 函数组件，它接受一个名为 `name` 的单一 prop。

- 在组件的 JSX 内部，我们使用花括号 `{props.name}` 将 `name` prop 的值插入到消息中。

### 步骤 3：使用 Props 渲染组件

现在，让我们使用 prop 值渲染 `Greet` 组件。再次打开 `src/App.js` 文件，并在文件顶部导入 `Greet` 组件：

```jsjsx

import Greet from './Greet';

```

接下来，更新 `App` 组件的 `render` 方法，将 `Greet` 组件与 `name` prop 一起包含：

```jsjsx

function App() {

return (

<div className="App">

<Greet name="React Enthusiast" />

</div>

);

}

```

在这段代码中：

- 我们导入了 `Greet` 组件。

- 我们在 `App` 组件的 JSX 中包含了 `Greet` 组件，并传递了一个值为 "React Enthusiast" 的 `name` prop。

### 第 4 步：查看带有 props 的组件

保存你对 `src/App.js` 文件所做的更改，并确保你的开发服务器正在运行（使用 `npm start`）。

`.

当你在网页浏览器中查看 React 应用时，你应该会看到页面上显示 "Hello, React Enthusiast!" 的消息。你传递给 `Greet` 组件的 `name` prop 会动态插入到消息中。

## 在类组件中使用状态

状态（State）是 React 中一个至关重要的概念，它允许组件管理和维护其数据。虽然函数组件非常适合根据 props 渲染 UI，但类组件也可以管理内部状态。在这一部分，我们将创建一个名为 `Counter` 的类组件，来探索如何使用状态。

### 第 1 步：创建一个新的组件文件

在你的 `src` 目录下，创建一个名为 `Counter.js` 的新文件。这个文件将包含你的 `Counter` 类组件。

### 第 2 步：定义类组件

打开 `Counter.js` 文件，并定义如下的 `Counter` 类组件：

```jsjsx

import React, { Component } from 'react';

class Counter extends Component {

constructor(props) {

super(props);

this.state = {

count: 0,

};

}

render() {

return (

<div>

<p>Count: {this.state.count}</p>

<button onClick={this.incrementCount}>Increment</button>

</div>

);

}

incrementCount = () => {

this.setState({ count: this.state.count + 1 });

};

}

export default Counter;

```

在这段代码中：

- 我们从 'react' 中导入 `React` 和 `Component`。

- 我们定义了 `Counter` 类组件，其中包括一个 `constructor` 方法，用于初始化其状态，设置 `count` 属性为 0。

- 在 `render` 方法中，我们使用 `{this.state.count}` 显示当前的计数，并提供一个带有 `onClick` 事件处理程序的按钮。

- `incrementCount` 方法被定义用来在按钮点击时更新组件的状态。它使用 `this.setState` 来增加 `count` 属性的值。

### 第 3 步：渲染类组件

现在，让我们在 `src/App.js` 文件中渲染 `Counter` 类组件。在文件顶部导入 `Counter` 组件：

```jsjsx

import Counter from './Counter';

```

接下来，在 `App` 组件的 `render` 方法中包含 `Counter` 组件：

```jsjsx

function App() {

return (

<div className="App">

<Counter />

</div>

);

}

```

### 第 4 步：查看你的类组件

保存你对`src/App.js`文件所做的更改，并确保你的开发服务器正在运行，可以使用`npm start`命令启动。

当你在网页浏览器中查看你的 React 应用时，你将看到“Count: 0”消息和一个标有“Increment”的按钮。点击“Increment”按钮将更新计数，演示了如何在类组件中使用 state 来管理和显示数据。

## 结论

在本章中，你迈出了创建和使用 React 组件的第一步。你学习了函数组件和类组件的基础知识，如何向组件传递 props，以及如何管理组件的 state。这些概念是使用 React 构建动态和交互式用户界面的基本构建块。

在你继续 React 学习之旅时，请记住，组件是你应用程序的构建块，它们可以组合在一起创建复杂的用户界面。尝试创建你自己的组件、传递 props 和管理 state，以增强你使用 React 的信心。
