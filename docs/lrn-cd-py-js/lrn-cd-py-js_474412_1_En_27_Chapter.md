© 作者，独家授权给 Springer Fachmedien Wiesbaden GmbH，Springer Nature 旗下公司 2024 J. L. Zuckarelli《Python 和 JavaScript 编程学习》[https://doi.org/10.1007/978-3-658-42912-6_27](https://doi.org/10.1007/978-3-658-42912-6_27)

# 27. 引言

Joachim L. Zuckarelli^([1](#Aff2) )(1)德国慕尼黑 概述

在这一部分，我们将开始学习 JavaScript，这是本书中我们将要处理的第二种编程语言。与 Python 一样，我们将采用9个问题的框架来掌握这门语言。在本部分的第一章中，我们将简要回顾 JavaScript 的起源和应用领域。

JavaScript 是 Web 的语言。可能没有其他语言比 JavaScript 更广泛地用于编写 Web 前端，即现代网页用户界面。如今，几乎没有一个访问量大的站点能在没有 JavaScript 的情况下运行。当你在网页上看到验证输入的表单时，比如检查你输入的电子邮件地址或电话号码是否符合有效格式时，JavaScript 通常在其中发挥作用。如果在搜索框中输入几个字母后，你看到可能的搜索建议，JavaScript 通常也在后台完成这一任务。如果一个网页中有动画效果，比如根据点击或鼠标移动的情况显示或隐藏元素，或者高亮显示它们，后台通常也运行着 JavaScript 程序。因此，JavaScript 经常出现在几乎所有的编程语言排行榜上，也就不足为奇了（参见 ► 第[6章](474412_1_En_6_Chapter.xhtml)）。

JavaScript 与你第一次阅读时可能想象的情况相反，和另一种流行的、但学习难度更大的编程语言 Java 的关系不大。两者之间只有少数的语法相似之处。

这门语言的起源可以追溯到 *Netscape Navigator* 浏览器主导市场的时期。1995年，正值 Netscape 和 Microsoft 在浏览器市场上展开“浏览器大战”前夕，Netscape 发布了一种名为 *LiveScript* 的语言。它由 *Brendan Eich* 开发，并在与 Sun Microsystems 合作的过程中被更名为 *JavaScript*。关于这个名字是否与 JavaScript 实际上是为了在网页上与小型 Java 应用程序（也叫 Java applets）配合使用有关，或者是否主要是出于市场营销原因，借助 Java 日益增长的流行度，这一点仍不完全清楚。不过可以确定的是，JavaScript 很快成为了 Web 上主流的编程语言，甚至把微软的 VBScript 等竞争对手推出了市场。

Netscape早期曾努力推动该语言的标准化，并将标准化组织命名为Ecma（当时其名称仍是*欧洲计算机制造商协会*的首字母缩写）。因此，他们发布了ECMA-262标准，定义了一种叫做*ECMAScript*的语言。从那时起，JavaScript被视为ECMAScript的一个实现，和其他也实现该标准的语言一起（并根据它们自己的特点进行补充），如Adobe的*ActionScript*或Microsoft的*TypeScript*。

然而，在JavaScript的情况下，关于标准化的讨论严格来说是朝着错误的方向走的，因为JavaScript根本不是标准化的。这主要是因为有多种流行的JavaScript实现。JavaScript程序运行在网页浏览器中，因此它们会被浏览器下载并解释。每个支持JavaScript的浏览器都会带有自己的解释器，一个JavaScript引擎，这些引擎在不同厂商之间肯定会有所不同。微软的JavaScript方言叫做*JScript*，它遵循ECMA-262标准，但带有一些特定内容，因此在细节上与比如Google的*Chrome*浏览器解释的JavaScript变体有所不同。最糟糕的情况是，这些差异可能导致某些网页功能在一个浏览器中正常工作，而在另一个浏览器中无法正常工作。问题的关键在于细节。当然，在接下来的章节中，我们几乎不会遇到这些问题，因为我们将讨论的是符合ECMA-262标准并且在几乎所有支持JavaScript的地方都能被解释的语言元素。

JavaScript是一种通常由网页浏览器解释的语言，因此是*客户端*语言。从某种意义上讲，它是*PHP*的对立面，PHP运行在网页服务器上，可以在网页发送到浏览器之前修改网页内容（例如，通过从数据库读取数据记录，如产品信息，并将其显示在网页上）。然而，也有一些运行时环境，比如*Node.JS*，提供了一个JavaScript的实现，使得JavaScript也可以在服务器端执行。

然而，在接下来的章节中，我们将专注于经典的变体，即JavaScript，它运行在网页中，从而使网页变得动态。正如本书中Python部分的做法，我们再次按照九个主要问题来概述这门语言。
