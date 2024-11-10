© 作者，独家授权给 Springer Fachmedien Wiesbaden GmbH，Springer Nature 旗下，2024年 J. L. Zuckarelli《学习编程：Python 和 JavaScript》 [https://doi.org/10.1007/978-3-658-42912-6_32](https://doi.org/10.1007/978-3-658-42912-6_32)

# 32. 用户界面：如何输入和输出数据？

Joachim L. Zuckarelli^([1](#Aff2)  )(1)德国慕尼黑概述

JavaScript 是 Web 上使用的主要语言，这解释了为什么数据输入和输出通常涉及与托管 JavaScript 代码的网页交互。

JavaScript 提供了许多接收网页用户信息并修改网页以输出信息的可能性。与周围网页的交互之所以能够实现，是因为 JavaScript 允许通过网页的*文档对象模型*（*DOM*）访问其单个元素。但在我们转向使用 DOM 之前，让我们快速回顾一下我们已经经常使用的 JavaScript 控制台输出，以及如何处理对话框。

在本章中，您将学习以下内容：

+   如何在控制台中输出对象

+   如何使用模板字面量和字符串替换方便地构建输出字符串

+   如何通过对话框显示信息并请求用户决策

+   *文档对象模型*（*DOM*）是什么，以及它是如何结构化的

+   如何根据 DOM 选择和修改网页的单个元素

+   如何使用表单接收用户输入

## 32.1 JavaScript 输入和输出概述

使用 JavaScript 输出数据的最简单方式是输出到控制台。在上一章中，我们广泛使用了这种方式，主要因为控制台提供了交互性，在尝试新的语言概念时非常有用。输入指令后，立即显示结果。

然而，在编写实际的 JavaScript 应用程序时，通常不希望使用控制台——它是开发者工具，通常对网站浏览者是不可见的。相反，您希望 JavaScript 应用程序与网页交互，并在网页上输出信息供用户查看。

在本章中，我们将首先快速回顾已经熟悉的控制台输出，接着探讨如何通过*对话框*输出（和输入）数据。然后，我们将转向输入和输出的核心领域——与嵌入脚本的网页的交互。在此过程中，我们将看到如何通过所谓的*文档对象模型*（*DOM*）从 JavaScript 程序中修改网页的各个元素。特别是，我们将关注*表单*，它们对网站交互性非常有用，因为它们允许用户直接输入文本和其他信息。处理表单是 JavaScript 的一个重要应用领域。

与其他编程语言不同，我们不会在 JavaScript 中涉及文件操作，因为出于安全原因，JavaScript 通常无法访问本地计算机的文件系统。

我们将通过两个小示例应用程序来结束本章，一个是简单的计算器，另一个是颜色选择器，可以方便地生成常用于 HTML 中的十六进制颜色代码。

## 32.2 通过控制台输出

在上一章中，我们已经频繁使用了 **log()** 方法来快速方便地将数据输出到控制台。在本节中，我们将更详细地了解它，特别是 **console.log()** 如何用于输出由多个不同部分组成的内容。这里介绍的 **console.log()** 使用方法是可转移的，能在许多使用字符串的地方应用。

打印多个对象的列表

如果你想在一行中输出多个值/对象，只需将它们作为逗号分隔的列表传递给 **console.log()**：

**>** console.log('今天是: ', Date(), '. 一个介于 0 和 10 之间的随机数是: ',Math.round(Math.random()*10,0))今天是: Mon Oct 03 2022 13:24:53 GMT+0200 (中央欧洲夏令时)。一个介于 0 和 10 之间的随机数是: 4

**console.log()** 简单地将作为参数传递的对象一个接一个地输出，不加选择。不同对象的输出之间用空格隔开。

打印多个对象作为连接字符串

如果你想避免这个空白，你必须首先将对象组合成一个字符串，按需控制空白的出现，然后输出完整的字符串：

**>** output = '今天是: ' + Date().toString() + '. 一个介于 0 和 10 之间的随机数是: ' +Math.round(Math.random()*10,0).toString()**>** console.log(output)今天是: Mon Oct 03 2022 13:30:19 GMT+0200 (中央欧洲夏令时)。一个介于 0 和 10 之间的随机数是: 9

达到相同效果的另一种方法是使用 *模板字面量*。模板字面量是包含占位符的字符串。与常规字符串不同，它们用 *反引号*（**`**）括起来。在模板字面量中，可以插入占位符来表示变量或其他表达式的值。通配符的特点是以美元符号（**$**）开始，并将表示的表达式用大括号括起来，如以下示例所示：

**>** randomNumber = Math.round(Math.random()*10,0)**>** output = `一个介于 0 和 10 之间的随机数是:${ randomNumber}.`**>** console.log(output)一个介于 0 和 10 之间的随机数是: 6。

这样，你就不必费力地组合你的字符串，确保每个子字符串的引号设置正确，并且每个子字符串都用加号运算符连接。只需写一个长字符串，在其中将你想要表示的变量或其他表达式写为占位符。

重要提示：变量的值在模板字面量创建时就已经固定。之后对变量值的修改将不再反映在模板字面量中。以下示例说明了这一点：

**>** value = 2**>** output = `Current value: ${value}`**>** value = 3**>** console.log(output)Current value: 2

顺便提一下，模板字面量的一个非常实用的功能是，与常规字符串不同，它们可以跨越多行，如以下示例所示：

**>** twoLines = `First lineSecond line`**>** console.log(twoLines)First lineSecond line

在普通字符串中，我们需要使用转义序列 **\n** 来实现这一点：

**>** console.log('First line\nSecond line')First lineSecond line 使用字符串替换生成组合输出 另一种生成组合输出的方式是使用字符串替换，这在 **console.log()** 和其他 JavaScript 函数中都得到了支持。这同样适用于通配符。一个简单的例子说明了这个如何工作：**>** pi = 3.14159**>** console.log('The value of the number pi is: %f', pi)3.14159

占位符由百分号和格式化指令组成；**f** 指示输出将数字显示为浮动小数。占位符最终填充的内容取决于 **console.log()** 函数的进一步参数。在我们的示例中，字符串后的第一个参数是我们的变量 **pi**，因此它会用于字符串中找到的第一个占位符。如果字符串包含更多占位符，它们的替换内容将作为 **pi** 后面的进一步参数添加。

同样，值可以使用 **%s** 输出为字符串，或使用 **%d** 和 **%i** 输出为整数：

**>** console.log('The value of the number pi is: %', pi)3 生成警告和错误

到目前为止，我们一直使用 **console.log()** 向控制台输出信息。然而，你也可以输出警告和错误消息，这些消息会被高亮显示并带有适当的图标：

**>** console.warn('Nothing bad, just a warning')**>** console.error('Now a real error')你可以在◘ 图 [32.1](#Fig1)中查看这些输出的结果。![](../images/474412_1_En_32_Chapter/474412_1_En_32_Fig1_HTML.jpg)

一个警告和错误消息的截图。警告消息是未定义的控制台错误。错误消息是未定义的。

图 32.1

自生成的警告和错误消息

## 32.3 通过对话框进行输入输出

JavaScript 提供了使浏览器显示消息为小对话框的功能。借助 **alert(*****message*****)** 函数，你可以显著地向用户显示消息：

**>** alert('An important Message') 会打开一个对话框，如图◘ [32.2](#Fig2)所示。![](../images/474412_1_En_32_Chapter/474412_1_En_32_Fig2_HTML.jpg)

一个警告框的截图。消息是，这个页面显示了一个重要的信息。确认按钮在底部。

图 32.2

**alert()** 框在 Google Chrome 中

如果你想让用户确认某个操作，可以使用**confirm(*****message*****)**函数，它会显示一条消息，并提供“确定”和“取消”按钮，如◘ 图 [32.3](#Fig3) 所示的对话框。**confirm()**返回**true**（如果用户选择了“确定”）或者返回**false**（如果用户选择了“取消”）。![](../images/474412_1_En_32_Chapter/474412_1_En_32_Fig3_HTML.jpg)

一个确认对话框的截图。消息内容是：你真的想继续学习JavaScript吗？确认和取消按钮位于底部。

图 32.3

使用**confirm()**的Google Chrome中的确认对话框

**>** action = confirm('你真的想继续学习JavaScript吗？')**>** console.log(action)True

另一种接受用户输入的方法是使用**prompt(*****message*****)**函数。它会创建一个对话框，用户可以在其中输入内容，**prompt()**会将输入返回为字符串（即使用户输入的是数字！）

以下示例，使用了我们在前一节中介绍的模板字面量，应该是你很熟悉的。它是将摄氏度的温度值转换为开尔文，这个过程之前已经使用过几次：

celsius = prompt('请输入摄氏温度：');console.log(`${celsius} 摄氏度是 ${Number(celsius) + 273.15} 开尔文。`);**prompt()**生成的输入对话框如◘ 图 [32.4](#Fig4) 所示。![](../images/474412_1_En_32_Chapter/474412_1_En_32_Fig4_HTML.jpg)

一个提示输入对话框的截图。它有一个文本框，用于输入摄氏温度。确认和取消按钮位于底部。

图 32.4

**prompt()**输入对话框在Microsoft Edge中的表现

你还可以尝试这个示例，而不调用**Number()**构造函数。会发生什么？你能解释结果吗？如果不能，请返回几页，参见► Sect. [31.​3.​1](474412_1_En_31_Chapter.xhtml#Sec8)。

## 32.4 输出到HTML文档/网页

### 32.4.1 将HTML代码写入网页

现在让我们转向最重要的输出形式——修改嵌入JavaScript程序的网页。

从JavaScript修改网页的最简单方法是使用**document.write(*****html*****)**方法。它将作为参数传入的字符串***html***直接写入网页的当前位置，即脚本嵌入在网页中的地方。这个字符串可能包含文本以及HTML指令（标签），它会被插入到HTML页面的源代码中，就像它最初是由网页设计者写的那样。

为了说明这一点，假设有一个（非常简化的）网页，它的源代码如下所示：

**<!DOCTYPE html>****<html>****<head>****<title>**测试页面**</title>****<noscript>**请启用JavaScript！**</noscript>****</head>****<body>****<h1>**我们的测试页面**</h1>****<p** id="output"**></p>****<script** src="script.js"**></script>****</body>****<html>**

该网页的主体仅包含一个标题（**<h1>…</h1>**）、一个空的段落（**<p>…</p>**）和对脚本的引用。

嵌入网页中的JavaScript程序**script.js**如下所示：

**var** random = Math.round(Math.random()*100, 0);document.write(`<p>0到100之间的随机数：${random}。</p>`);

如你所见，我们在这里使用了来自►第[32.2节](#Sec2)的模板字面量，以简单地表示要写入网页的HTML字符串。当然，我们本可以写**document.write('<p>0到100之间的随机数：', random, '。</p>');**，这虽然有效，但代码略显杂乱。

现在，每次刷新浏览器中的网页显示时，JavaScript代码都会执行，每次都绘制一个新的随机数。我们的脚本通过**document.write()**写入网页后，浏览器中显示的网页如下所示：

**<!DOCTYPE html>**<**html>**<**head>**<**title>**测试页面**</title>**<**noscript>**请启用JavaScript！**</noscript>**</head>**<body>**<h1>**我们的测试页面**</h1>**<**p** id="output"**></p>**<p>**0到100之间的随机数：62。**</p>**</body>**</html>**

我们的脚本通过添加一个HTML元素来修改网页。这实际上会导致一个“新”的网页，然后在浏览器中显示。你可以在浏览器中查看该页面的源代码。

当然，你不总是希望在脚本的当前位置输出新的内容，但你可能想要更改网页上现有的元素。例如，我们可能想要更改页面的标题。但我们的脚本“离标题太远”，所以我们无法直接访问标题。那么，应该有一种方法可以从任何地方更改网页的*任何*元素。确实有这种方法。那就是通过网页的*文档对象模型*（*DOM*），我们将在下一节中详细讲解。

### 32.4.2 文档对象模型（DOM）

在►第[29.1.1节](474412_1_En_29_Chapter.xhtml#Sec2)的HTML重复部分中，我们看到网页浏览器读取HTML文件，并将其内部转换为一种名为*文档对象模型*（*DOM*）的表示。这是一个层次结构的文档结构表示。结构中的节点可以是：

+   文档本身（最高节点），

+   单独的HTML元素，如**title**、**body**、**h1**或**p**，

+   与元素相关的任何文本（我们在上一节中示例网站的**title**和**h1**元素有直接关联的文本），或者

+   HTML元素的属性，如**script**元素的**src**属性。

绘制这些元素的层次结构结果是一个网页文档对象模型的表示，如图◘[32.5](#Fig5)所示。![](../images/474412_1_En_32_Chapter/474412_1_En_32_Fig5_HTML.jpg)

文档对象模型的流程图。文档后跟着 HTML，它被分为头部和主体。头部后面是标题和 JavaScript 测试。主体被分为 h1、p 和 script。

图 32.5

我们示例网站的文档对象模型（DOM）

文档对象模型的各个节点在 JavaScript 中由相应的对象表示。借助这些对象，我们可以编辑节点，从而更改网页上显示的 **h1** 标题的文本。为此，我们只需要获取正确的元素。这并不容易，因为文档中可能有多个相同类型的元素（例如 **h1**）。因此，诀窍是“定位”我们想要编辑的那个元素。这正是我们将在接下来的章节中讨论的内容。

顺便说一下，文档对象模型中表示整个文档的最高节点在 JavaScript 中由我们在前一节中已经使用过的对象表示：**document**。如你所记得，我们曾用它的 **write()** 方法将 HTML 代码写入网页，该方法在嵌入 JavaScript 程序的位置调用。

### 32.4.3 通过属性选择 DOM 节点

通过 ID 选择 HTML 元素

捕获 HTML 元素（即网页文档对象模型中的一个节点）最简单的方法是通过其 **id** 属性来定位它。在我们在 ► Sect. [32.4.1](#Sec5) 中的示例 HTML 文档中，你可以看到一个段落元素（**p**），其代码如下，我们之前没有使用过：

**<p** id="output"**></p>**

该元素不包含任何文本或其他 HTML 元素（在 **>** 和 **<** 之间没有任何内容），但它有一个 **id** 属性，我们可以用它来访问该元素。**document** 对象的 **getElementById(*****id*****)** 函数用于此目的。语句

**var** outputField = document.getElementById('output'); 创建一个 **outputField** 对象，它对应于我们网页中的 **p** 元素，通过它我们可以编辑网页上的该元素。你可以很快看到，**outputField** 是一个真正的对象，具有属性和方法，只需输入 **outputField**（即对象标识符后跟点操作符），弹出窗口会显示该对象的属性和方法。

提供的属性和方法当然取决于对象的类型。在我们的示例中，我们处理的是一个 **HTMLParagraph** 对象。类似地，对于各种 HTML 元素类型，还有一系列其他对象类型。每种对象类型可能带有与特定类型 HTML 元素相关的特定属性和方法。然而，它们的共同点是，它们都派生自 **HTMLElement** 对象类型，因此共享某些属性和方法。

所有 HTML 元素都可以有一个 **id** 属性，其值（如同 HTML 属性一样）用引号括起来。在处理 **id** 属性时，只需确保每个 ID 在文档中只出现一次，这样就可以用它来唯一标识相应的元素。

按照元素类型选择 HTML 元素

HTML 元素不仅可以通过其唯一 ID 获取，还可以通过其类型获取。为此，可以使用 **document.getElementsByTagName(*****type*****)** 方法。然而，需要注意的是，一个 HTML 文档中可能会有多个相同类型的元素。因此，**document.getElementsByTagName()** 也会返回一个包含所有找到元素的*数组*。如果你仔细观察，会发现该方法与 **getElementById()** 不同，它是复数形式——名字中有一个 s——这并非没有道理！

为了说明这一点，我们可以重建我们在 ► Sect. [32.4.1](#Sec5) 中的脚本，以便*所有*的 **p** 元素都能被获取：

**var** random = Math.round(Math.random()*100, 0);document.write(`<p>一个 0 到 100 之间的随机数：${random}。</p>`);**var** pElements = document.getElementsByTagName('p');console.log(pElements.length);

如果你打开 JavaScript 控制台，你会看到 **pElements** 数组的长度是 2。但为什么是两个元素呢？难道我们的 HTML 文档中只有一个 **p** 元素吗？第二个元素从哪里来？这个第二个元素是我们通过使用 **document.write()** 语句在脚本中创建的。

现在我们可以开始处理这些元素。例如，我们可以使用**innerText**属性来显示附加到我们脚本创建的 HTML 元素的文本元素内容，该元素直接位于文档对象模型中。这个元素是数组中的第二个，也就是索引为 1 的那个：

**>** pElements[1].innerText"一个 0 到 100 之间的随机数：62。"按 CSS 类选择 HTML 元素

类似于元素类型，HTML 元素也可以通过其 **class** 属性的值来获取。正如你从 ► Sect. [29.​1.​1](474412_1_En_29_Chapter.xhtml#Sec2) 中的 HTML 复习中记得的，HTML 元素可以通过其 **class** 属性进行分组，并且可以在层叠样式表（CSS）文件中为其设置特定的格式和展示设置。通过这种方式，可以定义格式和展示指令，这些指令不仅应用于某一类型的所有元素（例如，所有的 **p** 元素），而是只应用于其中的一部分元素。

使用 **document.getElementsByClassName(*****class*****)** 方法，可以获取所有其 class 属性与 **class** 对应的 HTML 元素的数组。我们上面的简单示例没有使用 CSS，因此没有任何 HTML 元素拥有 **class** 属性。

### 32.4.4 通过文档的层级结构选择 DOM 节点

文档对象模型的层次结构可以用来从一个节点开始捕获其他相关节点。为此，所有节点对象都提供了许多预定义的属性。

节点的子元素

以下示例展示了如何从 HTML 文档的 **body** 元素开始，抓取所有直接位于*下一级*的 DOM 节点：

**var** bodyElements = document.getElementsByTagName('body');**var** bodyChildren = bodyElements[0].childNodes;**for**(**var** i = 0; i < bodyChildren.length - 1; i++) {console.log('节点号', i)console.log('节点名称:', bodyChildren[i].nodeName);console.log('节点类型:', bodyChildren[i].nodeType, '\n');}

为此，我们首先选择 body 元素；更准确地说，我们通过 **document** 方法 **getElementsByTagName()** 抓取 *所有* body 元素。当然，在我们的网页中只有一个 body 元素。然而，**getElementsByTagName()** 方法总是返回一个数组。我们在下一行中访问它的第一个元素。然后，我们使用它的 **childNodes** 属性。**childNodes** 是每个 DOM 节点自动拥有的只读数组，包含了“子节点”，即那些在层次结构中直接位于该节点下的节点，也就是在我们这个例子中，它们的*父节点*是 **body**。

在一个 **for** 循环中（我们将在 ► 第 [35.​1](474412_1_En_35_Chapter.xhtml#Sec1) 节中详细讨论），我们遍历所有子元素并将它们的两个属性输出到 JavaScript 控制台，分别是它们的名称和类型。对于我们的示例网页，控制台输出将如下所示：

节点号 0节点名称: #text节点类型: 3节点号 1节点名称: H1节点类型: 1节点号 2节点名称: #text节点类型: 3节点号 3节点名称: P节点类型: 1节点号 4节点名称: #text节点类型: 3节点号 5节点名称: SCRIPT节点类型: 1

节点的名称对应 HTML 元素的标识符；对于文本节点，我们会看到**#text**作为名称。正如你所看到的，**body**元素下附有多个文本节点。在我们的示例网页中，body 内只有其他 HTML 元素，但它们前后可能会有文本。这些文本在我们的示例网页中是空的，实际上，它们包含了制表符缩进，以更好地强调 HTML 源代码的层次结构。这些制表符字符通过上面输出中的文本节点表示。为了清晰起见，我们在文档对象模型中省略了它们的表示，详见 ◘ 图 [32.5](#Fig5)。

文本也包含在文档的 **h1** 标题中（“我们的测试页面”），但它处于一个层级上*更低一级*的文本节点中：它没有附加在网页的 **body** 元素下，而是附加在 **h1** 元素下，因此不被我们的 body 元素子节点遍历所捕获。

查询属性

同样适用于**p**元素和**script**元素的*attributes*。它们是按层次结构附加在**p**和**script**元素上的，因此它们不是**body**元素的直接子节点（可以说是它的孙子节点）。

然而，属性有一个特殊性：它们并不作为独立的节点包含在数组**childNodes**中。你可以通过在控制台中输入**bodyChildren[5].childNodes**来轻松检查这一点（**body**的第5个子节点是**script**元素）。**childNodes**是空的！首先，这可以理解，因为在**script元素**下面没有其他HTML元素或文本节点按层次结构悬挂。但是属性**src**（脚本文件的名称）是附加在**script**元素上的，而这个属性在我们网页的文档对象模型中也是一个节点。然而，这个节点并未包含在**childNodes**中。属性是以数组对象**attributes**的形式映射的。**bodyChildren[5].attributes[0]**表示我们**script**元素的第一个属性，**src**。可以通过**nodeName**和**nodeValue**属性访问属性的名称和值，在我们的示例中是通过**bodyChildren[5].attributes[0].nodeName**（这将返回**"src"**）。

还有另一种访问HTML元素属性的方法。属性也是元素对象的属性。因为**bodyChildren[5]**是我们的**script**元素，我们可以通过**bodyChildren[5].src**直接访问它的**src**属性的*值*（名称已经在属性标识符中）。像许多情况一样，**bodyChildren[5]**对象的**src**属性值是一个简单的字符串。

识别节点的类型

让我们再回到上面的输出。有两点突出：首先，节点是按照它们在文档中出现的顺序映射到数组中的；如果你想按从上到下的顺序绘制**body**的子节点，这会很方便。其次，似乎有两种节点类型，1和3。类型为1的节点是HTML元素，类型为3的节点是文本节点。属性的节点类型是2；因此，我们的**script**元素的**src**属性也有一个**nodeType**属性：

bodyChildren[5].attributes[0].nodeType 查找节点的父元素

除了**childNodes**，还有一个用于在DOM结构中导航的重要对象，那就是每个DOM节点的一个属性：**parentNode**。**parentNode**是**childNodes**的对应物，它指定当前节点（我们查询其**parentNode**属性的节点）在层次结构中直接隶属于哪个节点。与**childNodes**不同，**parentNode**不是一个数组，而是一个单一的节点，因为每个子节点下只有一个父节点。

32.1 [5分钟]

假设你在JavaScript中有一个对象 **elem**，它表示网页中的一个HTML元素。你如何访问 **elem** 的兄弟元素（包括 **elem** 本身），也就是在HTML文档中与 **elem** 处于相同层级的所有HTML元素？

### 32.4.5 更改HTML元素

将HTML代码直接注入到对象中

所有HTML元素对象在JavaScript中都有 **innerHTML** 对象属性。它是一个字符串，包含了挂在各自HTML元素下方的所有HTML代码。

让我们看看我们网页的示例，来自► 第[32.4.1](#Sec5)节。它的body元素，如我们可以在控制台轻松检查到的，具有以下 **innerHTML** 属性：

**>** document.body.innerHTML"<h1>我们的测试页面</h1><p id="output"></p><script src="script.js"></script><p>0到100之间的随机数：31。</p>"

当然，我们也可以编辑这个属性，从而“注入”HTML代码到一个对象中。假设我们不想将随机数字输出到一个新的段落元素（**p**）中，脚本会在网站运行时将其插入到该位置，而是希望将数字写入到具有ID **output** 的现有段落元素中。为此，我们的脚本 **script.js** 只需通过ID获取该段落元素，然后将包含随机数字的输出“注入”到该元素中。这样，我们的脚本 **script.js** 就可以像这样：

rndNum = Math.round(Math.random()*100, 0);pOutput = document.getElementById("output");pOutput.innerHTML = '0到100之间的随机数：'+ rndNum + '。';

然而，我们可能希望将输出加粗并嵌入到 **strong** 元素中。为此，我们只需修改脚本的最后一行，方法如下：

pOutput.innerHTML ='<strong>0到100之间的随机数：'+ rndNum + '。</strong>';

如果你现在查看浏览器中显示的页面源代码，或者直接使用 **document.body.innerHTML** 在控制台中查看 **body** 元素的HTML内容，你会发现其中包含以下内容：

**"**<h1>我们的测试页面</h1><p id="output"><strong>0到100之间的随机数：33。</strong></p><script src="script.js"></script>**"**

如你所见，我们成功地将一段HTML代码“注入”到了 **p** 元素的输出中。

更改元素的属性

除了使用 **b** 元素外，还有另一种方法可以将文本加粗，那就是利用CSS属性 **font-weight**。如果将其设置为 **bold**，文本也会显示为加粗样式。

HTML 元素的 CSS 属性可以通过单独的 CSS 文件来描述（在我们本章结束时的两个示例中会采用这种方法），或者直接使用 HTML 元素的 **style** 属性来设置。因此，如果我们想让段落元素 **output** 的所有内容以粗体显示，我们需要修改打开的 HTML 标签，如下所示：

**<p** id="output" style="font-face: bold;"**>**

在 CSS 中，属性名和属性值总是通过冒号分隔。严格来说，我们不需要在最后加上分号。然而，在 **style** 属性中可以放置多个 CSS 属性赋值，这些赋值之间必须用分号分隔。因此，在 **style** 属性的末尾加上分号是没有问题的。

但我们现在如何通过 JavaScript 代码设置 **style** 属性呢？在上一节之后，这个方法应该不会让你感到惊讶。毕竟，我们已经知道 HTML 元素对象（在上面的脚本中，我们通过 **getElementById** 将其绑定到 **pOutput** 变量）有一个与每个标准属性相匹配的属性。当然，我们可以对这些属性进行赋值。需要注意的是，**style** 是一个对象，具有多个属性，反映了 CSS 属性。属性的名称与 CSS 属性相同，但 CSS 中常见的连字符被省略，代之以大小写字母。因此，**font-weight** 变成了 **fontWeight**：

pOutput.style.fontWeight = 'bold';

如果你现在——为了让我们也能观察到效果——将 HTML 代码的“注入”重置为

pOutput.innerHTML = '一个介于 0 和 100 之间的随机数：' + rndNum + '.'; 并重新加载浏览器中的网页，你会注意到操作成功，输出内容已经以粗体显示。现在，**style** 属性是一个特殊情况，HTML 元素对象的 **style** 属性不能像 **"font-face: bold;"** 这样直接赋值给 JavaScript，而必须通过 **style** 对象的各个属性来操作。

然而，许多属性在 JavaScript 中的 HTML 元素对象中都有对应的属性，可以直接赋值。例如，决定文本方向的 **align** 属性，可以通过以下语句赋值：

pOutput.align = 'right'; 使得段落内的文本右对齐（试试看！）。与 **style** 不同，HTML 元素对象（在我们这里是 **pOutput** 的 **align** 属性）的相应属性不是对象，而是一个简单的字符串，可以直接赋值。因此，这条语句使得 **p** 元素的代码看起来像这样：**<p** id="output" align="right"**>**32.2 [10 min]

创建一个简单的网页，其中包含一个**p**元素（段落），并在其中加入一段文字。在JavaScript程序中，改变该文字的字体背景颜色（CSS属性**background-color**），使文字呈现淡黄色（红色分量：255，绿色分量：255，蓝色分量：204）。

### 32.4.6 添加和删除HTML元素

添加HTML元素

在上一节中，我们使用了HTML元素对象的**innerHTML属性**将HTML代码直接“注入”到元素中，通过这种方式，我们还能够通过将完整的HTML代码写入父元素来创建新的HTML对象作为父元素的子元素。在这一节中，我们将探讨另一种方法，通过在JavaScript中生成相应的HTML元素对象，然后将它们“挂接”到文档中的目标位置来创建HTML元素。

新的HTML元素对象可以通过JavaScript中**document**对象的**createElement()**函数轻松创建。作为参数，这个函数期望传入要创建实例的HTML元素类型的标识符。

例如，要创建一个新的子标题（HTML元素类型为**h2**），只需以下语句即可：

**var** heading2 = document.createElement('h2');

现在我们可以根据需要编辑新元素的属性，例如，使用**align**属性使标题文字右对齐：

Headline2.align = 'right';

当然，标题也需要文字。我们可以通过元素对象已经知道的**innerHTML**属性来设置它，或者使用innerText属性。**innerText**通常表示附加到元素本身或其子元素中的所有文本节点；如果你查看我们网页的**body**元素的**innerText**属性，就能更清楚这一点。然而，我们也可以使用**innerText**向我们新创建的元素（它没有子元素）添加文本：

heading2.innerText = '另一个激动人心的部分';

在我们充分配置好新HTML元素对象之后，我们仍然需要将它添加到我们想要放置的网页上。最简单的方法是抓取目标父元素，然后通过元素对象方法**appendChild(*****newChild*****):**将新子元素添加到其中：

**var** bodyElem = document.getElementsByTagName('body')[0];bodyElem.appendChild(heading2);

另外，如果你不想仅仅将新元素追加到现有子元素的后面，你可以通过使用元素对象方法**insertBefore(*****newChildElement*****,** ***successorChildElement*****)**更精确地控制它的位置。通过这种方式，我们可以在段落元素**output**之前插入新标题，我们在程序中用对象**pOutput**表示它：

bodyElem.insertBefore(heading2, pOutput);32.3 [5 min]

开发一段 JavaScript 代码，你可以在 JavaScript 控制台中运行，它会将加粗格式的文本“这是结尾。”添加到网页的 HTML body 中（在网页底部）。

试试吧：拿一个网页，比如► [*wikipedia.com*](http://wikipedia.com)，打开浏览器的开发者工具并运行你的代码。你会看到你的 HTML 元素已经被添加到网页中了！

删除 HTML 元素

删除网页中的 HTML 元素，可以通过所有 HTML 节点对象在 JavaScript 中固有提供的 **remove()** 方法方便地实现。例如，要删除段落元素 **output**，我们只需在 **pOutput** 对象上调用 **remove()** 方法：

pOutput.remove()

该元素会立即从网页中消失。就像在添加和更改对象时一样，浏览器会重新生成显示，而无需用户或我们作为开发者做任何操作。

## 32.5 表单输入

在接下来的内容中，我们将了解如何使用 JavaScript 来验证或以其他方式处理来自 HTML 表单的输入。下一节首先简要介绍 HTML 表单的工作原理。如果你已经熟悉这部分内容，你可以—无需遗漏任何内容—直接跳到 ► Sect. [32.5.2](#Sec13)。

### 32.5.1 HTML 中的表单

除了对话框，我们迄今为止主要关注如何在网页中输出数据，但没有涉及用户如何输入数据。这正是 HTML 表单的作用：它们用于接受用户输入的数据。接收到的数据通常会发送到提供该页面的 Web 服务器并在服务器上处理。这通常涉及到 PHP 编程语言的使用，这正是为此目的开发的，但有时也会涉及到服务器端的 JavaScript 程序。在这种客户端-服务器的情况下，JavaScript 通常负责在数据发送到 Web 服务器之前，在客户端验证用户的输入，例如检查是否有不正确的输入，必要时停止数据发送，并通知用户输入错误。

然而，数据不一定非要发送到 Web 服务器。实际上，表单输入也可以作为 JavaScript 应用程序的输入；此应用程序将不再是一个验证机制，而在某种程度上是数据的最终接收者。数据的输入只是为了被 JavaScript 程序处理。本章的两个例子，一个计算器和一个颜色选择器，正好属于表单和 JavaScript 之间交互的范畴。

然而，在深入了解这些应用之前，让我们首先看看如何在HTML中构建表单。表单总是通过HTML元素**form**来创建的。这会创建一个最初为空的表单。在**form**内，可以有任意数量的不同**input**元素，代表不同的输入选项。每个元素所代表的输入类型由**input**属性中的**type**控制。考虑以下简单的（登录）表单作为示例：

**<form** action="http://www.mysupernicewebsite.com/login.php" method="POST"**>**用户名：**<br>****<input** type="entry" value="" name="username"**><br>**密码：**<br>****<input** type="password" value="" name="password"**><br>****<input** type="submit" value="登录"**>****</form>**在这个例子中，我们创建了一个包含三个输入元素的表单：

+   **entry** 类型的元素，用于输入用户名；这是一个简单的文本输入框

+   **password** 类型的元素，这实际上是**entry**类型的特殊变体，输入的字符会被星号掩盖

+   **submit** 类型的元素，一种将表单内容发送到服务器的特殊按钮

除了这些，还有许多其他类型的输入元素，例如**button**（“普通”按钮，**submit**类型的按钮有一个非常特殊的功能），**radio**（单选按钮），**checkbox**（复选框，可以进行查询），**range**（滑块）和**textarea**（多行文本输入）。还有允许选择日期的输入元素（**date**）、颜色（**color**）或上传文件（**file**），以及其他支持输入模式的元素。

所有元素都有一个**value**属性，包含它们的当前值；对于文本输入框来说，这是当前输入框中的文本，而对于**submit**按钮来说，这是按钮的标签。这个属性非常重要，因为它可以用来确定用户的输入，这些输入将被处理。除了**value**，输入元素还可以有一个**name**属性（与所有HTML元素一样）。如果你想在服务器端访问输入值，这非常有用。另一方面，如果我们仅在客户端使用JavaScript，我们也可以像平常一样通过**id**属性访问这些元素，为了简便，以上示例中省略了**id**。**name**还用于将那些需要一起评估的元素进行分组；这尤其适用于单选按钮组中的单个选择项，其中每次只能选择一个选项（我们将在下面的示例中深入探讨这个问题）。

输入元素的行为可以通过许多其他属性进行微调；例如，**required** 属性如果字段未填写则会阻止表单提交，而 **readonly** 属性则会阻止用户修改输入元素的当前值。这两个属性都是 **boolean** 类型，因此它们的值可以是 **true** 或 **false**。然而，实际上我们通常看到的是仅仅使用 **required**，而不是 **required="true"**。该属性的存在本身就被评估为 **true**，在这种情况下已经足够将输入元素指定为必填项。

除了这些标准属性外，各种输入元素还可以具有其他特定类型的属性。例如，**range** 输入元素（表示滑块）具有 **min** 和 **max** 属性，用于描述可以通过滑块选择的范围的限制（该范围的值随后可以在 **value** 属性中查询）；复选框有一个 **boolean** 类型的 **checked** 属性，用于指定复选框当前是否应该被选中。

到目前为止，我们尚未讨论 **form** 元素本身的属性。**action** 属性决定了在用户通过 **submit** 按钮触发表单提交时，应该调用哪个地址（通常是 PHP 脚本）来将数据传递给服务器。**method** 属性决定了应使用哪种方式通过 *超文本传输协议*（HTTP）来传输数据。该属性的默认值是 **GET**，但当需要传输敏感数据（例如密码）时，通常使用 **POST**。

**form** 元素的 **action** 和 **method** 属性，以及用于发送数据的 **submit** 按钮，只有在要将输入的数据传输到 web 服务器时才需要。然而，本章结尾的颜色选择器示例根本不需要任何按钮，计算器示例使用了按钮，但没有 **submit** 按钮。两个应用程序都直接在客户端 JavaScript 程序中处理数据，因此可以不需要任何传输数据的预防措施。

### 32.5.2 从 JavaScript 访问表单

在我们的 JavaScript 程序中，我们经常需要处理用户在表单中输入的数据。为了做到这一点，我们需要从 JavaScript 访问表单元素，以获取它们包含的数据，同时还需要找到一种方式将这种访问（以及随后的数据处理）与用户的操作关联起来。毕竟，在 web 界面领域，我们也在一个 *事件驱动* 的环境中工作，用户触发事件（例如，点击按钮），然后我们的 JavaScript 应用程序对此做出反应。

为了了解事件控制过程及如何访问表单数据，让我们来看一个常见的例子，即摄氏度与开尔文之间的温度转换。

这个应用程序可以有一个界面，用户输入温度并决定是否将该温度转换为摄氏度（如果输入的是开尔文温度）或转换为开尔文（如果输入的是摄氏度温度）。点击按钮启动转换并输出结果。

这样的界面的HTML代码如下所示：

**<!DOCTYPE html>****<html>****<head>****<title>**温度转换</title>**<noscript>**请启用JavaScript！**</noscript>****</head>****<body>****<script** src="kelvincelsius.js"**></script>****<h1>**温度转换：开尔文 <=> 摄氏度**</h1>****<form>****<p>**输入要转换的温度：**<input** id="temp" type="text" value="" size="5"**>****<span** id="unitLabel"> 开尔文**</span></p>**转换为：**<br>****<p><input** type="radio" name="direction" checked onchange="change('Kelvin')"**>**摄氏度**</p>****<p><input** type="radio" name="direction" onchange="change('Celsius')"**>**开尔文**</p>****<p></p>****<input** type="button" value="转换" onclick="convert()"**>****</form>****</body>****</html>**如图◘ [32.6](#Fig6)所示！[](../images/474412_1_En_32_Chapter/474412_1_En_32_Fig6_HTML.jpg)

一张开尔文-摄氏度转换的HTML表单截图。它有一个文本框用于输入，两个单选按钮用于选择摄氏度或开尔文。底部有一个转换按钮。

图 32.6

开尔文-摄氏度转换的HTML表单

该表单包括一个ID为**temp**的文本输入框，用于输入*温度*，两个单选按钮（**direction**）用来定义转换方向，还有一个按钮触发转换操作。

你还会看到一个我们以前没见过的HTML元素，即**span**。**span**本身没有任何特殊功能，但它帮助我们为文本显示提供一个自己的ID，以便在JavaScript程序中访问它。在我们的**span**元素**unitLabel**中，我们表示用户输入温度的单位。每次他更改转换方向的选择时，这个单位显示也必须随之更改。

我们通过**name**属性将两个单选按钮组合在一起：这意味着它们属于同一组，因此一次只能选择其中一个。请注意，单选按钮的分组是通过**name**属性实现的，而不是通过**id**属性。区别在于ID是一个*唯一*标识符，因此不能有两个元素具有相同的ID。我们的两个单选按钮根本没有ID，因为我们也可以通过名称在JavaScript程序中访问它们。启动转换的按钮甚至没有ID或名称。两者都不是必须的，因为按钮触发一个操作，从而启动我们的JavaScript程序，但我们不需要在程序中访问它。

**p**和**br**元素仅具有设计功能（**br**创建一个简单的换行符），它们帮助我们使表单看起来更加视觉吸引人。所以，正如您所看到的，**form**元素中不仅可以放置**input**元素，还可以使用整个HTML元素种类（包括表格和图片）来构建一个吸引人的表单。

然而，我们还没有考虑表单中的一个非常重要的部分：**direction**单选按钮和**Convert**按钮的**onchange**和**onclick**属性。每个属性的值是一个JavaScript函数（一个*事件处理函数*），该属性的名称与一个事件相关联，即在该事件发生时会调用相应的JavaScript函数。例如，当用户点击我们的按钮时，**click**事件会被触发。当**click**事件发生时，浏览器会自动检查**onclick**属性是否已设置，如果已设置，则执行其中指定的JavaScript函数。通过这种方式，我们将界面与JavaScript程序连接起来。

在我们的示例中，它看起来是这样的：

**function** convert() {**var** temp = Number(document.getElementById('temp').value);**var** direction = document.getElementsByName('direction');**if**(direction[0].checked == **true**) {document.write(`<p>${temp} Kelvin are${temp - 273.15} degrees Celsius.<p>`);}**else** {document.write(`<p>${temp} degrees Celsius are${temp + 273.15} Kelvin.<p>`);}}**function** change(unit) {**var** unitLabel = document.getElementById('unitLabel');unitLabel.innerHTML = unit;}

整个程序仅由两个函数组成，即与单选按钮和主按钮相关联的两个事件处理函数。函数**change()**作为事件处理函数存储在单选按钮的**onchange**属性中，因此每当**change**事件发生时，都会调用该函数。每当用户点击单选按钮中的一个时（顺便说一句，我们也可以将事件处理程序附加到**click**事件上），此事件便会发生。当事件发生时，函数会被调用，并传入一个参数，即要显示在**span**元素**unitLabel**中的单位，用于表示用户输入的单位。在HTML代码中，您可以清楚地看到，每当调用事件处理函数时，它都会立即传递所需的单位作为参数：**onchange="change('Kelvin')"**。

在事件处理函数**change()**中，我们首先使用**document.getElementById()**选择**span**元素，然后替换其中的HTML代码；在我们的示例中，这只是纯文本，实际上没有任何其他的HTML编码。

现在来看我们的另一个事件处理程序，**convert()**，它在用户点击“转换”按钮时被调用。它的结构非常简单。首先，我们通过查询**temp**输入框的**value**属性来获取温度值，我们是通过ID选择该输入框的。注意，我们需要将该值转换为**number**变量，因为我们想要用温度值进行计算。表单本身始终将输入的值保存为**string**；有一些方法可以配置表单输入框，使其一开始就只允许输入数字，但为了简单起见，我们这里没有这样做。接下来，我们通过名称选择单选按钮。为此，我们使用**getElementsByName()**函数。请注意**Elements**中的复数s！由于名称不像ID那样不一定是唯一的，因此在通过名称选择时，可能会选择到多个元素。这正是我们示例中的情况。调用**getElementsByName()**返回的值是一个*数组*，在我们的例子中是两个单选按钮。接下来的步骤是使用单选按钮的**checked**属性来检查我们的第一个单选按钮（索引0！）是否被选中。此时不用太担心If-Else结构，我们将在►第[34.1节](474412_1_En_34_Chapter.xhtml#Sec1)中详细讨论这类程序分支。如果第一个单选按钮被选中，意味着我们程序的用户希望将温度从开尔文转换为摄氏度。然后，我们通过**document.write()**将其输出到网页上，使用的是模板字符串（如果你不再熟悉模板字符串，请翻回几页到►第[32.2节](#Sec2)）。

如你所见，我们的JavaScript程序完全由事件处理程序组成，这些事件处理程序在浏览器触发它们时才会激活，因为有某个事件发生，并且它们与该事件相连。我们将在►第[34.3节](474412_1_En_34_Chapter.xhtml#Sec5)中更详细地讨论事件，当时我们将讲解程序流程控制。在这一点上，了解基本机制足矣，它告诉我们如何将JavaScript代码与界面控件进行“连接”。

32.4 [5分钟]

修改开尔文-摄氏度转换示例，使输出不再通过**document.write()**完成，而是输出到一个必须在网页界面中内嵌的类型为**span**的HTML元素中。

32.5 [30分钟]

开发一个简单的应用程序，在该程序中，用户可以使用滑块来改变应用程序网页上显示的一些示例文本的字体大小。字体大小可以通过HTML/CSS中的**fontsize** CSS样式选项设置，并且以像素（**px**）为单位；有效的字体大小设置可以是例如**'18px'**。如果你觉得在开始这项任务之前需要一些“灵感”，可以先处理接下来的两个章节中的示例。

## 32.6 示例：简单计算器

在本节及下一节中，我们将开发两个小示例应用程序。首先，我们将实现一个简单的计算器。该计算器应能处理四种基本的算术运算，并允许将计算结果复制到剪贴板。数字和运算符的输入可以通过按钮或通过键盘直接输入。

我们的应用程序由三个文件组成：

+   HTML 文件 **calculator.html**，构建网络接口

+   层叠样式表（CSS）文件 **calculator.css**，帮助我们定义按钮和显示器的设计，以及

+   JavaScript 程序 **calculator.js**，提供接口功能

### 32.6.1 网络接口

让我们从 HTML 文件 **calculator.html** 开始：1 **<!DOCTYPE html>**2 **<html>**34 **<head>**5 **<title>**计算器**</title>**6 **<link** rel="stylesheet" type="text/css" href="calculator.css"**>**7 **<noscript>**请启用 JavaScript！**</noscript>**8 **</head>**910 **<body** bgcolor="#282923"**>**11 **<script** src="calculator.js"**></script>**1213 **<form>**14 **<input** id="display" type="text" value="0" class="inputOutput"**>**15 **<p></p>**16 **<input** type="button" value="C" class="normalButton functionButton" onclick="clearDisplay()"**>**17 **<input** type="button" value="复制" style="width:104px" class="normalButton functionButton" onclick="copy()"**>**18 **<input** type="button" value="/" class="normalButton functionButton" onclick="key('/')"**>**19 **<p></p>**20 **<input** type="button" value="7" class="normalButton" onclick="key('7')"**>**21 **<input** type="button" value="8" class="normalButton" onclick="key('8')"**>**22 **<input** type="button" value="9" class="normalButton" onclick="key('9')"**>**23 **<input** type="button" value="*" class="normalButton functionButton" onclick="key('*')"**>**24 **<p></p>**25 **<input** type="button" value="4" class="normalButton" onclick="key('4')"**>**26 **<input** type="button" value="5" class="normalButton" onclick="key('5')"**>**27 **<input** type="button" value="6" class="normalButton" onclick="key('6')"**>28 **<input** type="button" value="-" class="normalButton functionButton" onclick="key('-')"**>**29 **<p></p>**30 **<input** type="button" value="1" class="normalButton" onclick="key('1')"**>**31 **<input** type="button" value="2" class="normalButton" onclick="key('2')"**>**32 **<input** type="button" value="3" class="normalButton" onclick="key('3')"**>**33 **<input** type="button" value="+" class="normalButton functionButton" onclick="key('+')"**>**34 **<p></p>**35 **<input** type="button" value="0" class="normalButton" style="width:104px" onclick="key('0')"**>**36 **<input** type="button" value="." class="normalButton" onclick="key('.')"**>**37 **<input** type="button" value="=" class="normalButton functionButton" onclick="calculate()"**>**38 **</form>**39 **</body>**4041 **</html>** 第 1–8 行

常见的HTML头部，在这里我们首先包含了CSS文件**calculator.css**，并使用**noscript**元素为用户在浏览器中禁用JavaScript的情况做出预处理。CSS文件通过**link**元素进行集成。

第10行

我们通过**bgcolor**属性将网页背景设置为深色调，这样我们的计算器看起来也更加时尚。毕竟，眼睛也在做数学！

第11行

我们包含了脚本**calculator.js**，该脚本包含了页面的实际功能。从技术上讲，它在网页加载时就会被执行，但正如我们下面所看到的，它仅由一些作为事件处理程序被调用的函数组成，换句话说，它是由各个按钮驱动的事件驱动型脚本。只要这些函数没有被明确调用，脚本执行时应用程序端什么都不会发生。我们完全可以将脚本放在网页的**body**部分，这不会影响应用程序的功能。

第13行和第38行

我们页面的其余**body**部分是一个HTML表单，包含了计算器的所有控件。

第14行

在这里我们定义了计算器的显示区域。我们给它设置了id为**"display"**，以便以后可以在JavaScript程序中引用。它的类型是**text**，所以它是一个输入字段，毕竟用户也应该能够通过键盘输入数字和运算符；在我们的计算器中，用户可以直接在显示区域输入。初始值应该为0，除非用户输入了其他内容。另外，我们通过**class**属性为显示区域赋予了一个类信息。对于这个类，我们定义了**inputOutput**，在CSS文件中有专门的设计说明。所以，我们不需要通过HTML代码中的属性（特别是CSS属性**style**）直接定义样式，而是将这些设置外包到单独的CSS文件中，使我们的代码更加清晰，易于维护。这样，如果我们想要更改计算器显示区域的样式，我们只需要通过页面头部的**link**元素包含另一个CSS文件，其中也包含了**inputOutput**类的设计声明，这样显示区域的样式就会改变，而我们无需调整实际的网页（HTML文档）。

第16至37行

这就是实际按钮的作用。通过**onclick**属性，我们为每个按钮分配一个JavaScript函数，该函数在用户点击按钮时触发。这个事件处理函数要么是**key(character)**，它将数字或运算符作为参数传递给按钮，要么是特殊函数**calculate()**，用于在用户点击等号时触发计算，或者是**clear()**，用于清除显示内容，或者是**copy()**，用于将当前显示的内容复制到剪贴板。最初，除了特殊功能按钮（如运算符、复制、清除和等号按钮）之外，所有按钮的**class**属性都为**normalButton**。功能按钮不仅属于**normalButton**类，还属于**functionButton**类。**functionButton**类确保这些按钮具有橙色的背景色，而**normalButton**类的按钮则具有默认的颜色（通常是灰色的阴影）。稍后我们会结合CSS指令详细了解这一点。

如你所见，按钮本身没有被赋予**id**。严格来说，这有些乱，但对我们来说并不必要，因为我们不需要通过JavaScript代码来访问按钮。恰恰相反：按钮通过点击时调用相应的事件处理函数来访问我们的代码。

你可以在◘ 图 [32.7](#Fig7) 中看到完整的界面。![](../images/474412_1_En_32_Chapter/474412_1_En_32_Fig7_HTML.jpg)

计算器界面的截图。界面顶部有一个显示屏，下方有从0到9的数字，除法、乘法、减法、加法、等号、C和复制的符号。

图 32.7

计算器应用程序的界面

### 32.6.2 CSS设计指令

为了将HTML文件中描述的界面基本结构与各个元素的详细设计分离，我们在本例中将后者移到一个独立的CSS文件**calculator.css**中。

CSS文件为三类对象定义了设计声明，分别是**normalButton**（基本所有按钮）、**functionButton**（功能按钮）和**inputOutput**（计算器的显示屏）。这些设计声明按类在一个用花括号括起来的CSS块中呈现。该块前面是*选择器*，它指定了要应用设计声明的网页HTML元素。前面的点表示“所有**class**属性*包含*指定类的对象”。在► 节 [32.6.1](#Sec15) 中，我们看到功能按钮属于两个类：**normalButton**（所有按钮的类）和特殊类**functionButton**。因此，CSS选择器**.functionButton**会使适当的设计声明应用于这些按钮。

1 .normalButton {2 width:50px;3 height:50px;4 }56 .functionButton {7 background-color: #ED5036;8 color: #FFFFFF;9 border: 1px solid #ED5036;10 }1112 .inputOutput {13 width:208px;14 height:60px;15 background-color: #282923;16 color: #66FF33;17 border: 1px solid #ED5036;18 padding-right: 5px;19 font-family: "Lucida Console";20 font-size:32px;21 font-weight: bold;22 text-align: right;23 }第2-3行

对于**normalButton**类，也就是最初所有按钮，我们定义了高度和宽度（从CSS文件中删除这些设计声明并重新加载页面，你会看到什么效果？）

对于**functionButton**类，我们额外定义了特殊的背景色和前景色，以及按钮边框的设计（这里是与按钮背景色相同的颜色，宽度为一像素的实线）。那些仅属于**normalButton**类的按钮（即，主要是数字按钮）自然也有一个配色方案，但我们没有显式地定义它；因此，使用的是默认值，这通常会导致这些按钮显示为灰色。对于**functionButton**类，我们通过自定义的颜色规范覆盖了这些默认值。一旦你在浏览器中加载了页面，打开开发者工具并点击“Elements”（在非谷歌*Chrome*浏览器中，可能会有不同的标签名称）。在这里，你会看到一个功能按钮（在谷歌*Chrome*浏览器中，位于最左上角），允许你切换到一个特别的元素检查模式。在此模式下，你可以通过点击页面上的元素来选择它，并在开发者工具中获取关于它的更多信息。在元素检查器中（◘ 图[32.8](#Fig8)），你会在页面的HTML源代码左侧看到所选元素，而在右侧则是该元素的CSS设计规范。设计的默认值是从下往上读取的。在我们的例子中（选中了带有除法运算符的功能按钮），你会看到一系列的CSS设计属性，首先是**input**类的默认值（位于最底部的CSS块），接着是上面的一个专门针对**button**类型的**input**元素的CSS块。再往上，是我们定义的两个按钮类的CSS块，**normalButton**和**functionButton**。一些属性被划掉了。这意味着这些属性被更具体的CSS块所覆盖。例如，**button**类型**input**元素的CSS块中的**color**和**background**属性被划掉了，因为它们在专门为**functionButton**类按钮定义的CSS块中有不同的定义（而且选中的按钮正是这种按钮）。通过这种方式，你可以快速看到你的元素有哪些CSS设计属性及其来源。![](../images/474412_1_En_32_Chapter/474412_1_En_32_Fig8_HTML.jpg)

计算器界面和元素检查器的截图。元素检查器显示一组程序代码，标题样式显示在右侧。

图 32.8

Google *Chrome*中的元素检查器

我们通过在网页界面的HTML代码中使用**style**属性，直接为复制显示内容的按钮和数字0分配宽度。**style属性**包含仅应用于当前元素的CSS代码。这优先于CSS样式表文件中的所有其他声明，正如你在元素检查器中检查某个元素的CSS声明层级时所看到的。

第13–22行

这是设置计算器显示设计的地方；包括背景、字体、颜色和大小，以及元素边缘的文本缩进（*padding*）。

### 32.6.3 JavaScript 代码

我们应用程序的JavaScript代码由四个事件处理函数组成，当不同的按钮被点击时，它们从HTML界面被触发：  

**key(character)**和**clearDisplay()**函数是事件处理函数，当用户点击对应按钮时会被调用。如你所记，我们总是通过网页的HTML代码调用**key(character)**函数，字符作为参数（无论是数字还是运算符），这个字符分配给被按下的键。通过使用这种“技巧”，我们只需要一个函数来处理所有按钮，而无需为每个按钮编写单独的事件处理器。

两个函数都会更改屏幕上的显示内容。为此，我们首先总是使用**document**对象的**getElementById()**方法“抓取”网页表单中的显示元素。然后我们修改显示元素的**value**属性，也就是输入元素上显示的文本；使用**key()**时，我们仅仅将按下按钮的标签添加到当前值中（第3行）。

第11–15行

要将当前显示的内容复制到剪贴板，我们首先使用**select()**方法选择现有文本，该方法属于**显示输入**元素，然后调用浏览器的复制命令。

第17–20行

当用户希望执行输入的计算并点击带有等号的按钮时，显示的值会更新。这里我们使用了**eval(*****expression*****)**函数，它会计算作为字符串传入的表达式，也就是在我们的例子中：对其进行计算。然后我们使用**Number()**将结果转换为数字，再使用**toFixed()**方法将其格式化为六位小数的字符串表示。

## 32.7 示例：颜色选择器

在这个例子中，我们开发了一个小应用程序，允许用户以简便的方式设计符合红绿蓝（RGB）方案的颜色，并将其转换为 HTML 中常见的十六进制编码。此类应用程序，即使是更为复杂的应用程序，也可以在互联网上**大量**找到。

### 32.7.1 Web 界面

我们应用的界面非常简单。它由三个滑块组成，分别用来改变红色、绿色和蓝色的色彩成分，并且有一个字段用来以**#RRGGBB**的十六进制代码形式显示结果颜色。通过滑块选择的颜色将作为网页的背景色，这样用户就能清楚地看到自己所创造的颜色。1 **<!DOCTYPE html>**2 **<html>**34 **<head>**5 **<title>**颜色选择器**</title>**6 **<noscript>**请启用 JavaScript！**</noscript>**7 **</head>**89 **<body** id="bodyElem"**>**1011 **<div** style="background:#FFFFFF; margin: 0 auto;padding:10px; width:400px;"**>**1213 **<form>**14 **<input** id="hexColor" type="input" value="#000000" readonly**>**15 **<p>**红色：**</p>**16 **<input** id="colorRedRange" type="range" value="255"min="0" max="255" oninput="adjustColor()"**>**17 **<input** id="colorRedOutput" type="input" value="255"readonly**>**18 **<p></p>**19 **<p>**绿色**</p>**20 **<input** id="colorGreenRange" type="range" value="255"min="0" max="255" oninput=" adjustColor ()"**>**21 **<input** id="colorGreenOutput" type="input" value="255"readonly>22 **<p></p>**23 **<p>**蓝色**</p>**24 **<input** id="colorBlueRange" type="range" value="255"min="0" max="255" oninput=" adjustColor ()"**>**25 **<input** id="colorBlueOutput" type="input" value="255"readonly**>**26 **</form>**2728 **</div>**2930 **<script** src="colorpicker.js"></script**>**3132 **</body>**3334 **</html>**

让我们详细看看界面：

第 9 行

这次我们给页面的**body**元素添加了**id**，因为我们想要以所选的色调为背景色渲染页面。为了做到这一点，我们需要在 JavaScript 代码中调整**body**元素的**bgcolor**属性。

第 11 行

HTML中的**div**元素简单地标记了页面上的一个连续区域，最终形成一个最初不可见的框。我们将所有控件放在这样的框中。然后，我们可以使用CSS属性**style**将**div**元素的颜色设置为白色（**#FFFFFF**表示红色、绿色和蓝色的颜色部分均为255），并将其居中显示在页面上（通过将**margin**属性的值设置为**0 auto**实现）。此外，我们还使用**padding**属性为该框设置了10像素的外边距，这样控件就可以离框的边缘有一些空白空间，并将框的宽度固定为400像素。

第13至26行

**div**框内的表单包含一个文本输入框，在其中显示转换为十六进制表示的颜色代码（第14行）。默认情况下，颜色应为白色，除非用户通过滑块选择了其他颜色。我们还希望输入框为只读，因此添加了**readonly**属性，这是一个**boolean**类型的属性，因此不需要显式赋值为真（但我们也可以写成**readonly="true"**）。

然后我们添加了三个滑块（**color*****Colorname*****Range**），每个滑块对应RGB值的一个颜色部分***Colorname***。这些滑块的类型为**range**，其可调范围在0（**min**）和255（**max**）之间。每当用户移动滑块时（事件**oninput**），事件处理函数**adjustColor()**被触发，该函数将调整**hexColor input**字段中的十六进制颜色代码，重置页面的背景颜色，并最终在滑块旁边的（只读）输入框中显示新的颜色值（**color*****Colorname*****Output**）。通过使用空段落元素**<p></p>**，我们提供了换行，从而提高了可读性。

你可以在◘ 图 [32.9](#Fig9)中看到整个界面。![](../images/474412_1_En_32_Chapter/474412_1_En_32_Fig9_HTML.jpg)

颜色选择器应用界面的截图。它有三个颜色，每个颜色都有一个滑块和一个文本框。文本框中显示了数值数据。

图 32.9

颜色选择器应用界面

### 32.7.2 JavaScript代码

我们在网页中第30行引入的JavaScript文件**colorpicker.js**仅包含事件处理函数**colorAdjust()**，该函数在用户每次移动滑块时被调用。

代码详细信息：1 **function** adjustColor() {23 **var** bodyElem = document.getElementById('bodyElem');4 **var** hexColor = document.getElementById('hexColor');56 **var** colorRedRange = document.getElementById('colorRedRange');7 **var** colorGreenRange = document.getElementById('colorGreenRange');8 **var** colorBlueRange = document.getElementById('colorBlueRange');910 **var** colorRedOutput = document.getElementById('colorRedOutput');11 **var** colorGreenOutput = document.getElementById('colorGreenOutput');12 **var** colorBlueOutput = document.getElementById('colorBlueOutput');1314 **var** hexRed = Number(colorRedRange.value).toString(16);15 **var** hexGreen = Number(colorGreenRange.value).toString(16);16 **var** hexBlue = Number(colorBlueRange.value).toString(16);1718 **if**(hexRed.length == 1) hexRed = '0' + hexRed;19 **if**(hexGreen.length == 1) hexGreen = '0' + hexGreen;20 **if**(hexBlue.length == 1) hexBlue = '0' + hexBlue;2122 **var** hex = '#' + hexRed + hexGreen + hexBlue;23 hexColor.value = hex.toUpperCase();2425 bodyElem.bgColor = hex;2627 colorRedOutput.value = colorRedRange.value;28 colorGreenOutput.value = colorGreenRange.value;29 colorBlueOutput.value = colorBlueRange.value;30 }第3–12行

在这里，我们首先为需要访问的界面中不同的元素创建变量。

第14–16行

接下来，我们获取当前滑块设置的值（使用它们的**value**属性），并将值转换为十六进制字符串。如你所记得，在►第31.3.2节中，**toString()**方法有一个参数，用于指定将数字转换为字符串时的进制系统，在我们的情况下是16，因为我们希望得到十六进制表示。

第18–20行

使用变量**hexRed**、**hexGreen**和**hexBlue**，我们已经将所有需要的信息准备好，以便以**#RRGGBB**格式显示十六进制颜色值。但有一个小问题：颜色组件变量的值可能是单个数字（如果相应颜色组件的十进制值小于16）。在这种情况下，我们必须在前面添加一个0，因为**#RRGGBB**形式的十六进制颜色代码要求每个颜色组件的值是*恰好两个*数字。因此，我们检查先前生成的颜色部分字符串的长度，并在必要时添加一个0。

第22–23行

现在，我们可以组合十六进制值并将其显示在我们的（只读）输入元素**hexColor**中。

第25行

我们还将刚刚确定的十六进制RGB值赋给**bgcolor**属性以及**body**元素。因此，一旦用户激活其中一个颜色比例滑块，不仅十六进制颜色值**hexColor**的显示会发生变化，网页的背景颜色也会随之变化。

第27–29行

最后，我们将颜色百分比值作为十进制数显示在分别放置在颜色百分比滑块旁的（只读）输入框中。

## 32.8 总结

在本章中，我们学习了如何使用 JavaScript 输入和输出数据。特别是，我们了解了 JavaScript 控制台以及 JavaScript 应用如何与网页进行交互。

请务必从本章中记住以下几点：

+   **console.log()** 方法可以用来在 JavaScript 控制台输出对象。

+   模板字面量允许你在字符串中以占位符的形式包含变量，在字面量创建时将占位符替换为变量的当前值；变量写作 **${variable}**，整个字面量本身用反引号 (**`**) 包围。

+   模板字面量的替代方法是字符串替换和字符串与对象的连接，这些都可以通过加号运算符输出为字符串。

+   使用 **console.warn()** 和 **console.error()** 可以在控制台输出警告或错误信息。

+   与用户的交互还可以通过对话框进行；特别是使用 **alert()**（显示消息）、**confirm()**（具有“确定”和“取消”选项的对话框）和 **prompt()**（弹出对话框中的文本输入）。

+   JavaScript 非常适合编辑网页的 HTML 元素，通过 JavaScript 应用使网页动态化。

+   最简单的方法是使用 **document.write()** 将 HTML 代码写入脚本正在网页中运行的当前位置。

+   HTML 页面中的组件，尤其是 HTML 元素本身、它们的属性和内部文本，可以作为*文档对象模型*（DOM）的节点以层级结构表示。

+   JavaScript 允许将 DOM 元素选择并编辑为 HTML 元素对象，对这些对象的修改会立即反映在网页的渲染中。

+   DOM 节点主要通过其 **id** 属性（使用 **document.getElementByID()**）、其类型（使用 **document.getElementsByTagName()**；注意复数形式，这里返回的是一个数组，因为可能有多个元素符合该条件！）或其 CSS 类（使用 **document.getElementsByClassName()**；同样，返回的是一个数组）来识别。

+   返回的是表示网页 HTML 元素的元素对象/元素对象数组，这些元素对象的属性是 HTML 元素的属性。

+   此外，从一个元素对象开始，可以利用 DOM 结构通过类似 **childNodes** 和 **parentNode** 的属性选择层级关联的对象。

+   元素对象的 **innerHTML** 和 **innerText** 属性分别表示 HTML 元素中包含的 HTML 代码（即 DOM 中层级从属元素的代码）和其中包含的文本。

+   HTML 元素可以通过 **document.createElement(*****type*****)** 在网页上创建，并通过调用其 **appendChild(*****new_element*****)** 方法将其添加到另一个元素下；HTML 元素的 **insertbefore(*****new_element*****,** ***before_child*****)** 方法将 ***new_element*** 作为子元素添加到另一个子元素（***before_child*****)** 之前；**remove(*****element*****)** 移除网页上的 HTML 元素对象 ***element***。

+   实际上，网页上与用户交互的最重要形式是使用 *表单*；它们通过 HTML 中的 **form** 元素创建，因此它们的组件（即文本输入框或按钮等控件）位于 **<form>** 和 **</form>** 之间。

+   表单的元素主要是 HTML 类型为 **input** 的元素，并根据其 **type** 属性进一步区分；例如，**"text"** 是文本输入框的类型，**"button"** 是按钮的类型，**"slider"** 是滑块的类型。

+   用户通过这些控件的操作（例如，点击按钮）可以通过事件与 JavaScript 代码中的事件处理函数相关联，每当与操作相关的事件被触发时，事件处理函数就会自动调用。事件处理函数的调用通过属性值传递给 HTML 元素，其中属性名由 **on** 和事件名称组成，例如，**onclick** 代表 **click** 事件。

## 32.9 练习解答

练习 32.1

**elem** 的兄弟元素（包括 **elem** 本身）实际上就是 **elem** 的父元素的子元素。因此，**elem.parentElement.children** 返回一个 **HTMLCollection**，即对应 HTML 元素的对象集合。你可以像处理数组一样操作这种类型为 **HTMLCollection** 的对象。

练习 32.2

在网页的 HTML 源代码中，你的 **p** 元素可能如下所示：

**<p** id="paragraph1">这里是一个注释。**</p>**

你现在可以在你的 JavaScript 程序中更改背景颜色：

**var** pElem = document.getElementById('paragraph1');pElem.style.backgroundColor = '#FFFFCC';

**background-color** 属性很方便更改，因为我们的元素对象 **pElem** 对应于一个同名的 **style** 属性。当这样做时，请注意，CSS 中的 **background-color** 属性在 JavaScript 中变成了元素对象 **style** 属性下的 **backgroundColor** 属性（即去掉了连字符，且属性名中第一个组件的字母后的任何字母变为大写）。当然，你还需要将 RGB 十进制颜色分量转换为十六进制数值，以获得有效的颜色代码，形式为 **'#RRGGBB'**。在转换时，255（红色和绿色分量）变为 **FF**，204（蓝色分量）变为 **CC**。

练习 32.3

代码可能如下所示：

**var** bodyElem = document.getElementsByTagName('body')[0];**var** pElem = document.createElement('p');pElem.style.fontWeight = 'bold';pElem.innerText = 'This is the end';bodyElem.appendChild(pElem);

首先，我们通过其元素标签抓取网页的**body**元素（注意：**getElementsByTagName()**返回一个HTML节点数组，因为网页中可能有多个相同类型的元素——至少对于**body**之外的元素）。然后我们创建一个新的**p**元素，使用CSS属性对其进行格式化，给它设置**"This is the end"**文本，并将其作为新的子元素添加到网页的**body**元素中，即将其附加到现有子元素的末尾。

顺便说一句：如果你将此脚本包含在网页中，像我们通常做的那样，即通过网页body的**script**属性，那么**"This is the end"**会出现在网页的*开头*！原因很简单：脚本在body的开始处加载和执行，这时网页的body中没有其他元素。我们通过上述代码添加的元素就是第一个元素，因此在页面上逻辑上显示在顶部。

练习 32.4

首先，必须将（仍然是“空”的）**span**元素插入到HTML代码中：

**<span** id="output">**</span>**

你只需要稍微修改一下**convert()**函数的代码，首先选择**span**元素，然后将输出赋值给**innerHTML**属性：

**function** convert() {**var** temp = Number(document.getElementById('temp').value);**var** direction = document.getElementsByName('direction');**var** outputSpan = document.getElementsById('output');**if**(direction[0].checked == **true**) {outputSpan.innerHTML = `<p>${temp}开尔文是${temp - 273.15}摄氏度。</p>`;}**else** {outputSpan.innerHTML = `<p>${temp}摄氏度是${temp + 273.15}开尔文。</p>`;}}**function** change(unit) {**var** unitLabel = document.getElementById('unitLabel');unitLabel.innerHTML = unit;} 练习 32.5

该网站可能会像这样显示：

**<!DOCTYPE html>****<html>****<head>****<title>**字体大小**</title>****<noscript>**请启用JavaScript！**</noscript>****</head>****<body>****<script** src="fontsizecontroller.js"**></script>****<form>**<p>字体大小：<input id="controller" type="range" min="1" max="150" value="20" onchange=" changeFontSize()">**</p>****</form>****<span** id="sampletext" style="font-size: 20px;"**>**一些字体大小为20的文本**</span>****</body>****</html>**

相应的JavaScript程序在**fontsizecontroller.js**中将如下所示：

**function** changeFontSize() {**var** size = Number(document.getElementById('controller').value);**var** text = document.getElementById('sampletext');text.style.fontSize = size + 'px';text.innerHTML = 'Some text in size ' + String(size);}
