# # 第11章：与API的工作

在第10章中，我们探讨了ES6及以后版本引入的现代JavaScript特性，这些特性极大地提高了语言的表现力和可维护性。现在，让我们深入了解API（应用程序编程接口）的世界。API使不同的软件系统能够相互通信和互动，允许开发者在应用程序中访问并使用外部服务、数据或功能。与API的工作是网页开发者的基本技能，因为它使他们能够集成强大的服务、从远程服务器获取数据，并构建动态和功能丰富的网页应用程序。在本章中，我们将探索API的概念，如何与它们互动，以及如何通过各种方法消费数据。

## 1. 什么是API？

API（应用程序编程接口）是一组规则和协议，允许不同的软件系统相互通信。API定义了应用程序可以使用的方法和数据格式，用于请求和交换信息。API可以用于与远程服务器互动、访问数据库、集成第三方服务以及执行各种其他任务。

## 2. API的类型

API有几种类型，每种类型的用途不同：

### a. Web API：

Web API是通过互联网暴露的API，可以通过HTTP请求访问。这些API通常用于网页开发中，用于获取数据、执行CRUD（创建、读取、更新、删除）操作，以及与各种服务交互。

### b. RESTful API：

REST（表述性状态转移）是一种设计网络应用程序的架构风格。RESTful API遵循REST原则，并使用标准的HTTP方法（GET、POST、PUT、DELETE）对资源进行操作。

### c. SOAP API：

SOAP（简单对象访问协议）是一种用于在实现 Web 服务中交换结构化信息的协议。SOAP API 使用 XML 来表示数据，并依赖 HTTP 协议进行通信。

### d. GraphQL API：

GraphQL 是一种用于 API 的查询语言，允许客户端仅请求所需的数据。与传统的 REST API 不同，GraphQL API 允许客户端指定他们希望检索的确切数据，从而使其更加高效和灵活。

## 3. API 请求和响应

与 API 交互时，开发者向 API 的端点发送请求，指定所需的操作和任何必需的数据。API 处理请求并返回响应，响应中包含请求的数据或有关操作成功与否的信息。

### a. HTTP 方法：

API 请求通常使用标准的 HTTP 方法：

- GET: 用于从服务器检索数据。

- POST: 用于向服务器发送数据以创建新资源。

- PUT: 用于更新服务器上的现有资源。

- DELETE: 用于从服务器移除资源。

### b. 请求头：

请求头提供了有关请求的附加信息，例如身份验证令牌、内容类型和用户代理详细信息。

### c. 请求参数：

请求参数用于将数据传递给服务器，通常通过 URL 或请求体传递。

### d. 响应状态码：

API 响应包括状态码，指示请求的结果。常见的状态码包括：

- 200 OK: 请求成功。

- 201 Created: 请求导致了新资源的创建。

- 400 Bad Request: 请求无效或格式错误。

- 401 Unauthorized: 请求需要身份验证。

- 404 Not Found: 请求的资源未找到。

- 500 Internal Server Error: 服务器在处理请求时遇到错误。

## 4. 使用 JavaScript 消耗 API

JavaScript 提供了多种方法来消费 API 并从远程服务器获取数据。我们来看看一些常见的技术：

### a. Fetch API：

Fetch API 是一种现代的 JavaScript API，允许你发起网络请求并使用 promises 处理响应。它广泛用于向 API 发起 HTTP 请求。

```jsjavascript

// Example 1: Using Fetch API

fetch("https://api.example.com/data")

.then((response) => response.json())

.then((data) => console.log(data))

.catch((error) => console.log("Error:", error));

```

在上面的示例中，我们使用 Fetch API 向 API 端点发起 GET 请求，并记录检索到的数据。

### b. XMLHttpRequest：

XMLHttpRequest 是一个较老的 API，提供了发起网络请求的能力，尽管它不像 Fetch API 那样常用。

```jsjavascript

// Example 2: Using XMLHttpRequest

const xhr = new XMLHttpRequest();

xhr.open("GET", "https://api.example.com/data", true);

xhr.onload = function () {

if (xhr.status === 200) {

const data = JSON.parse(xhr.responseText);

console.log(data);

} else {

console.log("Error:", xhr.statusText);

}

};

xhr.onerror = function () {

console.log("Network error occurred");

};

xhr.send();

```

在上面的示例中，我们使用 XMLHttpRequest 发起 GET 请求并处理响应。

### c. Axios：

