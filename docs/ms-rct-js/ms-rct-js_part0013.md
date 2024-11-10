# # 第9章：与API和数据获取的工作

在现代Web开发中，应用程序通常依赖外部数据源提供动态内容和功能。这些外部数据通常通过使用API（应用程序编程接口）来获取。在本章中，我们将探索在React应用程序中与API进行交互并获取数据的过程。

## 理解API

API是允许不同软件应用程序相互通信的一组规则和协议。在Web开发的背景下，API通常用于在客户端（例如Web浏览器）和服务器（例如Web服务器或第三方服务）之间请求和交换数据。

### API类型

API有多种类型，但最常见的两大类是：

1. **RESTful API**：表示性状态转移（REST）API是围绕一组架构原则设计的。它们使用HTTP方法（GET、POST、PUT、DELETE）对资源执行CRUD（创建、读取、更新、删除）操作。REST API广泛用于Web服务。

2. **GraphQL API**：GraphQL是一种用于API的查询语言，允许客户端仅请求所需的数据。与REST API不同，REST API具有预定义的端点并返回固定的数据结构，而GraphQL API使客户端能够定义响应的形状和结构。

### API端点

API通常通过特定的URL（称为端点）进行访问。每个端点对应API提供的特定资源或功能。例如，一个天气API可能有用于获取当前天气、预报和历史数据的端点。

## React中的数据获取

React应用程序经常需要从API获取数据以展示动态内容。为了实现这一点，开发者可以使用JavaScript内置的`fetch()`函数或像Axios这样的库向API端点发送HTTP请求。以下是如何使用`fetch()`函数从API获取数据的示例：

```jsjsx

// Using the fetch() function to fetch data from an API

fetch('https://api.example.com/data')

.then((response) => {

if (!response.ok) {

throw new Error('Network response was not ok');

}

return response.json();

})

.then((data) => {

// Process the data

console.log(data);

})

.catch((error) => {

// Handle errors

console.error('There was a problem with the fetch operation:', error);

});

```

在此示例中：

- 我们使用 `fetch()` 函数向指定的 API 端点（`https://api.example.com/data`）发起 GET 请求。

- 我们通过 `response.ok` 属性检查响应状态是否为 OK（状态码 200）。如果不是，我们抛出错误。

- 如果响应正常，我们使用 `response.json()` 解析 JSON 数据，它会返回一个 promise。

- 然后，我们处理数据或处理在获取数据过程中可能发生的错误。

## 在 React 组件中获取数据

在 React 组件中获取数据时，通常会在生命周期方法或 `useEffect` 钩子中发起数据请求。以下是使用 `useState` 和 `useEffect` 钩子在 React 组件中获取并显示数据的示例：

```jsjsx

import React, { useState, useEffect } from 'react';

function DataFetchingComponent() {

const [data, setData] = useState([]);

const [loading, setLoading] = useState(true);

const [error, setError] = useState(null);

useEffect(() => {

// Make a GET request to fetch data

fetch('https://api.example.com/data')

.then((response) => {

if (!response.ok) {

throw new Error('Network response was not ok');

}

return response.json();

})

.then((data) => {

// Update the data state

setData(data);

setLoading(false); // Set loading to false

})

.catch((error) => {

// Handle errors

setError(error);

setLoading(false); // Set loading to false

});

}, []); // The empty dependency array ensures this effect runs once

if (loading) {

return <div>Loading...</div>;

}

if (error) {

return <div>Error: {error.message}</div>;

}

return (

<div>

<h2>Fetched Data</h2>

<ul>

{data.map((item) => (

<li key={item.id}>{item.name}</li>

))}

</ul>

</div>

);

}

export default DataFetchingComponent;

```

在此示例中：

- 我们定义了一个名为 `DataFetchingComponent` 的组件，使用 `useState` 钩子来管理数据、加载状态和错误状态。

- 我们使用 `useEffect` 钩子在组件挂载时启动数据获取操作（空的依赖数组 `[]` 确保它只运行一次）。

- 在数据获取过程中，我们根据加载状态更新状态，并处理可能出现的错误。

- 最后，根据状态渲染数据或相应的消息。

## 在 React 中使用 Async/Await 获取数据

你还可以使用 `async/await` 语法在 React 组件中发起异步数据请求。以下是如何将 `async/await` 与 `fetch()` 一起使用的示例：

```jsjsx

import React, { useState, useEffect } from 'react';

function DataFetchingComponent() {

const [data, setData] = useState([]);

const [loading, setLoading] = useState(true);

const [error, setError] = useState(null);

useEffect(() => {

async function fetchData() {

try {

const response = await fetch('https://api.example.com/data');

if (!response.ok) {

throw new Error('Network response was not ok');

}

const data = await response.json();

setData(data);

setLoading(false);

} catch (error) {

setError(error);

setLoading(false);

}

}

fetchData();

}, []);

if (loading) {

return <div>Loading...</div>;

}

if (error) {

return <div>Error: {error.message}</div>;

}

return (

<div>

<h2>Fetched Data</h2>

<ul>

{data.map((item) => (

<li key={item.id}>{item.name}</li>

))}

</ul>

</div>

);

}

export default DataFetchingComponent;

```

在此示例中，我们在 `useEffect` 钩子内定义了一个 `async` 函数 `fetchData()`，允许我们使用 `await` 与 `fetch()` 请求一起使用，并通过 `try/catch` 处理错误。其余部分保持不变。

## React 数据获取的最佳实践

在 React 中处理数据获取时，考虑以下最佳实践：

1\. **关注点分离**：将数据获取逻辑与展示组件分开。这有助于改进代码组织结构，使其更容易测试。

2\. **状态管理**：使用 React 状态或像 Redux 这样的状态管理库来管理获取的数据、加载指示器和错误。

3\. **加载指示器**：

提供加载指示器或占位符，告知用户数据正在获取中。

4\. **错误处理**：实现错误处理机制，优雅地处理网络错误或 API 失败，并向用户提供有用的错误信息。

5\. **缓存**：考虑在客户端缓存数据，以减少不必要的 API 请求并提升性能。

6\. **乐观 UI**：在某些情况下，你可以使用乐观 UI 方法，在数据实际保存到服务器之前，乐观地更新 UI。

7\. **认证**：在访问受保护的 API 时，妥善处理认证和授权。安全存储认证令牌。

8\. **代码分割**：考虑进行代码分割，仅在需要时加载数据获取组件，以减少初始包的大小。

## 结论

从 API 获取数据是构建动态和数据驱动的 React 应用程序的基本部分。通过理解 API 的基础，发起 HTTP 请求，并在组件中管理数据，你可以创建提供实时信息和交互性的网页应用程序。随着你继续提升 React 技能，掌握数据获取将使你能够构建更复杂、更具功能的应用程序。
