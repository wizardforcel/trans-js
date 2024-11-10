# 第七章

DOM操作

我们即将探索JavaScript中最动态和最基本的Web开发领域之一：DOM（文档对象模型）操作。这项技能对于任何想要创建交互式和响应式用户界面的开发者来说至关重要。我们将讨论如何选择和操作DOM元素，处理事件，最后介绍虚拟DOM的概念，这一概念彻底改变了我们管理用户界面变化的方式。

DOM元素的选择和操作

DOM是您HTML文档结构的树形表示。每个HTML元素都是树中的一个节点，这些节点可以使用JavaScript访问和操作，以更改页面的内容和外观。

选择元素：操作DOM的第一步是选择您要处理的元素。JavaScript提供了几种方法来做到这一点。

`getElementById`：通过其ID选择一个元素。

```jsjavascript

const title = document.getElementById("title");

console.log(title.innerText); // Displays the text of the element with ID "title"

```

`getElementsByClassName`：选择所有具有给定类的元素。

```jsjavascript

const items = document.getElementsByClassName("item");

console.log(items.length); // Displays the number of elements with class "item"

```

`getElementsByTagName`：选择给定类型的所有元素。

```jsjavascript

const paragraphs = document.getElementsByTagName("p");

console.log(paragraphs.length); // Displays the number of elements <p>

```

`querySelector`和`querySelectorAll`：选择第一个匹配CSS选择器的元素或所有匹配的元素。

```jsjavascript

const firstItem = document.querySelector(".item");

console.log(firstItem.innerText); // Display the text of the first element with class "item"

const todosOsItens = document.querySelectorAll(".item");

todosOsItens.forEach(item => console.log(item.innerText)); // Display the text of all elements with class "item"

```

操作元素：选择元素后，您可以操作它们的属性和内容。

修改文本：使用`innerText`或`textContent`来更改元素的文本。

```jsjavascript

title.innerText = "NewTitle";

```

修改HTML：使用`innerHTML`来更改元素的内部HTML。

```jsjavascript

title.innerHTML = "<span>Text with HTML</span>";

```

修改属性：使用`setAttribute`来更改元素的属性。

```jsjavascript

titulo.setAttribute("class", "novo-titulo");

```

修改样式：通过`style`属性直接修改元素的样式。

```jsjavascript

titulo.style.color = "blue";

titulo.style.fontSize = "24px";

```

添加和删除类：使用`classList`来操作元素的类。

```jsjavascript

title.classList.add("featured");

title.classList.remove("featured");

```

创建和删除元素：您可以创建新元素并将其添加到DOM中，也可以删除现有元素。

创建元素：使用`createElement`来创建新元素，使用`appendChild`或`insertBefore`将它们添加到DOM中。

```jsjavascript

const novoParagrafo = document.createElement("p");

novoParagrafo.innerText = "This is a new paragraph.";

document.body.appendChild(novoParagrafo);

```

删除元素：使用`removeChild`删除元素。

```jsjavascript

const elementoARemover = document.getElementById("para-remover");

elementoARemover.parentNode.removeChild(elementoARemover);

```

事件与事件处理

事件是在浏览器中发生的动作或事件，可以使用JavaScript捕获和处理。事件处理对于在网页上创建交互性至关重要。

添加事件：使用`addEventListener`向元素添加事件。

```jsjavascript

const botao = document.getElementById("meuBotao");

botao.addEventListener("click", function() {

alert("Button clicked!");

});

```

事件类型：可以捕获几种类型的事件，例如点击、鼠标移动、按键等。

```jsjavascript

botao.addEventListener("mouseover", function() {

botao.style.backgroundColor = "green";

});

botao.addEventListener("mouseout", function() {

botao.style.backgroundColor = "";

});

```

键盘事件：捕获键盘事件以添加功能，例如键盘快捷键。

```jsjavascript

document.addEventListener("keydown", function(event) {

if (event.key === "Enter") {

alert("Enter pressed");

}

});

```

阻止默认行为：使用`preventDefault`来防止事件的默认行为。

```jsjavascript

const link = document.getElementById("meuLink");

link.addEventListener("click", function(event) {

event.preventDefault();

alert("Link clicked but not browsed");

});

```

事件传播：JavaScript中的事件通过DOM以两种方式传播：捕获和冒泡。使用`stopPropagation`来停止事件的传播。

```jsjavascript

const pai = document.getElementById("pai");

const child = document.getElementById("child");

pai.addEventListener("click", function() {

alert("Parent clicked");

});

filho.addEventListener("click", function(event) {

event.stopPropagation();

alert("Son clicked");

});

```

事件委托：将事件委托给父元素，以捕获其子元素的事件。这对于动态元素非常有用。

```jsjavascript

const lista = document.getElementById("lista");

lista.addEventListener("click", function(event) {

if (event.target && event.target.nodeName === "LI") {

alert("List item clicked: " + event.target.innerText);

}

});

```

虚拟DOM简介

`Virtual DOM`是现代库和框架（如`React`）中的一个核心概念。它允许你高效地更新用户界面，同时最小化对实际DOM的直接操作。

`Virtual DOM`的工作原理：`Virtual DOM`是对真实DOM的内存表示。当应用程序状态发生变化时，会创建一个新的`Virtual DOM`树，并与之前的树进行比较。然后以优化的方式将差异应用于真实的DOM。

`Virtual DOM`的好处：

1\. 性能：最小化对DOM的直接操作，这在性能上是代价高昂的。

2\. 简化：抽象了DOM更新的复杂性，使代码编写变得更简单。

3\. 一致性：确保用户界面状态以可预测的方式维护。

示例与`React`：

```jsjavascript

import React from 'react';

import ReactDOM from 'react-dom';

class App extends React.Component {

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

ReactDOM.render(<App />, document.getElementById('root'));

```

在这个例子中，`React`使用`Virtual DOM`来优化计数器更新。每次点击按钮时，状态发生变化，这导致创建一个新的`Virtual DOM`。然后，`React`有效地将必要的更改应用于实际的DOM。

我们探索了DOM操作、事件捕获和处理，以及对`Virtual DOM`的介绍。这些技能是创建交互式和高效网页应用的基础。通过掌握这些技术，你将能够构建响应灵活、直观的用户界面。随着我们继续前进，这些工具将为更高级和动态的`JavaScript`应用打下基础。保持好奇和参与，你将能够很好地应对现代网页开发中出现的挑战和机遇。
