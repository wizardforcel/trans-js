第六章

# 编写文档对象模型代码

本章内容

![Bullet](images/check.png) 理解对象

![Bullet](images/check.png) 操作对象属性和方法

![Bullet](images/check.png) 深入探索文档对象模型

![Bullet](images/check.png) 理解事件

在过去几章中我讲了很多 JavaScript，但从某种意义上说，这些内容只是编程的开胃小菜。现在是时候开始正餐了：编写文档对象模型代码。

在本章中，你将探索文档对象模型的迷人世界。你将学习许多强大的编码技巧，使你能够让网页执行几乎任何你想要的操作。你也会了解到，这是网页编码变得有趣并且可能有点上瘾（我保证是好的一种上瘾）的地方。## 熟悉对象

要编写真正有用的脚本，你必须做的是 JavaScript 从一开始就设计的事情：操作它所显示的网页。这就是 JavaScript 的全部内容，这种操作可以以许多不同的形式出现：

+   向 `element` 添加文本和 HTML 属性。

+   修改类或其他选择器的 CSS `property`。

+   将一些数据存储在浏览器的内部 `storage` 中。

+   在提交 `form` 数据之前进行验证。

该列表中的粗体项是你可以操作的“事物”示例，它们之所以特殊，只因为它们是可编程的。在 JavaScript 术语中，这些“可编程的事物”被称为 `objects`。

你可以通过以下三种方式之一来操作 JavaScript 中的对象：

+   你可以读取并修改对象的 `properties`。

+   你可以通过激活与 `object` 相关的 `method` 来使对象执行任务。

+   你可以定义一个过程，当某个特定的 `event` 发生时，该过程会在 `object` 上运行。

### 操作对象属性

你可以通过以下通用表达式中的语法来引用一个属性：

`*object*.*property*`

+   `object`：具有该属性的对象

+   `property`：你要操作的属性名称

例如，考虑以下表达式：

`document.location`

