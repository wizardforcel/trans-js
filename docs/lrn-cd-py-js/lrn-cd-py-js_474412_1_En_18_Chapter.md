© 作者，独家授权 `Springer Fachmedien Wiesbaden GmbH`，`Springer Nature` 2024J. L. Zuckarelli《用 `Python` 和 `JavaScript` 学习编码》 [https://doi.org/10.1007/978-3-658-42912-6_18](https://doi.org/10.1007/978-3-658-42912-6_18)

# 18. `工具与帮助`：编程需要什么？

`Joachim L. Zuckarelli`^([1](#Aff2) )(1)`慕尼黑`，`德国`概述

首先，我们来看看你编程所需的 `Python` 环境。幸运的是，这并不复杂，因此我们可以很快开始实际工作。

在本章中，你将学习：

+   如何安装 Python 解释器

+   如何安装 `PyCharm` 开发环境

+   如何使用 `Python` 的帮助功能

+   如何使用非官方的 Python 帮助资源。

## 18.1 安装 Python 解释器

你可以方便地从 ► [http://www.python.org](http://www.python.org) 下载 Python 安装程序。该网站由 `Python Software Foundation` 运营，后者是负责协调 Python 进一步开发的组织。在该网站的“Downloads”栏目下，选择适合你操作系统的最新 Python 版本即可。在本书中，我们使用的是适用于 `Windows` 的 `Python`，但我们在这里讨论的内容同样适用于 `macOS` 和 `Linux` 版本。你安装的 `Python` 被称为 `CPython`，可以说是“官方”的 Python 版本，Python 的发明者 `Guido van Rossum` 也参与了它的开发。此外，还有许多其他的 Python 实现，甚至有些 Python 解释器是用 Python 自己编写的！另一方面，`CPython` 是用 `C` 编程语言开发的。而你现在下载的正是这个 `CPython`，尽管在 ► [python.org](http://python.org) 网站上它没有以这个名称列出。

下载完成后，运行安装程序并按照屏幕上的指示进行操作。记下 Python 将安装到的路径。你无需更改安装程序提供的默认设置。安装通常会在几分钟内完成。

顺便提一下，`CPython` 仅以英文存在，这意味着所有的消息、警告和其他输出都仅以英文显示；Python 编程语言也只使用英文术语。在这方面，你并没有错过安装时可以选择语言的对话框，因为根本没有这个选项！除此之外，建议你还是安装所有工具的英文版本，因为如果你不理解错误消息，或者想了解如何使用某个工具执行某项操作时，使用英文版可以更容易在互联网上查找帮助。

安装完成后，您就可以开始使用了。如果您切换到Python安装目录，您可以在该位置调用`Python`程序。一个窗口将打开，看起来像图◘[18.1](#Fig1)。![](../images/474412_1_En_18_Chapter/474412_1_En_18_Fig1_HTML.jpg)

Python控制台的截图。它显示了用户可以输入以获取额外信息的单词列表，如help、copyright、credits和license。

图18.1

Python控制台首次启动后的界面

这就是`Python console`。它允许您在`interactive mode`中运行Python，即输入语句并直接执行（如果您不再记得交互模式和脚本模式之间的区别，请滚回►第`[9](474412_1_En_9_Chapter.xhtml)`章）。控制台处理的一个命令是`**quit()**`；它退出Python控制台并关闭窗口。

除了这种交互模式，Python当然还提供了脚本模式，允许我们编写和运行更长的程序。Python代码文件通常具有扩展名`**.py**`。因此，如果您有一个程序`myprogram.py`并想要运行它，您需要在操作系统的终端/控制台中进入Python目录并输入：

`python myprogram.py`当然，使用集成开发环境比直接使用Python解释器更方便。Python以`IDLE`的形式提供了这样的环境。然而，即使它支持语法高亮等功能，它也相当基础。您可以在◘图`[18.2](#Fig2)`中获取`IDLE`的印象。在接下来的部分，我们将使用`PyCharm`，这是一个更强大的开发环境，我们将在下一步进行安装。![](../images/474412_1_En_18_Chapter/474412_1_En_18_Fig2_HTML.jpg)

Python开发环境的截图显示了几行文本。顶部的菜单栏包括文件、编辑、shell、调试、选项、窗口和帮助。底部的一行提示输入help、copyright、credits和license以获取更多信息。

图18.2

Python开发环境`IDLE`

## 18.2 安装`PyCharm` IDE

`PyCharm`是一个流行的集成开发环境（IDE），用于Python，由捷克软件公司`JetBrains`开发，总部位于布拉格。`JetBrains`专注于开发工具，并提供一些知名的IDE，如`IntelliJ IDEA`（特别用于Java）、`WebStorm`（用于Web开发，特别是JavaScript）、`PHPStorm`（用于PHP）或`RubyMine`（用于Ruby）。他们还开发了一种编程语言`Kotlin`，主要用于移动应用开发。

您可以从►[https://​www.​jetbrains.​com/​PyCharm/​](https://www.jetbrains.com/PyCharm/) 网站下载免费的社区版`PyCharm`。此版本功能有限，但已提供了本书中使用的功能之外的更多特性。点击“Download”按钮后选择您的操作系统；Windows、MacOS和Linux均受支持。下载完安装程序后，启动安装过程。您可以保留默认设置；但是，建议在安装程序的“Create Associations”部分至少将`.py`文件与`PyCharm`关联，这样以后`.py`文件就会自动用IDE打开。安装通常不需要很长时间，但需要超过1.6 GB的可用硬盘空间。曾经可以通过三四张容量为1.44MB的3.5英寸软盘安装MS-DOS开发环境的时代已经一去不复返了！

当您第一次启动`PyCharm`时，您可以在“Customize”部分配置是否使用深色或浅色配色方案。本书中的所有插图都是使用浅色配色方案制作的，以便于打印；然而，作者通常使用深色模式，这对眼睛的压力较小。此时最好先退出`PyCharm`，关闭对话框。在下一章中，我们将开始我们的第一个Python项目，然后继续进行这部分内容。

## 18.3 获取Python帮助

在互联网上

Python 是世界上最流行的编程语言之一。因此，互联网上有无数与 Python 相关的资源也就不足为奇了。其中之一是前面提到的 `Stack Overflow` 平台，你可以在这里找到大量关于 Python 的问题和答案，几乎可以满足你的所有需求。截至本文写作时，`Stack Overflow` 上有超过 210 万个标记为 `Python` 的问题，今天就新增了 1,039 个。你的问题也许就能在这 200 万个问题中找到答案。因此，`Stack Overflow` 是解决大部分问题的好地方。`Stack Overflow` 的热门问题也经常出现在 Google 的搜索结果前列。当然，你可以在 Google 搜索中加入 `site` 关键字（`site:`► [`StackOverflow.com`](http://stackoverflow.com)），以将搜索范围缩小到 `Stack Overflow`。但即便是超出 `Stack Overflow`，互联网也充满了关于 Python 的帖子、博客、教程、视频和各种各样的内容格式。

“官方” Python 帮助

Python 本身也提供了官方帮助。如果你想了解某个特定的编程语言元素是如何工作的，可以参考 Python 自动安装的类和函数文档。你可以通过在 Python 控制台中调用 `help(element)` 函数，并将模块、包、类或函数的名称作为参数传入，来查看相关信息。例如，调用 `help(print)` 会返回以下帮助信息：

`>>> help(print) print(...) print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False) 将值打印到流中，默认情况下是打印到 sys.stdout。可选的关键字参数：file：一个类文件对象（流）；默认是当前的 sys.stdout。sep：值之间插入的字符串，默认为空格。end：在最后一个值后附加的字符串，默认为换行符。flush：是否强制刷新流。`

如同在►第 [18.1](#Sec1) 节中所述，重新启动控制台并试试看！不要输入 `>>>`，这是提示符，表示控制台已经准备好接受你的输入。顺便说一句，如果你输入 `help()` 而不加参数，控制台会切换到 Python 帮助系统。修改后的提示符 `help>` 表示你现在可以输入术语，系统会显示匹配的帮助条目。你可以通过输入 `quit`（不加括号）退出帮助系统并返回到 Python 控制台。

我们的 `help()` 调用的输出为我们提供了有关 `print()` 函数参数的一些信息，最重要的是，告诉我们 `print()` 函数究竟做了什么。然而，这些帮助信息相当基础。如果你需要更多详细信息，最好自己在互联网上进行搜索。

`Python Software Foundation` 也在其网站 ► [python.​org](http://python.org) 上提供了大量关于 Python 标准库的信息（包括 `print()` 函数），位于“Library Reference”部分：► [https://​docs.​python.​org/​3/​library/​functions.​html#print](https://docs.python.org/3/library/functions.html%2523print)。 （请注意，这与我们下载 Python 解释器的网站相同。）“Language Reference” 解释了语言的结构和语法，但相对较为技术性。“Tutorial”部分包含了 Python 的介绍，但没有其他编程语言的先前知识，可能很难理解。

## 18.4 小结

在本章中，我们学习了如何安装 Python 以及 `PyCharm IDE`。我们还了解了获得 Python 帮助的最重要方式。

请确保从本章中掌握以下要点：

+   “官方”的 Python 实现，`CPython`，由 `Python Software Foundation` 进一步开发，并且是你从 ► [python.​org.​](http://python.org) 下载 Python 时默认安装的版本。

+   Python 配备了名为 `python` 的 Python 解释器程序，可以作为交互式 Python 控制台使用，也可以用来解释整个 Python 脚本。

+   通过 `IDLE`，Python 还提供了一个简陋的 IDE。

+   `PyCharm` 是 `JetBrains` 开发的一个非常强大的 Python 开发环境，其有限的社区版是免费的。

+   Python 本身通过 `help(element)` 函数提供帮助。它提供关于 Python 模块、类或函数的帮助文本，但这些文本通常不够详细。

+   进一步的“官方”帮助主要通过语言参考和 Python 标准库参考提供，地址为 ► [python.​org](http://python.org)。

+   此外，鉴于 Python 的高度普及，互联网上有很多丰富的信息来源；其中最重要的之一——像大多数其他编程语言一样——是开发者论坛 `Stack Overflow`。
