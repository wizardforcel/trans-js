© 作者（们），根据 Springer Fachmedien Wiesbaden GmbH 的独家许可，属于 Springer Nature 2024 J. L. Zuckarelli 《Python 和 JavaScript 编程入门》 [https://doi.org/10.1007/978-3-658-42912-6_28](https://doi.org/10.1007/978-3-658-42912-6_28)

# 28. 工具与帮助：我编程需要哪些工具？

Joachim L. Zuckarelli^([1](#Aff2) )(1) 德国慕尼黑 概述

在本章中，我们将讨论 JavaScript 是如何执行的，哪些开发工具可用，以及在哪里可以找到更多有关 JavaScript 的信息。正如你将看到的，你不需要太多的工具就能开始编写 JavaScript。为了简化，我们只会使用“基础工具”，而不使用像 Python 那样的集成开发环境。

在本章中，你将学习：

+   JavaScript 代码是如何被解释的，以及这对运行 JavaScript 代码所需工具的意义

+   如何编辑 JavaScript 代码

+   如果你需要帮助，可以在互联网上找到哪里提供帮助

## 28.1 解释器

在本书这一部分的介绍中，我们已经看到 JavaScript 是一种在网页开发中广泛使用的编程语言。因此，显而易见，JavaScript 程序的执行方式与例如 Python 程序的执行方式必须有所不同。毕竟，网站的用户不能被要求在查看网页之前先下载一个解释器。事实上，这根本不必要。所有现代浏览器都自带 JavaScript 引擎，能够解释 JavaScript。因此，作为开发者，你不需要安装解释器，浏览器会为你完成这项工作！

## 28.2 代码编辑器和开发环境

市场上有许多集成开发环境（IDEs）支持 JavaScript（以及其他语言）。例如，JetBrains 的 *WebStorm*（同样是提供本书上一部分使用的 *PyCharm* 的供应商）和 Apache 软件基金会的 *NetBeans*。其中一些是商业软件（如 *WebStorm*），而另一些则是免费的（如 *NetBeans*）。

然而，我们在这里会采取不同的方法：在本书的上一部分，我们使用了一个复杂的 Python 集成开发环境（IDE），而现在我们将使用一个更简单的工具来处理 JavaScript，即一个纯粹的代码编辑器。由于我们的 JavaScript 代码反正会嵌入到网页中，并在浏览器中执行，因此我们不需要为如何将解释器与代码编辑器集成而烦恼。我们只需在代码编辑器中编写 JavaScript 代码和使用它的网页，然后在网页浏览器中查看结果。

以下内容使用的是流行的编辑器 *SublimeText*，根据编写这些内容时的许可条款，它可以在试用期内（通常是无限期的）免费使用，但长期使用需要购买许可证。你也可以使用其他编辑器，比如微软的 *Visual Studio Code* 或 *Notepad++*。归根结底，所需的只是一个能够编辑实际 JavaScript 代码及其嵌入的网页的编辑器，其余的都将在网页浏览器中完成。因此，尽管你可以自由选择编辑器，还是建议选择一个支持 JavaScript 和 HTML 语法高亮的工具，无论是开箱即用还是通过适当的插件。

如果你只是想先试试 JavaScript，并尽量避免将 JavaScript 代码嵌入网页的麻烦，那么像 *JS Bin*、*JS Do* 或 *Plunker* 这样的网络服务可能对你有帮助。这些服务允许你直接输入 JavaScript 代码并执行，而无需任何额外的麻烦。你可以在同一个浏览器窗口中看到代码及其执行结果。在接下来的章节中，我们将简要介绍这些网络服务。不过，如果你打算认真学习和使用 JavaScript，还是应该选择一个代码编辑器或相应的集成开发环境（IDE）。

## 28.3 帮助与文档

与所有流行的编程语言一样，互联网上有无数关于 JavaScript 的信息来源。然而，JavaScript 并没有官方的、可用的文档。制定官方语言标准的 ECMA 提供了语言规范（2023年6月发布的 ECMAScript 13 版本，网址为 ► [https://​262.​ecma-international.​org/​13.​0/​](https://262.ecma-international.org/13.0/)）。然而，这对于实际工作来说并不那么愉快。

Mozilla 基金会提供了很好的面向应用的文档（► [https://​developer.​mozilla.​org/​en-US/​docs/​Web/​JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)），这个组织通过其 *Firefox* 浏览器继承了 JavaScript 发明者 Netscape 的事业。在这里，你可以找到包括所有标准 JavaScript 函数的帮助页面，页面内容包括函数的一般描述、调用该函数所需的参数、函数返回的值以及一些应用示例。此外，帮助页面还显示了各大浏览器（如 Internet Explorer、Edge、Chrome、Safari、Firefox 或 Opera）对每个函数支持的版本概述。例如，你可以查看 **sqrt()** 函数的帮助页面，它返回一个数字的平方根：► [https://​developer.​mozilla.​org/​en-US/​docs/​Web/​JavaScript/​Reference/​Global_​Objects/​Math/​sqrt](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/sqrt)。

此外，和几乎所有已知的编程语言一样，程序员论坛*StackOverflow*是一个解决具体问题的优秀信息来源，你可以在这里找到质量非常高的答案，涵盖各种常见（以及不常见）问题，如果没有相关答案，你还可以发起自己的问题讨论。

此外，互联网上有无数的文章、教程、博客、视频以及其他格式的资源，针对不同经验水平的用户，突出介绍了流行的JavaScript语言的各个方面。

## 28.4 小结

本章中，我们探讨了JavaScript是如何被解释的，以及编写和运行JavaScript代码所需的工具。

请务必记住本章中的以下几点：

+   JavaScript由网页浏览器解释执行；因此，你不需要单独的解释器或编译器。

+   一个文本编辑器就足以编辑JavaScript代码（以及集成的网页）。像*NetBeans*或*WebStorm*这样的集成开发环境也可以用于JavaScript。

+   JavaScript的官方文档相对有限。最好的文档是Mozilla基金会的文档。

+   与许多编程语言一样，JavaScript在遇到问题时，*StackOverflow*是一个不错的去处。

+   此外，互联网上还有许多“非官方”的信息来源，为所有实际编程问题提供了很好的服务。
