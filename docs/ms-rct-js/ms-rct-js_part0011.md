# # 第7章：表单和表单处理

表单是Web应用程序的基础部分，它允许用户输入数据、提交信息并与网站互动。React 提供了强大的工具来处理表单，包括受控组件、表单提交、验证和处理用户输入。在本章中，我们将探索如何在 React 中创建和管理表单，并通过示例来说明这些概念。

## React 中的表单简介

在 React 中，表单是通过 HTML 表单元素创建的，如 `<form>`、`<input>`、`<textarea>` 和 `<select>`。然而，React 为表单数据和用户交互提供了一层抽象，能够更高效地处理这些内容。在使用 React 处理表单时，你将经常遇到以下概念：

### 受控组件

受控组件是指通过 React 组件的状态来渲染表单元素并管理其状态的 React 组件。这意味着表单元素的值由组件的状态控制，输入值的任何变化都会反映在状态中，反之亦然。

```jsjsx

class ControlledForm extends React.Component {

constructor(props) {

super(props);

this.state = {

inputValue: '',

};

}

handleChange = (event) => {

this.setState({ inputValue: event.target.value });

};

handleSubmit = (event) => {

event.preventDefault();

// Access the form data using this.state.inputValue

};

render() {

return (

<form onSubmit={this.handleSubmit}>

<input

type="text"

value={this.state.inputValue}

onChange={this.handleChange}

/>

<button type="submit">Submit</button>

</form>

);

}

}

```

在这个例子中，`<input>` 元素的值由 `inputValue` 状态控制。当用户在输入框中输入时，`handleChange` 方法会更新状态，确保输入值始终与组件的状态同步。

### 表单提交

React 通过监听 `<form>` 元素的 `onSubmit` 事件来处理表单提交。当表单提交时，事件处理函数会被调用，这样你就可以访问并处理表单数据。

```jsjsx

class FormSubmission extends React.Component {

handleSubmit = (event) => {

event.preventDefault();

// Access and process the form data

};

render() {

return (

<form onSubmit={this.handleSubmit}>

{/* Form fields */}

<button type="submit">Submit</button>

</form>

);

}

}

```

在这个例子中，当表单提交时，`handleSubmit` 方法被调用，我们可以在此时进行数据处理或将表单数据发送到服务器。

### 表单验证

表单验证是确保用户输入满足特定标准或约束的过程。React 允许你通过在事件处理函数中添加条件逻辑来实现表单验证，检查输入数据，并向用户提供反馈。

```jsjsx

class FormValidation extends React.Component {

constructor(props) {

super(props);

this.state = {

inputValue: '',

errorMessage: '',

};

}

handleChange = (event) => {

const inputValue = event.target.value;

this.setState({ inputValue });

// Validate the input

if (inputValue.length < 5) {

this.setState({ errorMessage: 'Input must be at least 5 characters' });

} else {

this.setState({ errorMessage: '' });

}

};

handleSubmit = (event) => {

event.preventDefault();

if (this.state.inputValue.length >= 5) {

// Submit the form

} else {

this.setState({ errorMessage: 'Input must be at least 5 characters' });

}

};

render() {

return (

<form onSubmit={this.handleSubmit}>

<input

type="text"

value={this.state.inputValue}

onChange={this.handleChange}

/>

<button type="submit">Submit</button>

<div className="error-message">{this.state.errorMessage}</div>

</form>

);

}

}

```

在这个示例中，我们通过检查输入的长度来验证输入，如果长度少于5个字符，则显示错误消息。错误消息会随着用户输入实时更新，提供即时反馈。

## 创建一个简单的表单

让我们从创建一个简单的 React 表单开始。我们将创建一个表单，允许用户输入姓名和电子邮件地址。当用户提交表单时，我们将显示包含提供的姓名和电子邮件的问候消息。

### 第一步：创建一个新组件

在你的 React 项目中，创建一个名为`SimpleForm.js`的新文件。这个文件将包含`SimpleForm`组件。

### 第二步：定义组件

打开`SimpleForm.js`文件，并按如下方式定义`SimpleForm`组件：

```jsjsx

import React, { Component } from 'react';

class SimpleForm extends Component {

constructor(props) {

super(props);

this.state = {

name: '',

email: '',

submittedData: null,

};

}

handleChange = (event) => {

const { name, value } = event.target;

this.setState({ [name]: value });

};

handleSubmit = (event) => {

event.preventDefault();

const { name, email } = this.state;

const submittedData = { name, email };

this.setState({ submittedData });

};

render() {

const { name, email, submittedData } = this.state;

return (

<div>

<h2>Simple Form</h2>

<form onSubmit={this.handleSubmit}>

<div>

<label>Name:</label>

<input

type="text"

name="name"

value={name}

onChange={this.handleChange}

/>

</div>

<div>

<label>Email:</label>

<input

type="email"

name="email"

value={email}

onChange={this.handleChange}

/>

</div>

<button type="submit">Submit</button>

</form>

{submittedData && (

<div>

<h3>Submitted Data:</h3>

<p>Name: {submittedData.name}</p>

<p>Email: {submittedData.email}</p>

</div>

)}

</div>

);

}

}

export default SimpleForm;

```

在这段代码中：