该表达式指的是 `document` 对象的 `location` 属性，它保存当前在浏览器窗口中显示的文档地址。（在对话中，你可以将这个表达式读作“document dot location”。）以下代码展示了一个简单的一行脚本，它将在控制台中显示这个属性，如[图 6-1](#c06-fig-0001)所示。

`console.log(document.location);`

![脚本快照显示 `document.location` 属性在控制台消息中的输出。](images/9781394263219-fg0601.png)

[图 6-1:](#rc06-fig-0001) 该脚本在控制台消息中显示`document.location`属性。

因为属性始终包含一个值，所以你可以在几乎任何类型的JavaScript语句中使用属性表达式，并将其作为操作数使用。例如，以下语句将`document.location`属性的当前值赋给名为`currentUrl`的变量：

`const currentUrl = document.location;`

类似地，以下语句将`document.location`作为字符串表达式的一部分：

`const message = "当前地址是 " + document.location + "。";`

一些属性是`“只读”`，这意味着你的代码只能读取当前的值，不能更改它。然而，许多属性是`“读/写”`，意味着你也可以更改它们的值。要更改属性的值，请使用以下通用语法：

`object.property = value`

以下是各部分的解释：

+   `object`：包含该属性的对象

+   `property`：你想要更改的属性名称

+   `value`：一个字面值（如字符串或数字）或一个返回你想要设置的属性值的表达式

这是一个示例：

`const newAddress = prompt("请输入你想要访问的网址："); document.location = newAddress;`

这个脚本会提示用户输入一个网页地址，并将结果存储在`newAddress`变量中。然后，这个值被用来更改`document.location`属性，在本例中告诉浏览器打开指定的地址。

要运行一个方法，从最简单的情况开始，即一个不需要任何参数的方法：

`object.method()`

以下是各部分的解释：

+   `object`：包含你想要操作的方法的对象

+   `method`：你想要执行的方法的名称

例如，考虑以下语句：

`history.back();`

这将运行`history`对象的`back()`方法，该方法告诉浏览器返回到之前访问的页面。

如果方法需要参数，你可以使用以下通用语法：

`object.method(argument1, argument2, …)`

例如，考虑`confirm()`方法，在以下语句中使用，它接受一个参数——一个字符串，用于指定显示给用户的文本：

`confirm("你想要返回吗？")`

最后，与属性一样，如果方法返回一个值，你可以将该值赋给一个变量（如我在前面示例中使用的`confirm()`方法），或者将方法嵌入到表达式中。

这是一个简单网页的源代码：

`<html lang="en"> <head> <title>So Many Kale Recipes</title> </head> <body> <header> <h1>Above and Beyond the Kale of Duty</h1> </header> <main> <p> 你喜欢用<a href="kale.html">甘蓝</a>做饭吗？ </p> </main> </body> </html>`

检查此代码的一种方式是从层次结构的角度进行。这意味着`html`元素在某种意义上是最上层的元素，因为每个其他元素都包含在其中。下一层级包含`head`和`body`元素。`head`元素包含一个`title`元素，`title`元素包含文本`So Many Kale Recipes`。类似地，`body`元素包含一个`header`元素和一个`main`元素。

层次结构通常在视觉形式上更易于理解，因此[图 6-2](#c06-fig-0002)将页面元素以层次结构方式呈现。

![网页代码的流程图。它包括文档、元素、文本和属性。](images/9781394263219-fg0602.png)

[图 6-2:](#rc06-fig-0002) 网页代码的层次结构。

![记住](images/remember.png) 当谈到对象层次结构时，如果对象`P`包含对象`C`，则对象`P`被称为对象`C`的`parent`，而对象`C`被称为对象`P`的`child`。在[图 6-2](#c06-fig-0002)中，箭头表示父子关系。此外，同一层级上的元素——例如`header`和`main`元素——被称为`siblings`。

您需要考虑几个关键点：

+   [图 6-2](#c06-fig-0002)中的每个框表示一个对象。

+   [图 6-2](#c06-fig-0002)中的每个对象都是三种类型之一：元素、文本或属性。

+   [图 6-2](#c06-fig-0002)中的每个对象，无论其类型如何，都被称为`node`。

+   整个页面由`document`对象表示。

因此，这种层次化的对象表示法被称为文档对象模型，通常称为DOM。DOM使您的JavaScript代码能够访问HTML文档的完整结构。## 在您的代码中指定元素

元素代表文档中的标签，因此您将在代码中不断使用它们。本节展示了几种引用一个或多个元素的方法。

### 通过id指定元素

如果您希望在脚本中操作特定元素，可以通过首先使用`id`属性为其分配一个标识符来直接引用该元素：

`<div id="kale-quotations">`

完成后，您可以通过使用`document`对象的`getElementById()`方法在代码中引用该元素：

`document.getElementById(*id*)`

***注意：***`id`*是一个字符串，表示您想要操作的元素的`id`属性。

例如，以下语句返回对前一个`<div>`标签的引用（该标签的`id="kale-quotations"`）：

`document.getElementById("kale-quotations")`

![警告](images/warning.png) 当您编写`document`对象的代码时，不要将`<script>`标签放在网页的`head`部分（即`<head>`和`</head>`标签之间）。如果将代码放在那里，浏览器会在有机会创建`document`对象之前运行代码，这将导致代码失败。因此，请将`<script>`标签放在网页的底部，在`</body>`标签之前。 ### 通过标签名指定元素

除了操作单个元素，您还可以操作元素的集合。一个这样的集合是页面中所有使用相同标签名的元素。例如，您可以引用所有的`<a>`标签或所有的`<div>`标签。

返回具有相同标签的元素集合的机制是`getElementsByTagName()`方法：

`document.getElementsByTagName("tag")`

`注意：` `tag` 是一个字符串，表示您希望操作的标签所使用的 HTML 名称。

此方法返回一个类数组集合，其中包含文档中所有使用指定标签的元素。（有关数组的工作原理，请参考[第7章](c07.xhtml)。另外，请查看本章稍后的部分“[操作元素集合](#c06-sec-0011)”）。例如，要返回一个包含当前页面中所有`div`元素的集合，您可以使用以下语句：

`const divs = document.getElementsByTagName("div");`  ### 通过类名指定元素

另一个您可以操作的集合是页面中所有使用相同类名的元素集合。返回所有共享特定类名的元素的JavaScript工具是`getElementsByClassName()`方法：

`document.getElementsByClassName("class")`

`注意：` `class` 是一个字符串，表示您希望操作的元素所使用的类名。

此方法返回一个类数组集合，其中包含文档中所有使用指定类名的元素。集合的顺序与元素在文档中出现的顺序相同。以下是一个示例：

`const keywords = document.getElementsByClassName("keyword");`  ### 通过选择器指定元素

你在 CSS 中使用的相同选择器和组合器，也可以在 JavaScript 代码中使用，通过 `document` 对象的 `querySelector()` 和 `querySelectorAll()` 方法来引用页面元素：

`document.querySelector("selector") document.querySelectorAll("selector")`

`注意:` `selector` 是一个字符串，表示你想要操作的元素或元素组的选择器或组合器。

这两种方法的区别在于，`querySelectorAll()` 返回一个集合，包含所有匹配选择器的元素，而 `querySelector()` 只返回第一个匹配的元素。

例如，以下语句返回所有作为 `article` 元素的直接子元素的 `section` 元素集合：

`const articles = document.querySelectorAll("article > section");`  ### 处理元素集合

`getElementsByTagName()`, `getElementsByClassName()`, 和 `querySelectorAll()` 方法分别返回一个类似数组的集合，包含文档中使用指定标签、类或选择器的所有元素。集合的顺序与元素在文档中出现的顺序相同。比如，考虑以下 HTML 代码：

`<div id="div1"> 当然，这是 div 1。 </div> <div id="div2"> 好吧，<em>这是</em> div 2！ </div> <div id="div3"> 忽略那些家伙。欢迎来到 div 3！ </div>`

现在考虑以下语句：

`divs = document.getElementsByTagName("div");`

在结果集合中，第一个项目（``divs[0]``）将是 ``<div>`` 元素，其 ``id`` 等于 ``div1``；第二个项目（``divs[1]``）将是 ``<div>`` 元素，其 ``id`` 等于 ``div2``；第三个项目（``divs[2]``）将是 ``<div>`` 元素，其 ``id`` 等于 ``div3``。

你也可以直接使用它们的 ``id`` 值来引用元素。例如，以下语句是等效的：

`const firstDiv = divs[0]; const firstDiv = divs.div1;`

要了解集合中有多少个项目，请使用 ``length`` 属性：

`const totalDivs = divs.length;`

要对集合中的每个项目执行一个或多个操作，可以使用 ``for…of`` 循环逐个运行集合中的项目。在 JavaScript 领域，这被称为 *迭代* 集合。以下是要使用的语法：

`for (const item of collection) { statements }`

这是各部分的含义：

+   ``item``: 一个在集合中保存项目的变量。第一次循环时，``item`` 被设置为集合中的第一个元素；第二次循环时，``item`` 被设置为第二个元素；以此类推。

+   ``collection``: 你想要迭代的元素集合。

+   ``statements``: 你希望用来操作（或查看，或其他）``item`` 的 JavaScript 代码。

例如，这里有一些代码，可以迭代前面的 ``div`` 元素，并在控制台中显示每个项目的 ``id`` 值（请参阅 [第 9 章](c09.xhtml) 了解控制台的详细信息），如 [图 6-3](#c06-fig-0003) 所示：

`divs = document.getElementsByTagName("div"); for (const d of divs) { console.log(d.id); }`

![迭代 div 元素的脚本输出截图。](images/9781394263219-fg0603.png)

[图 6-3:](#rc06-fig-0003) 迭代 ``div`` 元素的脚本输出。

![警告](images/warning.png) ``for…of`` 循环是 ECMAScript 2015 (ES6) 的新增内容。如果需要支持古老的浏览器，比如 Internet Explorer 11，可以使用常规的 ``for`` 循环：

`for (var i = 0; i < collection.length; i += 1) { statements // 使用 collection[i] 来引用每个项目 }`  ## 用代码游览 DOM

在 JavaScript 代码中，一个常见的任务是操作页面中某个元素的子元素、父元素或兄弟元素。这被称为 `遍历 DOM`，因为你使用这些技术在 DOM 层级中上下移动。

在接下来的章节中，我使用以下 HTML 代码作为每个示例技术：

`<html lang="en"> <head> <title>So Many Kale Recipes</title> </head> <body> <header id="page-banner"> <h1>Above and Beyond the Kale of Duty</h1> </header> <main id="page-content"> <p> 你喜欢用 <a href="kale.html">羽衣甘蓝</a> 做菜吗？ </p> </main> </body> </html>`

### 获取父元素的子元素

当你正在处理特定元素时，通常会希望对该元素的子元素执行一个或多个操作。每个父元素都提供了几个属性，允许你处理它的所有或部分子节点：

+   所有子节点

+   第一个子节点

+   最后一个子节点

#### 获取所有子节点

要返回父元素的所有子元素集合，可以使用 `children` 属性：

`parent.children`

**注意：** `parent` 是父元素。

例如，以下语句将 `body` 元素的所有子元素节点存储在一个变量中：

`const bodyChildElements = document.body.children;`

结果是一个 `HTMLCollection` 对象，这是一个类数组的元素节点集合。如果你在控制台使用（参考 [第 9 章](c09.xhtml)）来显示 `bodyChildElements` 的值，你会得到 [图 6-4](#c06-fig-0004) 中显示的输出。

![`bodyChildElements` 变量在控制台中显示的值的快照。](images/9781394263219-fg0604.png)

[图 6-4:] `bodyChildElements` 变量在控制台中显示的值。

这里是输出结果：

`HTMLCollection { 0: header, 1: main, length: 2 }`

数字 `0` 和 `1` 是每个子节点的索引号。例如，你可以使用 `bodyChildElements[0]` 来引用集合中的第一个元素，在这个示例中是 `header` 元素。  #### 获取第一个子节点

如果你使用父元素的 `childNodes` 或 `children` 属性来返回父元素的子节点，正如我在上一节中所描述的那样，可以通过在集合的变量名后加上 `[0]` 来引用结果集合中的第一个项。例如：

`bodyChildren[0] bodyChildElements[0]`

然而，DOM 提供了一种更直接的方法来获取第一个子节点：

`parent.firstChild`

**注意：** `parent` 是父元素。

例如，假设你想处理本节开头 HTML 示例中 `main` 元素的第一个子节点。这里有一些代码可以完成这个任务：

`const content = document.getElementById("page-content"); const firstContentChildNode = content.firstChild;`

在此示例中，结果节点是一个文本节点（`<main>` 和 `<p>` 标签之间的空白）。如果你想要第一个子元素节点，请使用 `firstElementChild` 属性：

`parent.firstElementChild`

`Note:` `parent` 是父元素。

要获取本节开头代码中的 `main` 元素的第一个子元素节点，可以这样做：

`const content = document.getElementById("page-content"); const firstContentChildElement = content.firstElementChild;`

在此示例中，这段代码返回 `p` 元素。#### 获取最后一个子节点

如果你的代码需要处理最后一个子节点，请使用父元素的 `lastChild` 属性：

`parent.lastChild`

`Note:` `parent` 是父元素。

例如，假设你想处理本节开头 HTML 示例中的 `p` 元素的最后一个子节点。以下是一些可以完成此工作的代码：

`const para = document.querySelector("main > p"); const lastParaChildNode = para.lastChild;`

在此示例中，结果节点是表示问号（`?`）的文本节点，以及`</p>`标签的空白。如果你想要最后一个子元素节点，请使用`lastElementChild`属性：

`parent.lastElementChild`

`Note:` `parent` 是父元素。

要获取本节开头代码中`p`元素的最后一个子元素节点，你可以这样做：

`const para = document.querySelector("main > p"); const lastParaChildElement = para.lastElementChild;`

在示例中，这段代码返回`a`元素。### 获取子元素的父元素

如果你的代码需要处理子元素的父元素，请使用子元素的`parentNode`属性：

`child.parentNode`

`Note:` `child` 是子元素。

例如，假设你想处理本节开头HTML示例中的`h1`元素的父元素。以下是一些可以完成此工作的代码：

`const childElement = document.querySelector("h1"); const parentElement = childElement.parentNode;` ### 获取元素的兄弟节点

父元素的子节点在DOM中按HTML代码出现的顺序出现，这意味着兄弟节点也按它们在HTML中出现的顺序出现。因此，对于给定的子元素，有两种兄弟节点可能性：

+   **前一个兄弟节点：** 这是在DOM中紧接着你正在处理的子元素之前出现的兄弟节点。如果子元素是第一个兄弟节点，则没有前一个兄弟节点。

+   **下一个兄弟节点：** 这是在DOM中紧接着你正在处理的子元素之后出现的兄弟节点。如果子元素是最后一个兄弟节点，则没有下一个兄弟节点。

#### 获取前一个兄弟节点

要返回特定元素的前一个兄弟节点，请使用`previousElementSibling`属性：

`element.previousElementSibling`

注意：`element`是您正在处理的元素。

例如，以下语句将`main`元素的前一个兄弟元素存储在一个变量中：

`const currElement = document.querySelector("main"); const prevSib = currElement.previousElementSibling;`  #### 获取下一个兄弟元素

要返回特定元素的下一个兄弟元素，使用`nextElementSibling`属性：

`element.nextElementSibling`

注意：`element`是您正在处理的元素。

例如，以下语句将`header`元素的下一个兄弟元素存储在一个变量中：

`const currElement = document.querySelector("header"); const nextSib = currElement.nextElementSibling;`  ## 添加、修改和删除元素

在获得对一个或多个元素的引用后，您可以使用代码以各种方式操作这些元素，如接下来几节所示。

### 将元素添加到页面

Web 开发中最常见的任务之一是在页面上动态添加元素。当您添加元素时，始终指定将要添加的父元素，然后决定是将新元素添加到父元素子元素集合的末尾还是开头。

要将元素添加到页面，您需要遵循三个步骤：

1.  创建要添加的元素类型的对象。

1.  将步骤 1 的新对象作为现有元素的子元素添加。

1.  插入一些文本和标签到步骤 1 的新对象中。

#### 步骤 1：创建元素

对于步骤 1，您使用`document`对象的`createElement()`方法：

`document.createElement(elementName)`

注意：`elementName`是一个包含您要创建的元素类型的 HTML 元素名称的字符串。

此方法创建元素并返回它，这意味着您可以将新元素存储在一个变量中。以下是一个示例：

`const newArticle = createElement("article");`  #### 步骤 2：将新元素作为子元素添加

创建元素后，步骤 2 是将其添加到现有父元素中。您有四个选择：

+   将新元素附加到父元素的子元素集合的末尾：使用`append()`方法：`parent.append(child)`

    下面是`append()`方法的组成部分：

    +   `parent`：指向将要附加新元素的父元素的引用。

    +   `child`：指向您要附加的子元素的引用。请注意，您可以通过用逗号分隔每个元素来同时附加多个元素。`child`参数也可以是文本字符串。

+   将新元素放在父元素的子元素集合的开头：使用`prepend()`方法：`parent.prepend(child)`

    下面是`prepend()`方法的组成部分：

    +   `parent`：指向将要预先添加新元素的父元素的引用。

    +   ``child``: A reference to the child element you’re prepending. Note that you can prepend multiple elements at the same time by separating each element with a comma. The ``child`` parameter can also be a text string.

+   **将新元素插入到父元素的现有子元素之后：** 使用`after()`方法：``child``.after(``sibling``)

    这里是`after()`方法的组成部分：

    +   ``child``: A reference to the child element after which the new element will be inserted.

    +   ``sibling``: A reference to the new element you’re inserting. Note that you can insert multiple elements at the same time by separating each element with a comma. The ``sibling`` parameter can also be a text string.

+   **将新元素插入到父元素的现有子元素之前：** 使用`before()`方法：``child``.before(``sibling``)

    下面是`before()`方法的各部分：

    +   ``child``: 新元素将被插入到此子元素之前。

    +   ``sibling``: 新插入元素的参考对象。注意，你可以通过逗号分隔每个元素同时插入多个元素。``sibling``参数也可以是一个文本字符串。

这里有一个示例，创建一个新的`article`元素，并将其添加到`main`元素中：

`const newArticle = document.createElement("article"); document.querySelector("main").append(newArticle);`

这里有一个示例，创建一个新的`nav`元素并将其插入到`main`元素之前：

`const newNav = document.createElement("nav"); document.querySelector("main").prepend(newNav);` #### 步骤3：向新元素添加文本和标签

在创建并添加元素到父元素之后，最后一步是使用`innerHTML`属性添加文本和标签：

``element``.innerHTML = ``text``

下面是各部分的说明：

+   ``element``: 一个引用，指向你希望添加文本和标签的新元素。

+   ``text``: 包含你要插入的文本和HTML标签的字符串。

![警告](images/warning.png) 无论你为`innerHTML`属性赋予什么值，它都会完全覆盖元素现有的文本和标签，因此在使用`innerHTML`时要小心。查看下一个部分，了解如何插入文本和标签，而不是覆盖它们。

在这个示例中，代码创建一个新的`nav`元素，将其插入到`main`元素之前，然后添加一个标题：

`const newNav = document.createElement("nav"); document.querySelector("main").prepend(newNav); newNav.innerHTML = "<h2>Navigation</h2>";` ### 向元素中插入文本或HTML

通常情况下，你希望保留元素现有的标签和文本，同时插入新的标签和文本。每个元素提供了几种方法，让你能够做到这一点：

+   **仅将文本插入到元素中：** 使用`insertAdjacentText()`方法：``element``.insertAdjacentText(``location``, ``text``)

    下面是各部分的说明：

    +   ``element``: 一个引用，指向你希望插入新文本的元素。

    +   `location`: 一个字符串，指定你希望文本插入的位置。稍后我会简要概述你的选择。

    +   `text`: 一个包含你希望插入的文本的字符串。

+   **要将标签和文本插入到元素中：** 使用 `insertAdjacentHTML()` 方法：`element.insertAdjacentHTML(location, data)`

    各部分的内容如下：

    +   `element`: 一个引用，指向你希望插入新标签和文本的元素。

    +   `location`: 一个字符串，指定你希望插入标签和文本的位置。稍后我会简要概述你的选择。

    +   `data`: 一个包含你希望插入的标签和文本的字符串。

对于这两种方法，你可以使用以下字符串之一作为 `location` 参数：

+   `"beforebegin"`: 在元素外部并紧接着元素之前插入数据。

+   `"afterbegin"`: 在元素内部，紧接着元素的第一个子元素之前插入数据。

+   `"beforeend"`: 在元素内部，紧接着元素的最后一个子元素之后插入数据。

+   `"afterend"`：将数据插入到元素外部并紧接元素之后

例如，假设你的文档中有以下元素：

`<h2 id="nav-heading">导航</h2>`

如果你想将标题更改为 `Main Navigation`，以下代码将完成该任务：

```const navHeading = document.getElementById("nav-heading"); navHeading.insertAdjacentText("afterbegin", "Main ");```  ### 移除元素

如果你不再需要页面上的某个元素，可以使用该元素的 `remove()` 方法将其从 DOM 中删除：

`element.remove()`

例如，以下语句将具有 `id` 值为 `temp-div` 的元素从页面中移除：

```document.getElementById("temp-div").remove();``` ## 使用代码修改 CSS

尽管你在静态样式表（`.css`）文件中指定了 CSS 规则，但这并不意味着规则本身必须是静态的。通过 JavaScript，你可以以多种方式修改元素的 CSS。

### 更改元素的样式

大多数元素都有一个 `style` 属性，可以让你获取和修改标签的样式。它的工作原理是：`style` 属性实际上返回一个 `style` 对象，该对象具有每个 CSS 属性的属性。在引用这些样式属性时，你需要牢记两件事：

+   对于单词 CSS 属性（如 `color` 和 `visibility`），请使用全小写字母。

+   对于多个单词的 CSS 属性，去掉连字符，并对第二个单词的首字母及后续单词的首字母使用大写。例如，`font-size` 和 `border-left-width` CSS 属性变为 `fontSize` 和 `borderLeftWidth` 样式对象属性。

这里有一个例子：

```const pageTitle = document.querySelector("h1"); pageTitle.style.fontSize = "64px"; pageTitle.style.color = "maroon"; pageTitle.style.textAlign = "center"; pageTitle.style.border = "1px solid black";```

这段代码获取页面上第一个 `<h1>` 元素的引用。通过这个引用，代码使用 `style` 对象来设置标题的四个样式属性：`fontSize`、`color`、`text-align` 和 `border`。 ### 向元素添加类

如果你在 CSS 中定义了一个类规则，你可以通过向元素的标签添加 `class` 属性，并将 `class` 属性的值设置为类规则的名称来应用该规则。

首先，你可以通过使用 `classList` 属性获取元素的类列表：

`element.classList`

-   `element` 是你正在处理的元素。

返回的类列表是一个类似数组的对象，它包含一个 `add()` 方法，你可以使用该方法将新类添加到元素现有的类中：

`element.classList.add(class)`

这里是各部分的解释：

+   `element`：你正在处理的元素。

+   `class`：表示你要添加到 `element` 的类的名称。你可以通过逗号分隔来添加多个类。

这里有一个例子，[图 6-5](#c06-fig-0005) 显示了结果。

![代码快照使用 add() 方法将名为 my-class 的类添加到 <div> 标签中。](images/9781394263219-fg0605.png)

[图 6-5：](#rc06-fig-0005) 这段代码使用 `add()` 方法将名为 `my-class` 的类添加到 `<div>` 标签中。

CSS:

`.my-class { display: flex; justify-content: center; align-items: center; border: 6px dotted black; font-family: Verdana, serif; font-size: 2rem; background-color: lightgray; }`

HTML:

`<div id="my-div"> 你好，世界！ </div>`

JavaScript:

`document.getElementById('my-div').classList.add('my-class');`

![记住](images/remember.png) 如果元素中没有 `class` 属性，`addClass()` 方法会将其插入到标签中。所以在之前的示例中，代码执行后，`<div>` 标签现在会变成这样：

`<div id="my-div" class="my-class">`

#### 移除一个类

要从元素的 `class` 属性中移除一个类，可以使用 `classList` 对象的 `remove()` 方法：

`element.classList.remove(class)`

以下是各部分的说明：

+   `element`：你正在操作的元素。

+   `class`：表示要从 `element` 中移除的类名的字符串。你可以通过用逗号分隔每个类名来移除多个类。

以下是一个示例：

`document.getElementById('my-div').classList.remove('my-class');` #### 切换类

`classList` 对象提供了 `toggle()` 方法，用于在元素上切换类。这意味着，它会检查元素是否具有指定的类；如果该类存在，JavaScript 会移除它；如果该类不存在，JavaScript 会添加它。非常棒！以下是语法：

`element.classList.toggle(class)`

以下是各部分的说明：

+   `element`：你正在操作的元素

+   `class`：表示要切换的 `element` 的类名的字符串。

以下是一个示例：

`document.getElementById('my-div').classList.toggle('my-class');` ## 使用代码调整 HTML 属性

DOM 的一个关键特性是页面上的每个标签都会变成一个元素对象。你可能会想，这些元素对象有属性吗？是的，它们有很多属性。特别是，如果标签包含一个或多个属性，这些属性会成为元素对象的属性。

例如，考虑以下 `<img>` 标签：

`<img id="header-image" src="mangosteen.png" alt="Drawing of a mangosteen">`

这个标签有三个属性：``id``、``src`` 和 ``alt``。在 DOM 对 `<img>` 标签的表示中，这些属性变成了 ``img`` 元素对象的属性。以下是一些引用 ``img`` 元素的 JavaScript 代码：

`const headerImage = document.getElementById("header-image");`

`headerImage` 变量保存了 ``img`` 元素对象，因此你的代码现在可以通过以下属性引用来访问 ``img`` 元素的属性值：

``headerImage.id headerImage.src headerImage.alt``

然而，DOM 不会为自定义属性或程序matically 添加的属性创建属性。幸运的是，每个元素对象还提供了可以读取任何属性的方法，以及添加、修改或移除元素属性的方法。接下来的几节会详细介绍。

### 读取属性值

如果你想读取元素的当前属性值，可以使用元素对象的 ``getAttribute()`` 方法：

``element``.getAttribute(`attribute`)

以下是各部分的说明：

+   ``element``：你要操作的元素

+   ``attribute``：你要读取的属性名

这里有一个示例，获取具有``id``值为``header-image``的元素的``src``属性：

`const headerImage = document.getElementById("header-image"); const srcHeaderImage = headerImage.getAttribute("src");` ### 设置属性值

要在元素上设置属性值，可以使用元素对象的``setAttribute()``方法：

``element``.setAttribute(`attribute`, `value`);

以下是各个部分的解释：

+   ``element``：您想要操作的元素

+   ``attribute``：您要设置的属性名称

+   ``value``：您想要分配给``attribute``的字符串值

如果属性已存在，``setAttribute``会覆盖该属性的当前值；如果属性不存在，``setAttribute``会将其添加到元素中。

这是一个示例，设置``id``值为``header-image``的元素的``alt``属性：

`const headerImage = document.getElementById("header-image"); headerImage.setAttribute("alt", "菠萝蜜的版画");` ### 删除属性

要从元素中删除属性，可以使用元素对象的``removeAttribute()``方法：

``element``.removeAttribute(`attribute`);

以下是各个部分的解释：

+   ``element``：您想要操作的元素

+   `attribute`：一个字符串，指定您要从元素中删除的属性名称

这是一个示例：

`const headerImage = document.getElementById("header-image"); headerImage.removeAttribute("id");`  ## 监听页面事件

在网页开发中，`event`是响应某些外部刺激而发生的操作。常见的外部刺激之一是用户与网页的交互。以下是一些示例：

+   浏览页面或重新加载页面

+   点击按钮

+   按下键盘

+   滚动页面

为什么网页不会自动响应事件？为什么它们只是静静地待在那里？因为网页默认是`静态`的，这意味着它们忽略了周围发生的所有事件。作为网页开发者，您的工作就是通过使网页“监听”特定的事件来改变这种行为。您可以通过设置名为`事件处理器`的特殊代码块来实现这一点。一个事件处理器由两部分组成：

+   `事件监听器：` 指示网页浏览器监听（“监听”）特定元素上发生的特定事件。

+   `回调函数：` 网页浏览器在检测到事件发生时执行的代码。

通过设置事件处理器，您可以配置代码以监听和响应事件，使用元素对象的`addEventListener()`方法。语法如下：

`*element*.addEventListener(*event*, *callback*);`

以下是各个部分的解释：

+   `element`：需要监控事件的网页元素。该事件被认为是`绑定`到该元素的。

+   `event`: 一个字符串，指定你希望浏览器监听的事件名称。对于我在上一节中提到的主要事件，使用以下之一，并用引号括起来：`DOMContentLoaded`、`click`、`dblclick`、`mouseover`、`keypress`、`focus`、`blur`、`change`、`submit`、`scroll` 或 `resize`。

+   `callback`: 当事件发生时，JavaScript执行的回调函数。回调可以是一个匿名函数或一个命名函数的引用。

以下是一个示例：

HTML：

`<div id="my-div"></div> <button id="my-button">点击添加上面的文本</button>`

JavaScript：

`const myButton = document.getElementById('my-button'); myButton.addEventListener('click', function() { const myDiv = document.getElementById('my-div'); myDiv.innerHTML = '<h1>Hello Click World!</h1>'; });`

HTML设置了一个空的`div`元素和一个`button`元素。JavaScript代码将一个`click`事件监听器附加到按钮上，回调函数将HTML字符串`<h1>Hello Click World!</h1>`添加到`div`中。[图6-6](#c06-fig-0006)展示了按钮点击后的页面效果。

![点击事件回调函数将一些HTML和文本添加到div元素中的快照。消息内容为“Hello Click World”。](images/9781394263219-fg0606.png)

[图6-6:](#rc06-fig-0006) `click`事件的回调函数将一些HTML和文本添加到`div`元素中。

![提示](images/tip.png) 如果你希望在网页文档加载完成后运行某些代码，可以为`document`对象添加一个事件处理程序，监听`DOMContentLoaded`事件：

`document.addEventListener('DOMContentLoaded', function() { console.log('我们已加载完成！'); });`

当事件触发时，DOM会创建一个`Event`对象，其属性包含关于事件的信息，包括以下内容：

+   `target`: 事件发生的网页元素。例如，如果你为一个`div`元素设置了`click`事件处理程序，那么该`div`就是点击事件的目标。

+   `which`: 一个数字代码，指定在`keypress`事件中按下的键。

+   `pageX`: 鼠标指针距离浏览器内容区左边缘的距离（以像素为单位）当事件触发时。

+   `pageY`: 鼠标指针距离浏览器内容区顶部边缘的距离（以像素为单位）当事件触发时。

+   `metaKey`: 一个布尔值，如果用户在事件触发时按下了Windows键 (![Windows](images/windows.png)) 或 Mac Command键 (⌘  )，则该值为`true`。

+   `shiftKey`: 一个布尔值，如果用户在事件触发时按下了Shift键，则该值为`true`。

要访问这些属性，你需要在事件处理程序的回调函数中插入一个`Event`对象的名称作为参数：

`*element*.addEventListener(*event*, function(e) { *该代码在事件触发时运行* });`

***注意:*** `e` 是事件对象 `Event` 的名称，该对象由 DOM 在事件触发时生成。你可以使用任何你想要的名称，但大多数开发者使用 `e`（虽然 `evt` 和 `event` 也很常见）。

例如，在处理 `keypress` 事件时，你需要访问 `which` 属性来找出用户按下的键的代码。以下是一个示例页面，帮助你确定需要使用的代码值：

HTML:

`<div> 输入一个键： </div> <input id="key-input" type="text"> <div> 你按下的键的代码是： </div> <div id="key-output"> </div>`

JavaScript:

`const keyInput = document.getElementById('key-input'); keyInput.addEventListener('keypress', function(e) { const keyOutput = document.getElementById('key-output'); keyOutput.innerHTML = e.which; });`

HTML 设置了一个 `<input>` 标签来接收按键输入，并且设置了一个 `id="key-output"` 的 `<div>` 标签来显示输出。JavaScript 代码为 `input` 元素添加了一个 `keypress` 事件监听器，当事件触发时，回调函数将 `e.which` 写入到输出的 `div` 中。[图 6-7](#c06-fig-0007) 展示了页面的实际效果。

![Paulmcfederies 网页的快照，字段包括，输入一个键，一个。你按下的键的代码是：97。](images/9781394263219-fg0607.png)

[图 6-7:](#rc06-fig-0007) `keypress` 事件的回调函数使用 `e.which` 将按下的键的数字代码写入到 `div` 元素中。
