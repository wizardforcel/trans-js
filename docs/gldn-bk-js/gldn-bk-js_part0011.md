# `第8章`  

`异步编程`  

让我们探索JavaScript开发中最迷人且富有挑战性的领域之一：异步编程。本章对于理解如何处理可能需要时间的操作（如网络请求或文件读写操作）而不阻塞程序的主要流程至关重要。我们将讨论回调和`promises`，深入了解强大的`async/await`语法，并讨论异步错误处理。  

`回调和承诺`  

异步编程对于创建响应迅速且高效的应用程序至关重要。在`promises`和`async/await`出现之前，回调是处理异步操作的主要方式。  

`回调`  

回调是作为参数传递给另一个函数的函数，该函数将在操作完成后执行。尽管它们功能强大，但当嵌套过深时，回调可能导致所谓的“回调地狱”。  

`回调示例:`  

```jsjavascript

function buscarDados(url, callback) {

const xhr = new XMLHttpRequest();

xhr.open("GET", url);

xhr.onload = function() {

if (xhr.status === 200) {

callback(null, xhr.responseText);

} else {

callback(`Erro: ${xhr.status}`);

}

};

xhr.send();

}

fetchData("https://api.exemplo.com/dados", function(error, data) {

if (error) {

console.error(error);

} else {

console.log(JSON.parse(data));

}

});

```

在这个例子中，`BuscaDados`使用一个回调来处理请求响应。如果出现错误，它将被传递给回调，否则数据将被处理。  

`Promises`  

`Promises`的引入旨在解决与回调相关的许多问题。`Promise`是一个对象，表示异步操作的最终完成或失败。  

`Promise 示例:`  

```jsjavascript

function fetchData(url) {

return new Promise(function(resolve, reject) {

const xhr = new XMLHttpRequest();

xhr.open("GET", url);

xhr.onload = function() {

if (xhr.status === 200) {

resolve(xhr.responseText);

} else {

reject(`Erro: ${xhr.status}`);

}

};

xhr.send();

});

}

fetchData("https://api.exemplo.com/dados")

.then(function(dados) {

console.log(JSON.parse(data));

})

.catch(function(erro) {

console.error(error);

});

```

`Promises`使异步代码更具可读性，更易于管理，通过使用`then`链式操作并使用`catch`处理错误。  

`Async/await`  

`async/await`是ES2017中引入的一种语法，允许你以更同步和可读的方式编写异步代码。`async`标记一个函数为异步，`await`暂停函数的执行，直到承诺被解决。

`Async/await 示例:`  

```jsjavascript

async function fetchData(url) {

try {

const response = await fetch(url);

if (!response.ok) {

throw new Error(`Error: ${response.status}`);

}

const data = await response.json();

return data;

} catch (error) {

console.error(error);

}

}

async function displayData() {

const data = await fetchData("https://api.exemplo.com/dados");

console.log(data);

}

displayData();

```

使用`async/await`大大简化了异步代码的阅读和维护，消除了复杂的承诺链的需求。  

`异步错误处理`  

有效处理错误对于任何应用程序的健壮性至关重要。在异步编程中，正确捕获和处理错误是防止它们中断程序流程的关键。  

`处理回调的错误:`  

```jsjavascript

function buscarDados(url, callback) {

const xhr = new XMLHttpRequest();

xhr.open("GET", url);

xhr.onload = function() {

if (xhr.status === 200) {

callback(null, xhr.responseText);

} else {

callback(`Erro: ${xhr.status}`);

}

};

xhr.onerror = function() {

callback("Network error");

};

xhr.send();

}

fetchData("https://api.exemplo.com/dados", function(error, data) {

if (error) {

console.error(error);

} else {

console.log(JSON.parse(data));

}

});

```

在上面的例子中，`onerror`捕获网络错误并将其传递给回调。  

`处理承诺的错误:`  

```jsjavascript

function fetchData(url) {

return new Promise(function(resolve, reject) {

const xhr = new XMLHttpRequest();

xhr.open("GET", url);

xhr.onload = function() {

if (xhr.status === 200) {

resolve(xhr.responseText);

} else {

reject(`Erro: ${xhr.status}`);

}

};

xhr.onerror = function() {

reject("Network error");

};

xhr.send();

});

}

fetchData("https://api.exemplo.com/dados")

.then(function(dados) {

console.log(JSON.parse(data));

})

.catch(function(erro) {

console.error(error);

});

```

使用`promises`时，错误是通过使用`catch`方法捕获的。  

`处理 async/await 的错误:`  

```jsjavascript

async function fetchData(url) {

try {

const response = await fetch(url);

if (!response.ok) {

throw new Error(`Error: ${response.status}`);

}

const data = await response.json();

return data;

} catch (error) {

console.error(error);

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

使用`async/await`时，`try/catch`块用于以更结构化的方式捕获错误。  

我们探讨了`JavaScript`中异步编程的主要概念和技术，包括`回调`、`承诺`和`async/await`。每种方法都有其优点和适用场景，但语言的演变使得通过引入`承诺`和`async/await`来管理异步操作变得更加直观和高效。理解这些工具对于开发现代和响应迅速的应用程序至关重要。随着我们前进，这些技能将对处理网络应用程序日益复杂的情况至关重要，并确保它们稳健、高效且易于维护。持续练习并应用这些概念，以掌握在`JavaScript`中异步编程的艺术。  
