# # 第4章：React 中的 State 和 Props

在上一章，你对 React 组件有了基础的理解，学习了如何创建组件，以及如何通过 props 传递数据和管理状态。在本章中，我们将更深入地探讨 React 中的 state 和 props，探索它们的作用、区别以及如何有效使用它们的最佳实践。通过掌握 state 和 props，你将能够构建动态和交互式的用户界面。

## 理解 Props：数据从父组件流向子组件

Props，简称“属性”，是 React 中从父组件传递数据到子组件的主要机制。它们通过提供外部数据和配置，使你的组件变得动态。以下是 props 工作原理的概述：

1\. **父组件**：Props 起源于父组件。父组件定义它希望传递给子组件的数据或值。

2\. **子组件**：子组件接收父组件传递下来的 props。这些 props 本质上是只读的，不能在子组件内部修改。

3\. **使用 Props 渲染**：在子组件的渲染逻辑中，你可以访问并使用 props 来显示数据、定制行为或构建组件的 UI。

### 传递 Props

让我们探讨如何将 props 从父组件传递到子组件。假设你有一个名为 `Parent` 的父组件和一个名为 `Child` 的子组件。以下是如何传递 props 的方式：

#### 父组件（`Parent.js`）：

```jsjsx

import React from 'react';

import Child from './Child';

function Parent() {

// Define data to be passed as props

const greeting = "Hello, React!";

return (

<div>

{/* Pass the 'greeting' prop to the 'Child' component */}

<Child message={greeting} />

</div>

);

}

export default Parent;

```

在父组件（`Parent.js`）中，我们定义一个变量 `greeting`，然后将其作为名为 `message` 的 prop 传递给 `Child` 组件。

#### 子组件（`Child.js`）：

```jsjsx

import React from 'react';

function Child(props) {

return (

<div>

<p>{props.message}</p>

</div>

);

}

export default Child;

```

在子组件（`Child.js`）中，我们接收 `message` prop 并用它来显示问候信息。

### 使用 Props

在子组件中使用 props 非常简单。你可以将 props 当作 `props` 对象的属性来访问。在上面的示例中，我们使用 `props.message` 来访问从父组件传递过来的 `message` prop。

```jsjsx

<p>{props.message}</p>

```

在子组件中，Props 是不可变的，这意味着你不能直接改变它们的值。Props 作为父组件与子组件之间传递数据的方式，允许你构建可重用和可组合的组件。

## 理解状态：管理组件数据

虽然 props 促进了父组件向子组件的数据流动，但状态是一个至关重要的概念，它使组件能够管理和维护自己的数据。状态代表了组件中的动态和可变信息，比如用户输入、应用数据或 UI 状态。以下是状态的关键方面：

1\. **局部于组件**：每个组件可以拥有自己的状态，独立于其他组件。这使得组件内部的数据能够实现封装和隔离。

2\. **可变的**：与不可变的 props 不同，状态是可变的。你可以随着时间改变状态的值，从而触发组件更新和重新渲染。

3\. **由类组件管理**：状态主要在类组件中使用。函数组件可以通过 React 的 `useState` 钩子来使用状态，该钩子是在 React 16.8 及之后的版本中引入的。

### 在类组件中使用状态

要在类组件中使用状态（state），你需要理解以下几个关键概念：

#### 初始化状态

你可以在构造函数中使用 `this.state` 来初始化组件的状态。通常，状态属性会在组件的构造函数中定义。例如：

```jsjsx

class MyComponent extends React.Component {

constructor(props) {

super(props);

this.state = {

count: 0,

isActive: true,

inputValue: '',

};

}

// ...

}

```

在这个示例中，我们定义了三个状态属性：`count`、`isActive` 和 `inputValue`，每个属性都有其初始值。

#### 访问状态

你可以使用 `this.state` 来访问状态属性。例如，要访问 `count` 状态，你可以使用 `this.state.count`。以下是渲染组件状态的示例：

```jsjsx

render() {

return (

<div>

<p>Count: {this.state.count}</p>

<p>Active: {this.state.isActive ? 'Yes' : 'No'}</p>

<input

type="text"

value={this.state.inputValue}

onChange={this.handleInputChange}

/>

</div>

);

}

```

在这个`render`方法中，我们访问`count`、`isActive`和`inputValue`状态属性。

#### 更新状态

要更新组件的状态，你应该使用`this.setState()`。此方法用于更新状态属性并触发组件重新渲染。以下是一个示例：

```jsjsx

incrementCount = () => {

this.setState({ count: this.state.count + 1 });

};

toggleActive = () => {

this.setState({ isActive: !this.state.isActive });

};

handleInputChange = (event) => {

this.setState({ inputValue: event.target.value });

};

```

在这些示例中，我们定义了使用`this.setState()`来响应各种事件更新`count`、`isActive`和`inputValue`状态属性的函数。

