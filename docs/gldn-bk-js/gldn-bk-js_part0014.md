# `第11章`

`React：基础与应用`

欢迎来到关于React的章节，这是创建现代用户界面最流行和广泛使用的库之一。让我们探索React的基础知识，包括组件与props、状态和组件生命周期。本章对于任何想要创建动态和响应式Web应用程序的开发者来说都是必不可少的。

`React基础`

React是一个由`Facebook`开发的JavaScript库，于`2013`年推出。React的主要理念是以声明的方式创建用户界面，组合可重用的组件。React使用`虚拟DOM`来优化用户界面的更新，确保仅更新必要的DOM部分，从而提高性能。

`为什么使用React？`

- `组件化`：React允许你将用户界面分割成独立的、可重用的组件，每个组件管理自己的状态。

- `性能`：使用虚拟DOM减少了对真实DOM的直接操作成本，使更新更高效。

- `单向数据流`：React采用单向数据流，使得跟踪应用程序状态的变化变得更容易。

- `强大的生态系统`：一个庞大的社区和丰富的库及工具生态系统支持使用React进行开发。

`组件与props`

组件是React的基础。它们可以定义为函数或类，代表用户界面的独立部分。组件可以通过`props`（属性）接收数据，并维护自己的状态。

`函数组件`

函数组件是一个接受`props`作为参数并返回React元素的JavaScript函数。

```jsjavascript

function Saudacao(props) {

return <h1>Hello, {props.name}!</h1>;

}

```

在这个示例中，`Greetings`是一个函数组件，显示自定义问候语。`props.nome`的值被插入到组件渲染中。

`类组件`

类组件是一个扩展自`React.Component`的ES6类，并定义一个返回React元素的`render`方法。

```jsjavascript

class Saudacao extends React.Component {

render() {

return <h1>Hello, {this.props.name}!</h1>;

}

}

```

在这里，`Saudacao`是一个类组件，使用`this.props`来访问传递给组件的属性。

`Props`

`Props`是传递给React组件的参数。它们允许将数据从父组件传递到子组件。

```jsjavascript

function App() {

return <Greeting name="John" />;

}

```

在上面的示例中，`App`组件将值为"João"的`nome`属性传递给`Greeting`组件。

`组件的状态与生命周期`

组件的状态是一个数据结构，用于存储可以随时间变化的信息。与不可变的`props`不同，状态可以通过`setState`方法进行更改。

`类组件中的状态`

类组件使用构造函数来初始化状态。

```jsjavascript

class Contador extends React.Component {

constructor(props) {

super(props);

this.state = { contador: 0 };

}

increment = () => {

this.setState({ contador: this.state.contador + 1 });

};

render() {

return (

<div>

<h1>{this.state.contador}</h1>

<button onClick={this.incrementar}>Incrementar</button>

</div>

);

}

}

```

在上面的示例中，`Counter`是一个管理其状态中计数器的类组件。`increment`方法使用`setState`来更新状态并重新渲染组件。

`函数组件中的状态与钩子`

React在`React 16.8`中引入了`钩子`，允许在函数组件中使用状态和其他React特性。

```jsjavascript

import React, { useState } from 'react';

function Contador() {

const [counter, setCounter] = useState(0);

const increment = () => {

setCounter(counter + 1);

};

return (

<div>

<h1>{counter}</h1>

<button onClick={increment}>Increment</button>

</div>

);

}

```

在此示例中，我们使用`useState` Hook为`Counter`函数组件添加状态。`increment`函数更新状态并重新渲染组件。

生命周期的两个组件

React中的类组件具有生命周期方法，允许代码在组件存在的特定时刻执行。一些主要的生命周期方法包括：

- `componentDidMount`：在组件插入DOM后执行。

- `componentDidUpdate`：在组件更新后执行。

- `componentWillUnmount`：在组件从DOM中移除之前执行。

使用生命周期方法的示例

```jsjavascript

class Relogio extends React.Component {

constructor(props) {

super(props);

this.state = { data: new Date() };

}

componentDidMount() {

this.timerID = setInterval(() => this.tick(), 1000);

}

componentDidUpdate() {

console.log('The clock has been updated.');

}

componentWillUnmount() {

clearInterval(this.timerID);

}

tick() {

this.setState({ data: new Date() });

}

render() {

return (

<div>

<h1>Current time: {this.state.data.toLocaleTimeString()}</h1>

</div>

);

}

}

```

在此示例中，`Clock`组件在`componentDidMount`方法中设置定时器，以每秒更新一次时间。当组件从DOM中移除时，`componentWillUnmount`方法会清除定时器。

在这一章中，我们探讨了React的基础知识，包括组件和属性、状态以及组件生命周期。React允许您通过组合可重用组件来创建动态和高效的用户界面。理解这些基本概念后，您将能够很好地构建现代交互式Web应用程序。随着我们深入，继续探索更多高级React特性及其如何集成到您的应用程序中，以最大化其潜力。请继续练习并应用这些概念，成为使用React编程艺术的专家。