- 我们定义了`SimpleForm`类组件，该组件有三个状态属性：`name`、`email`和`submittedData`。`submittedData`用于存储提交的表单数据。

- `handleChange`方法会在用户输入字段时更新`name`和`email`状态。我们使用输入元素的`name`属性动态地更新相应的状态属性。

- `handleSubmit`方法在表单提交时被调用。它会阻止表单的默认提交行为，创建一个包含表单数据的对象，并用这个对象更新`submittedData`状态。

- 在`render`方法中，我们显示表单元素，并在有提交数据时有条件地渲染提交的数据。

### 第三步：使用组件

要使用`SimpleForm`组件，在另一个组件中导入它（例如，`App.js`）并渲染它。以下是如何使用它的示例：

```js

jsx

import React from 'react';

import SimpleForm from './SimpleForm';

function App() {

return (

<div className="App">

<SimpleForm />

</div>

);

}

export default App;

```

现在，当你查看你的 React 应用时，你将看到带有姓名和电子邮件输入字段的“简单表单”。提交表单后，提交的数据将显示在下面。

## 表单验证

表单验证对于确保用户提供有效数据至关重要。让我们通过为姓名和电子邮件字段添加验证来增强我们的简单表单。

### 第一步：更新组件

打开 `SimpleForm.js` 文件并按如下方式更新 `SimpleForm` 组件：

```jsjsx

import React, { Component } from 'react';

class SimpleForm extends Component {

constructor(props) {

super(props);

this.state = {

name: '',

email: '',

submittedData: null,

errors: {

name: '',

email: '',

},

};

}

handleChange = (event) => {

const { name, value } = event.target;

this.setState({ [name]: value });

this.validateField(name, value);

};

validateField = (fieldName, value) => {

const errors = { ...this.state.errors };

switch (fieldName) {

case 'name':

errors.name = value.length < 3 ? 'Name must be at least 3 characters' : '';

break;

case 'email':

// A simple email validation regex pattern

const emailPattern = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}$/;

errors.email = emailPattern.test(value) ? '' : 'Invalid email address';

break;

default:

break;

}

this.setState({ errors });

};

handleSubmit = (event) => {

event.preventDefault();

// Check if there are errors

if (this.validateForm()) {

return;

}

const { name, email } = this.state;

const submittedData = { name, email };

this.setState({ submittedData });

};

validateForm = () => {

const { name, email, errors } = this.state;

const isFormInvalid = name.length === 0 || email.length === 0 || Object.values(errors).some((error) => error !== '');

return isFormInvalid;

};

render() {

const { name, email, submittedData, errors } = this.state;

return (

<div>

<h2>Simple Form with Validation</h2>

<form onSubmit={this.handleSubmit}>

<div>

<label>Name:</label>

<input

type="text"

name="name"

value={name}

onChange={this.handleChange}

/>

<span className="error-message">{errors.name}</span>

</div>

<div>

<label>Email:</label>

<input

type="email"

name="email"

value={email}

onChange={this.handleChange}

/>

<span className="error-message">{errors.email}</span>

</div>

<button type="submit">Submit</button>

</form>

{submittedData && (

<div>

<h3>Submitted Data:</h3>

<p>Name: {submittedData.name}</p>

<p>Email: {submittedData.email}</p>

</div>

)}

</div>

);

}

}

export default SimpleForm;

```

在更新的代码中：

- 我们添加了一个 `errors` 状态对象，用于存储 `name` 和 `email` 字段的验证错误。

- 每当用户在输入字段中输入时，`validateField` 方法会被调用。它根据字段名称验证输入，并相应地更新 `errors` 状态。

- 我们添加了一个 `validateForm` 方法，用于检查表单是否有效。如果有验证错误，或者 `name` 或 `email` 字段为空，则认为表单无效。

- 如果表单无效，提交按钮将被禁用，防止用户提交不完整或错误的数据。

现在，表单将向用户提供实时验证反馈，对于无效的输入显示错误信息，并防止提交不完整或无效的数据。

## 结论与最佳实践

在本章中，我们探讨了如何在 React 中创建和处理表单，包括受控组件、表单提交和表单验证。以下是处理 React 表单时需要记住的一些最佳实践：

1\. **使用受控组件**：使用受控组件来管理表单元素的状态，并确保输入值与组件状态之间的同步。

2\. **处理表单提交**：使用 `event.preventDefault()` 阻止默认的表单提交行为，并通过自定义函数处理表单提交。这允许你处理表单数据或执行额外操作。

3\. **实现表单验证**：实现表单验证，确保用户输入符合特定标准。提供

提供清晰且信息丰富的错误信息，以指导用户。

4\. **实时反馈**：考虑在用户与表单互动时提供实时反馈。这包括在更改时验证输入并动态显示错误信息。

5\. **禁用提交按钮**：当表单无效时禁用提交按钮，防止用户提交不完整或无效的数据。

6\. **使用验证库**：对于复杂的表单，考虑使用像 Formik 或 Yup 这样的验证库，以简化表单验证和错误处理。

通过遵循这些最佳实践，你可以在 React 应用程序中创建用户友好且互动性强的表单。表单是用户交互的重要组成部分，掌握 React 中的表单处理将使你能够构建健壮且用户友好的 Web 应用程序。