Axios 是一个流行的第三方库，用于在 JavaScript 中进行 HTTP 请求。它提供了一个简单方便的接口来与 API 进行交互。

```jsjavascript

// Example 3: Using Axios

axios.get("https://api.example.com/data")

.then((response) => console.log(response.data))

.catch((error) => console.log("Error:", error));

```

在上面的示例中，我们使用 Axios 发起 GET 请求并记录检索到的数据。

## 5\. API 认证操作

许多 API 需要认证，以确保只有授权的用户或应用程序能够访问它们的资源。API 认证有多种方法，包括：

### a. API 密钥：

API 密钥是一个唯一标识符，开发者在 API 请求中包含该密钥，以标识自己并获取对 API 资源的访问权限。

```jsjavascript

// Example 4: Using API Key for authentication with Fetch API

const apiKey = "YOUR_API_KEY";

fetch(`https://api.example.com/data?apiKey=${apiKey}`)

.then((response) => response.json())

.then((data) => console.log(data))

.catch((error) => console.log("Error:", error));

```

在上面的示例中，我们将 API 密钥作为查询参数包含在请求 URL 中。

### b. OAuth：

OAuth（开放授权）是一种更安全且复杂的认证协议，用于代表用户访问第三方 API。

## 6\. 分页和筛选操作

API 通常返回大量数据，这些数据需要分页或筛选以高效地检索特定信息。

### a. 分页：

分页允许你按块或按页检索数据，从而减少每次请求中传输的数据量。

```jsjavascript

// Example 5: Using pagination with Fetch API

const page = 2;

const pageSize = 10;

fetch(`https://api.example.com/data?page=${page}&pageSize=${pageSize}`)

.then((response) => response.json())

.then((data) => console.log(data))

.catch((error) => console.log("Error:", error));

```

在上面的示例中，我们使用分页来请求第二页数据，每页大小为 10 条。

### b. 筛选：

过滤功能允许你指定检索符合特定条件的数据的标准。

```jsjavascript

// Example 6: Using filtering with Fetch API

const category = "electronics";

fetch(`https://api.example.com/data?category=${category}`)

.then((response) =>

response.json())

.then((data) => console.log(data))

.catch((error) => console.log("Error:", error));

```

在上述示例中，我们使用过滤来请求与“电子产品”类别相关的数据。

## 7\. CORS（跨源资源共享）

CORS 是浏览器实施的一项安全功能，它防止网页向与提供网页的域不同的域发出请求。API 可能需要支持 CORS，以允许来自其他域的请求。

## 8\. API 错误处理

在使用 API 时，必须优雅地处理错误并向用户提供有意义的反馈。

```jsjavascript

// Example 7: Handling errors with Fetch API

fetch("https://api.example.com/data")

.then((response) => {

if (!response.ok) {

throw new Error("Network response was not ok");

}

return response.json();

})

.then((data) => console.log(data))

.catch((error) => console.log("Error:", error));

```

在上述示例中，我们使用 Fetch API 处理错误，并在网络响应不正常时抛出错误。

## 9\. API 最佳实践

在使用 API 时，考虑以下最佳实践：

- 在进行 API 请求时始终使用安全的 HTTPS，以确保数据的隐私和安全。

- 实现适当的错误处理，向用户提供有意义的反馈。

- 尊重 API 提供者设定的速率限制和使用配额，以避免被封锁。

- 在适当情况下缓存 API 响应，以减少不必要的请求并提高性能。

- 减少从 API 返回的数据量，以降低带宽使用并提高效率。

## 结论：

在本章中，我们探索了 API 的世界，API 对于 web 开发者与外部服务交互并从远程服务器获取数据至关重要。我们了解了不同类型的 API，如 Web API、RESTful API、SOAP API 和 GraphQL API，以及它们各自的用途。

我们探索了多种使用 JavaScript 调用 API 的方法，包括 Fetch API、XMLHttpRequest 和 Axios。这些方法使我们能够高效地发出 HTTP 请求并处理响应。

此外，我们讨论了使用 API 密钥和 OAuth 进行 API 认证，以及如何使用分页和过滤功能从 API 中检索特定数据。我们还简要提及了 CORS 和在与 API 交互时错误处理的重要性。

通过掌握API概念和集成技术，你可以构建强大而动态的Web应用程序，利用外部服务和数据源。随着你作为Web开发者的不断进步，实践使用API以获得实际经验并提升你的技能。
