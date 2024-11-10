# 第 9 章

异步编程

我们即将深入现代 web 开发中最强大和实用的方面之一：与 API 互动和发起 AJAX 请求。这些概念对于创建动态、交互式应用程序至关重要，这些应用程序可以与服务器通信以实时发送和接收数据。我们将探讨 API 和 AJAX 的概念，学习如何执行 AJAX 请求，并理解如何高效地消费 `RESTful API`。

API 和 AJAX 概念

API（`应用程序编程接口`）是一组规则和定义，允许不同的软件系统相互通信。API 定义了应用程序可以用来连接服务或其他软件的方法和数据。API 有不同类型，但最常见和广泛使用的是 `RESTful API`。

`AJAX`（`异步 JavaScript 和 XML`）是一种允许浏览器与服务器之间进行异步通信而无需重新加载页面的技术。这使得用户体验更加流畅和响应，因为页面的部分可以动态更新。

发起 AJAX 请求

让我们开始学习如何使用纯 JavaScript 执行 AJAX 请求。最古老的方法之一是使用 `XMLHttpRequest` 对象。

使用 `XMLHttpRequest` 的 AJAX 请求示例：

```jsjavascript

function fetchData(url) {

const xhr = new XMLHttpRequest();

xhr.open("GET", url);

xhr.onload = function() {

if (xhr.status === 200) {

console.log(JSON.parse(xhr.responseText));

} else {

console.error(`Error: ${xhr.status}`);

}

};

xhr.onerror = function() {

console.error("Network error");

};

xhr.send();

}

fetchData("https://api.exemplo.com/dados");

```

在这个示例中，我们创建一个新的 `XMLHttpRequest` 实例，使用 `open` 配置请求，并使用 `send` 发送请求。我们使用 `onload` 和 `onerror` 事件来处理请求响应和可能的错误。

随着语言的发展，`Fetch API` 应运而生，它提供了一种更现代和简化的 AJAX 请求方式。

使用 `Fetch` 的 AJAX 请求示例：

```jsjavascript

function fetchData(url) {

fetch(url)

.then(response => {

if (!response.ok) {

throw new Error(`Erro: ${response.status}`);

}

return response.json();

})

.then(data => {

console.log(data);

})

.catch(error => {

console.error(error);

});

}

fetchData("https://api.exemplo.com/dados");

```

`Fetch` 简化了语法，使代码更具可读性和易于理解。它返回一个 promise，可以使用 `then` 和 `catch` 分别处理响应和错误。

消费 `RESTful API`

`RESTful`（`表现层状态转移`）API 是创建 Web 服务的一种架构风格。它们使用标准的 HTTP 方法（`GET`、`POST`、`PUT`、`DELETE`）来执行 CRUD（`创建`、`读取`、`更新`、`删除`）操作。

让我们探索如何使用 `Fetch` 消费 `RESTful API`，涵盖最常见的操作。

`GET`：获取数据

```jsjavascript

async function fetchData() {

try {

const response = await fetch("https://api.exemplo.com/dados");

if (!response.ok) {

throw new Error(`Erro: ${response.status}`);

}

const data = await response.json();

console.log(data);

} catch (error) {

console.error(error);

}

}

fetchData();

```

`POST`：发送数据

```jsjavascript

async function sendData(url, data) {

try {

const response = await fetch(url, {

method: "POST",

headers: {

"Content-Type": "application/json"

},

body: JSON.stringify(dados)

});

if (!response.ok) {

throw new Error(`Erro: ${response.status}`);

}

const response = await response.json();

console.log(response);

} catch (error) {

console.error(error);

}

}

const data = { name: "João", age: 30 };

sendData("https://api.exemplo.com/dados", data);

```

`PUT`：更新数据

```jsjavascript

async function updateData(url, data) {

try {

const response = await fetch(url, {

method: "PUT",

headers: {

"Content-Type": "application/json"

},

body: JSON.stringify(dados)

});

if (!response.ok) {

throw new Error(`Erro: ${response.status}`);

}

const response = await response.json();

console.log(response);

} catch (error) {

console.error(error);

}

}

const updateddata = { name: "João", age: 31 };

updateDados("https://api.exemplo.com/dados/1", dadosAtualizados);

```

`DELETE`：删除数据

```jsjavascript

async function deletarDados(url) {

try {

const response = await fetch(url, {

method: "DELETE"

});

if (!response.ok) {

throw new Error(`Erro: ${response.status}`);

}

console.log("Data deleted successfully");

} catch (error) {

console.error(error);

}

}

deleteData("https://api.exemplo.com/dados/1");

```

错误处理

在消费 API 时，有效处理错误是很重要的，以确保应用程序能够处理网络问题或意外的服务器响应。

使用 `Fetch` 的错误处理：

```jsjavascript

async function fetchData(url) {

try {

const response = await fetch(url);

if (!response.ok) {

throw new Error(`Erro: ${response.status}`);

}

const data = await response.json();

return data;

} catch (error) {

console.error("Error fetching data:", error);

throw erro;

}

}

async function displayData() {

try {

const data = await fetchData("https://api.exemplo.com/dados");

console.log(data);

} catch (error) {

console.error("Error displaying data:", error);

}

}

displayData();

```

在这个示例中，我们使用 `try/catch` 块来捕获和处理请求及数据处理中的错误。这使得应用程序能够优雅地处理错误并向用户提供反馈。

在本章中，我们探索 API 和 AJAX 的概念，学习如何使用 `XMLHttpRequest` 和 `Fetch` 执行 AJAX 请求，并理解如何高效地消费 RESTful API。这些知识对于开发现代和动态的 Web 应用程序至关重要，这些应用程序依赖于与服务器的持续通信以发送和接收数据。随着你继续你的 Web 开发旅程，掌握与 API 的交互和处理 AJAX 请求将对创建丰富、响应迅速的用户体验至关重要。继续练习并应用这些概念，成为 JavaScript 网页编程艺术的高手。