#### 异步更新

请记住，`this.setState()`可能会异步更新状态。为了性能考虑，React 会批量处理状态更新。如果你需要在调用`this.setState()`后立即访问更新后的状态，你可以将回调函数作为第二个参数传递：

```jsjsx

this.setState({ count: this.state.count + 1 }, () => {

console.log('Updated count:', this.state.count);

});

```

这确保了回调函数会在状态更新后被调用。

### 在函数组件中使用状态与`useState`

随着 React 16.8 引入了 hooks，函数组件也可以使用`useState`钩子来管理状态。Hooks 允许你在不编写类的情况下使用状态和其他 React 特性。以下是如何在函数组件中使用`useState`：

```jsjsx

import

React, { useState } from 'react';

function Counter() {

// Initialize state using the 'useState' hook

const [count, setCount] = useState(0);

// Define a function to update the state

const incrementCount = () => {

setCount(count + 1);

};

return (

<div>

<p>Count: {count}</p>

<button onClick={incrementCount}>Increment</button>

</div>

);

}

export default Counter;

```

在这个函数组件中，我们使用`useState`初始化`count`状态，并使用`setCount`函数更新它。`setCount`函数在状态变化时会自动触发重新渲染。

## Props 与 State：何时使用哪一个

理解何时使用 props 和何时使用 state 对于高效构建 React 应用程序至关重要。以下是选择每种情况的指南：

### Props

当你需要使用 props 时：

1. 你需要将数据从父组件传递到子组件。

2. 数据在子组件中是只读的。

3. 你希望配置和定制子组件。

4. 你希望组件具有可重用性和可组合性。

5. 你希望确保应用程序中的数据流是可预测的。

### 状态

当你需要使用状态时：

1. 你需要在组件内部管理和更新数据。

2\. 数据特定于该组件，并未与其他组件共享。

3\. 你希望通过重新渲染组件来反映数据的变化。

4\. 你正在处理用户输入或 UI 交互。

5\. 你需要维护与 UI 相关的信息，例如切换开关、表单输入或组件可见性。

理解这些区别有助于你设计出模块化、可维护且高效的 React 组件。

## 操作 Props 和 State 的最佳实践

为了确保你的 React 组件结构良好且易于维护，在处理 props 和 state 时，可以考虑以下最佳实践：

### Props 最佳实践

1\. **保持 Props 不可变**：Props 应在组件内部视为不可变。避免直接修改 props；应依赖 props 来获取只读数据。

2\. **记录 Props**：记录组件预期的 props，包括其类型和默认值。你可以使用 PropTypes 或 TypeScript 来实现这一点。

3\. **默认 Prop 值**：在合适的情况下，使用默认函数参数或类组件的 defaultProps 为 props 提供默认值。

4\. **解构 Props**：在函数组件的参数中或组件体内解构 props 可以提高代码的可读性。

```jsjsx

// Before destructuring

function MyComponent(props) {

return <div>{props.message}</div>;

}

// After destructuring

function MyComponent({ message }) {

return <div>{message}</div>;

}

```

5\. **使用 Prop 校验**：在构建可重用组件时，考虑使用 Prop 校验库，如 PropTypes 或 TypeScript，以确保 props 的类型和形状正确。

### 状态最佳实践

1\. **正确初始化 State**：在构造函数中初始化 state（用于类组件）或使用 `useState` 钩子（用于函数组件）。确保初始状态反映组件的起始状态。

2\. **避免直接修改状态**：永远不要直接修改状态；使用`this.setState`（用于类组件）或`useState`返回的更新函数（用于函数组件）来更新状态。

3\. **功能性状态更新**：当根据之前的值更新状态时，使用`this.setState`的函数式形式（适用于类组件）或更新函数（适用于函数组件），以确保更新的准确性，尤其是在异步场景中。

4\. **无状态组件**：尽可能偏好无状态的函数组件，而不是类组件，用于根据props渲染UI。将类组件保留给那些需要状态管理和生命周期方法的组件。

5\. **提升状态**：当多个组件需要访问相同的状态或需要同步它们的状态时，将状态提升到一个共同的父组件，并通过props将其传递下去。

6\. **使用受控组件**：对于表单元素如输入框，使用受控组件。将输入框的值绑定到一个状态属性，并通过状态更新处理变化。

## 结论

在本章中，你加深了对React中状态（state）和属性（props）的理解，这两个基本概念驱动着动态和交互式的用户界面。Props使得数据可以从父组件流向子组件，而state赋予组件管理自身动态数据的能力。

通过选择适合的工具—使用props进行数据流和配置，使用state管理组件特定的数据—you'll create well-structured, maintainable, and efficient React applications. 你还学习了使用props和state的最佳实践，确保你的代码保持可读性和可靠性。
