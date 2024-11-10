© 作者，专有许可给 Springer Fachmedien Wiesbaden GmbH，属于 Springer Nature 2024 J. L. Zuckarelli 学习 Python 和 JavaScript 编程 [https://doi.org/10.1007/978-3-658-42912-6_8](https://doi.org/10.1007/978-3-658-42912-6_8)

# 8. 我需要什么才能开始编程？

Joachim L. Zuckarelli^([1](#Aff2)  )(1)德国慕尼黑概述

在我们开始编写程序之前，我们首先需要准备好正确的软件工具。这些工具包括编译器和/或解释器，它们将你编写的程序源代码翻译成机器语言，从而使计算机能够执行该程序。这还应该包括代码编辑器，用于编写程序的源代码。集成开发环境将这些工具和其他工具整合在一个共同的用户界面下。

除了这些“技术”工具，你有时还需要编程方面的帮助。因此，在本章中，我们还将讨论如何以及在哪里找到与你的编程语言相关的信息和支持。

在本章中，你将学习以下内容：

+   如何为你的编程语言获取编译器/解释器

+   代码编辑器提供的功能，以及它们与普通文本编辑器的区别

+   集成开发环境（IDEs）提供的功能，以及它们与纯代码编辑器的区别

+   市面上有哪些流行的代码编辑器和集成开发环境

+   如何在互联网上找到与你的编程语言相关的信息和支持

+   如何使用像 ChatGPT 这样的人工智能（AI）工具进行编程。

## 8.1 工具

> 我告诉你多少次了？做对事，选对工具！
> 
> （《星际迷航 VI：未来的国家》中的 Montgomery “Scotty” Scott）

### 8.1.1 编译器和解释器

从上一章中，你已经知道——根据编程语言的不同——你需要一个解释器或编译器将你的程序翻译成计算机可以理解的可执行机器代码，或者在运行时对你的程序源代码进行解释和执行。对于许多编程语言，编译器或解释器可以从互联网免费下载。特别是对于那些由事实上的非营利组织进行进一步开发的语言，例如 Python 或 R，就是这种情况。即使是由特定商业公司提供的专有语言，如由 Embarcadero 开发并发布的 Object Pascal 方言 Delphi，也通常有一个社区版，或是一个免费版，功能有限，但对于个人用户来说已经足够。然而，使用社区版开发商业应用程序可能会受到法律限制。因此，如果你打算出售自开发的软件，提前熟悉许可证条款是非常重要的。对于一些编程语言，根本不需要单独的解释器。例如，如果你想使用 JavaScript 编程，网页浏览器会负责解释和执行你的程序代码。如果你想使用 PHP 开发服务器端应用程序，代码的解释会直接在服务器上进行，只有其结果会被返回给客户端，并在浏览器中显示。

### 8.1.2 代码编辑器

要能够有意义地使用编译器或解释器，首先必须编写一个程序。正如我们已经看到的，程序最终不过是用一种特殊语言编写的指令文本。这里的重点是“文本”。因为你的程序源代码仅仅是文本，所以你可以使用任何允许编辑未格式化文本（即没有特殊格式，如粗体或斜体）的程序。如果你使用 Windows 操作系统，例如，你可以使用非常简单的 Windows 编辑器。然而，它的功能仅限于打开或创建文件、输入一些文本以及在编辑后保存文件。尽管这些基本功能原则上足以编写计算机程序，但仍然建议使用专门为编程开发的编辑器，或者至少使用一些可以让编程更容易的功能。

一个特别重要的功能叫做语法高亮。正如你所记得的，语法是编程语言的语法规则。语法高亮，顾名思义，就是一种功能，可以突出显示程序代码的某些部分，使代码更易读。例如，关键字（即编程语言的特殊保留“词”）或变量名会通过不同的字体颜色和/或字体样式（如粗体）来标记。没有语法高亮的编程当然也是可能的，但显然要不那么舒适，因为没有高亮显示，眼睛更难迅速地定位程序代码中的关键部分，也更难快速掌握代码中的某些结构。由于不同编程语言的语法各不相同，语法高亮必须针对每种语言进行不同的处理。许多文本编辑器支持多种编程语言的语法高亮，可能是开箱即用，也可能是通过扩展包来实现。这类文本编辑器包括 Atom、Notepad++、Sublime Text、Vim 或 Visual Studio Code。许多编辑器都可以免费使用，或者至少有一些功能受限的版本，但依然能够非常好地工作，例如流行的 Sublime Text。

由于市场上有大量的文本编辑器，提供了处理程序代码的特殊功能，因此这样的列表无法穷尽。所以，关于哪个是最佳代码编辑器的文章、博客和视频铺天盖地也就不足为奇了。这个决策取决于个人偏好，尤其是在功能和视觉外观方面；毕竟，眼睛也在编程。视觉外观的一个特殊方面是深色主题：也许你已经从一位经验丰富的程序员那里看到过，他坐在一个深色、几乎是黑色的背景前，在这种背景下，通过语法高亮显示的程序代码显得非常突出。为什么这种深色背景（“在*深色模式*下工作”）如此受欢迎？也许是因为将编辑器设置成这样“酷”，显示出你属于那个神秘的程序员社区，他们不断地在键盘上敲打着对普通人几乎无法理解的代码。这种假设可能部分正确。然而，另一个因素要重要得多。深色背景对眼睛的感觉远比明亮甚至白色背景要舒适。如果你需要连续几个小时专注于程序代码，你会很快发现，深色背景更适合眼睛，且不会刺眼，而程序代码则在高对比度下变得更为突出。在本书中，代码编辑器的屏幕截图始终保持明亮，但这只是因为这样在印刷时更容易重现。事实上，作者通常使用深色背景，这在大多数编辑器中都可以设置，某些编辑器（如 Sublime）甚至默认使用深色背景。

### 8.1.3 集成开发环境（IDE）

除了代码编辑器，还有一类工具——*集成开发环境*（IDE）。这些工具在功能上超越了纯粹的代码编辑器。

大多数集成开发环境（IDE）所具备的重要功能包括：

+   直接调用编译器/解释器

+   超越语法高亮的高效源代码编辑功能

+   如果语言支持图形用户界面，则提供图形化用户界面构建的功能

+   故障排除功能（调试）

+   管理包含多个文件的整个项目的功能。

在源代码编辑方面，常见的一个功能是自动补全：当你输入几个字母时，可能的指令或关键词会直接作为建议显示出来。这可以提高代码编写速度，同时减少错误率。此外，IDE 通常还提供自动语法检查功能，能够在你编写程序代码时就提醒你可能的错误。例如，如果你打开了一个括号，但没有在后面关闭它，IDE 会提醒你。这样，你可以在早期阶段就发现并修正程序中的错误，而不至于在调用编译器或解释器时才看到错误信息。源代码编辑中的实用功能通常还包括深入的帮助集成。例如，你通常可以直接从 IDE 中调用你当前正在编写的语句的帮助信息。

很多时候，你不仅需要为程序编写代码，还需要设计图形用户界面（GUI）。一些 IDE 为开发人员提供了丰富的支持。通常，你可以通过拖拽标准元素（如按钮、输入框或列表框）来拼接你的界面，然后根据需求调整这些标准元素的属性，比如为按钮设置新的标签，或更改它的大小甚至颜色。完成后，你只需将 UI 元素与你的程序代码连接起来，并在程序中对其进行调用，以便当用户点击按钮时，能够触发相应的操作。支持这种 UI 设计的 IDE 包括 Embarcadero 的 RAD Studio 或微软的 Visual Studio。

除了直接调用编译器或解释器，以及进行源代码编辑和界面设计的实用功能外，IDE 通常还提供调试功能，即系统地查找和修正错误。这个领域中的一个重要功能是例如在源代码中创建断点。如果你在设置了断点之后启动程序，它将只运行到断点所在的代码位置；之后，你可以手动让程序继续执行超出断点的部分。使用断点可以帮助你检查程序在没有错误的情况下是否能运行到断点所标记的位置。此外，你还可以查看断点处变量的内容。这种监控变量内容的功能是另一个重要的调试功能。它使你可以在程序运行时“查看”变量的内容，并实时查看其当前值，甚至在必要时修改它们。

如果你的程序由多个源代码文件组成，你通常可以在集成开发环境（IDE）中将它们保存为一个连贯的项目。这意味着你只需打开该项目，所有代码文件就都可以使用了。你还可以在项目层面保存一些特定设置，比如编译器的设置。

如同代码编辑器一样，市场上也有几乎无法管理的 IDE 数量，有些是免费的（开源或社区版），有些是收费的。有些专注于某种编程语言（例如 RStudio 或 JetBrains 的 PyCharm 用于 Python），而有些则是为处理多种不同语言而设计的，有时通过适当的插件来支持（例如微软的 Visual Studio 或开源解决方案 NetBeans）。

移动应用程序的 IDE，例如谷歌的 Android Studio，也允许你在具有特定参数的移动环境中模拟已开发应用的运行（例如硬件设备、配置），并评估系统资源的需求，如处理器负载或移动数据传输。因此，这些 IDE 是为特定目的设计的，即开发移动应用，而不是围绕特定的编程语言，因此通常支持不同的语言；以 Android Studio 为例，支持 C/C++、Java 和 Kotlin。

代码编辑器与 IDE 之间的过渡是相对流动的。许多代码编辑器允许附加编译器或解释器，从而已经具备了 IDE 的核心功能，但除了语法高亮外，它们在语言特定的代码编辑、调试或界面设计方面的支持较少。

◘ 图 [8.1](#Fig1)、[8.2](#Fig2)、[8.3](#Fig3) 和 [8.4](#Fig4) 展示了不同的 IDE。◘ 图 [8.4](#Fig4) 展示了一个非常古老的 Borland C/C++ IDE，运行在 MS-DOS 上。不过，你可以非常清晰地看到菜单栏中重要的 IDE 功能，如运行、编译、调试以及项目管理功能。![](../images/474412_1_En_8_Chapter/474412_1_En_8_Fig1_HTML.jpg)

Delphi 测试应用程序的截图。该页面包含多个部分，包括结构、对象检查器、表单 1、模型视图和调色板。表单 1 部分中间的文字是 "Say Hello World"。

图 8.1

Delphi 的集成开发环境（IDE）

![](../images/474412_1_En_8_Chapter/474412_1_En_8_Fig2_HTML.jpg)

一张截图展示了一行 Python 代码，用于打印 "Hello World"。文件名是 test.py。屏幕底部部分表示输出和文件路径。

图 8.2

用于 Python 的 PyCharm 集成开发环境（IDE）

![](../images/474412_1_En_8_Chapter/474412_1_En_8_Fig3_HTML.jpg)

R Studio 的截图包含 4 个部分。1\. 它展示了一段代码。2\. 在控制台选项卡下提供了不同的值。3\. 在环境选项卡下有一个表格，表示不同变量的功能。4\. 在帮助选项卡下列出了相关性、方差和协方差的描述及使用方法。

图 8.3

R 的集成开发环境（IDE）RStudio

![](../images/474412_1_En_8_Chapter/474412_1_En_8_Fig4_HTML.jpg)

一张代码编辑器的截图展示了一个用于打印 Hello World 的 C 语言代码。菜单栏位于顶部。不同功能键的操作标注在底部。

图 8.4

TurboC 集成开发环境（IDE）用于 C/C++ 

◘ 表格[8.1](#Tab1)展示了一些本地支持常见编程语言的 IDE 选择。像 Eclipse 或 NetBeans 这样的 IDE 可以通过插件扩展，支持多种语言。表格 8.1

选定的集成开发环境（IDEs）

| 编程语言 | 从 IDE 中选择 |
| --- | --- |
| C# | SharpDevelop, Visual Studio |
| C/C++ | AppCode, C++ Builder, CLion, NetBeans, QT Creator, Visual Studio |
| Java | AppCode, Eclipse, IntelliJ IDEA, JBuilder, NetBeans |
| JavaScript | AppCode, Aptana Studio, NetBeans, RubyMine, Visual Studio, WebStorm |
| Perl | Komodo IDE, Padre |
| PHP | Aptana Studio, Komodo IDE, NetBeans, PhpStorm, Zend Studio |
| Python | Aptana Studio, PyCharm, Rodeo, Spyder, Thonny |
| R | Rcommander, RStudio |
| Ruby | Aptana Studio, Komodo IDE, RubyMine |
| Swift | AppCode, Xcode |
| VBA | Microsoft Office, Visual Studio Tools for Office (VSTO) |

在决定使用代码编辑器还是 IDE 时，通常会考虑你希望使用的仅 IDE 提供的工具（如调试功能或界面设计功能）。即便你不打算使用这些功能，IDE 提供所有功能的一个大优势仍然是很重要的，尤其是当你考虑到在开发过程中总是需要的核心工具，如编译器或解释器时。另一方面，IDE 本身往往是相当复杂的程序，拥有大量按钮、不同的工具栏/功能区、窗口和标签，你首先需要摸索这些界面。通过◘ 图[8.1](#Fig1)，[8.2](#Fig2) 和 [8.3](#Fig3)，可以大致了解其复杂性。由于 IDE 是为专业人士开发的，制造商显然并不关心你能在几分钟内学会如何使用所有功能和选项。毕竟，IDE 不是临时使用的工具，也不是偶尔使用的，而是作为所有编程工作的控制中心长期使用。因此，可能需要一些时间才能完全了解新工具的所有可能性。但一旦你掌握了 IDE，你就能高效工作，因为这正是这些工具的开发目的。

提示

尝试不同的代码编辑器和 IDE，看看哪种最适合你。不要被众多功能所困扰。你写和运行程序时只需要很少的功能。随着时间的推移，你会学会使用并欣赏工具中的更多功能。不要一开始就试图理解所有的功能，而是集中精力使用那些真正必要的功能，即编辑和编译/执行代码的功能。

最终，你必须自己决定想要使用哪些工具。试用不同的代码编辑器/集成开发环境（IDE）是个不错的主意，然后再做决定。本书中，我们将使用一个完整的 IDE——Python 的 PyCharm，以及一个经典的代码编辑器——在处理 JavaScript 时使用 Sublime Text。在写这些段落时，作者意识到自己似乎无意识地遵循了一个简单的规则——如果编程语言不需要在自己电脑上安装特殊的独立编译器或解释器（例如 JavaScript 或 PHP 等），那么代码编辑器就是首选工具。对于需要安装编译器或解释器的语言，则需要使用语言特定的 IDE。然而，最终并没有一个适用于所有人的金科玉律。只有一件事有效：试一试！

### 8.1.4 简单的在线开发环境

如果你想在不安装所有必要工具的情况下尝试某种语言，通常可以使用一些特殊的网站，允许你直接输入和执行代码。执行所需的所有功能，如编译和解释代码，都是由网站提供的。一些这样的“在线 IDE”的例子包括：

+   ► [http://​cpp.​sh/​](http://cpp.sh/) 用于 C++ 编程语言，

+   ► [https://​www.​compilejava.​net/​](https://www.compilejava.net/) 用于 Java，

+   ► [https://​js.​do/​](https://js.do/) 用于 JavaScript，

+   ► [http://​phptester.​net/​](http://phptester.net/) 用于 PHP，

+   ► [https://​www.​pythonanywhere.​com/​](https://www.pythonanywhere.com/) 用于 Python，

+   ► [https://​rextester.​com/​](https://rextester.com/) 提供多种语言支持，包括 C#、Haskell、Kotlin、Ruby、Pascal 和 Visual Basic。

通过搜索引擎输入“try *programminglanguage* online”（其中 *programminglanguage* 替换为你想要的编程语言名称），你可以很容易找到更多类似的平台。在大多数情况下，你甚至不需要创建账户；你可以直接开始编写代码。需要（免费）账户的网站，如 ► [https://​www.​pythonanywhere.​com/​](https://www.pythonanywhere.com/)，通常还允许你将文件保存在云端，并稍后重新使用。

像上述提到的网络服务当然不能替代真正的开发环境，因为它们通常功能非常有限，且程序的执行可能会受到限制（例如，在某些情况下，一个程序只能占用五秒钟的计算时间）。如果你想认真学习这门语言，无法避免需要在自己的计算机上安装必要的工具。不过，这些网站是一个有趣的机会，可以在没有风险和不必要努力的情况下尝试某种语言。

## 8.2 帮助与信息

拥有合适的工具并不代表一切。有时候，你会需要帮助。因此，事先考虑在哪里可以获取更多关于编程语言的信息是有意义的。例如，如果你不知道如何解决某个具体问题，不知道编程语言中的某些命令做什么或如何使用它们，或者你不理解解释器或编译器的那些有时令人困惑的错误信息。在所有这些情况下，拥有一个即时的联系点来获得支持是非常有帮助的。这样的联系点在实际工作中是一个重要的资源，不仅仅对编程初学者如此。当然，除了像这本书这样的书籍，互联网还提供了大量的资源，几乎没有信息需求是得不到满足的——当然，前提是你能找到它们。

许多编程语言，无论是开源的还是专有的（厂商特定），都有详尽的网页文档，你可以在其中找到关于编程语言特定命令的详细信息。这些帮助文档的例子有 PHP 的函数参考、Python 的库参考或微软的 Visual Basic for Applications (VBA) 参考。

官方文档的一部分通常不仅包括这样的函数参考，也就是一本类似字典的参考书，描述编程语言中的某些命令的作用及其使用方法，还常常包括语言参考。语言参考解释了该语言的语法、语法规则，从而描述了如何正确地用该语言编写指令。然而，这种语言参考并不总是容易让初学者消化的。因此，一些官方文档还会提供针对初学者的教程和“入门指南”文章，作为补充内容。

对于任何想要认真学习某种编程语言的人，建议将官方语言文档，尤其是函数参考，添加到浏览器书签中。当你想要了解某个特定命令的作用以及如何使用它时，通常这是最先要去的地方。

除了官方文档之外，当然也有一些非官方的信息和帮助渠道，这些渠道并非由负责该编程语言的组织运营。在实际应用中，许多编程语言最重要的非官方渠道就是互联网平台 Stack Overflow（► [https://​StackOverflow.​com/​](https://stackoverflow.com/)）。在这个平台上，有超过 1700 万个问题，涵盖了各种编程语言，几乎无所不包。如果你在这里搜索某个具体问题的解决方案，你常常会有这样的印象：几乎每个可以想到的问题都已经被某人提问过了。但不仅是回答问题的数量庞大和不同编程语言的广泛覆盖使 Stack Overflow 成为一个极为有用的信息来源，回答的质量通常也非常高。

高质量和高数量的内容一方面通过游戏化实现，即通过为论坛参与者提供积分（“声誉”）来激励他们参与特定行为。这些积分不仅会显示在用户名旁边作为能力的证明，还可以让用户使用一些所有用户无法使用的功能。一个重要的功能（即使是相对较低的分数也能使用）就是对回答进行投票，包括对其他用户回答的评价。这帮助读者更好地评估答案的质量。反过来，获得投票的回答者会获得声誉积分，这增加了提供高质量答案的动力。此外，提问者可以标记一个答案为最佳答案。其他用户将通过答案旁边的大绿勾标识，看到这正是最终帮助提问者解决问题的答案。答案的作者也会因此获得声誉积分。通过这种方式，不仅建立了相互质量控制的系统，还为他人付出的努力提供了强大的激励，而这种付出除了带来帮助他人的良好感觉外，什么也没有。通过 Stack Overflow，除了带来良好的感觉，你还可以获得声誉和权限，这显然对许多参与者的自我满足感有益。

除了游戏化元素外，论坛中的严格规则也在确保信息质量方面发挥着重要作用。例如，与其他问题重复或者偏离相关论坛区域的话题的问题会立即被版主关闭。提问者需要为他们的问题提供一个最小化但可执行的代码示例，并且必须在帖子的标题中准确地表述问题。Stack Overflow 自身的行为规范呼吁友好的互动，但论坛中的语气有时对 Stack Overflow 新手来说似乎有些粗鲁。

尽管语气有时需要适应，Stack Overflow 仍然是一个一流的信息来源。即使是那些难以理解的编译器或解释器错误信息——编程中常见的烦恼——通常也能在 Stack Overflow 上找到解决方案。由于 Stack Overflow 支持多种编程语言，因此在搜索时始终包括编程语言的名称非常重要。

如果你在 Google 上搜索问题，Stack Overflow 的搜索结果通常会排在前面。在 Google 搜索查询中添加“site:► [StackOverflow.​com](http://stackoverflow.com)”后，结果会只显示 Stack Overflow 的内容；当然，► [StackOverflow.​com](http://stackoverflow.com) 也有其自己的搜索功能。除了 Stack Overflow，还有许多其他论坛，包括在 Facebook 或 Reddit 等知名平台上的论坛。许多博客也提供针对特定问题的好建议和解决方案。

那么，什么时候应该使用官方文档，什么时候应该使用其他来源，比如 Stack Overflow 呢？如果你已经知道该使用哪个命令，现在只需要理解如何正确使用它，那么该语言的官方函数参考通常是最好的起点。但是如果你不知道该采取什么命令或方法来解决问题，那么 Stack Overflow（或类似的论坛）就是你的首选。在这里，你可以找到很多常见问题的解决方案。同样，如果你无法解读编译器或解释器的错误消息，或者只是无法理解为什么你在函数参考中查找的命令会以那样的方式表现，Stack Overflow 也是你该去的地方。使用 Stack Overflow 的好处在于，由于已经有大量的问题被提出，极有可能你的问题已经被问过，你可以立即获得问题的解决，而不必自己发帖并等待几个小时甚至几天才能得到一个合适的答案。

## 8.3 生成型人工智能（如 ChatGPT）

人工智能工具，如 OpenAI 的 ChatGPT、Google 的 Gemini、Anthropic 的 Claude 或 Meta 的 Llama，是一种非常不同的工具。它们建立在强大的大型语言模型（LLM）之上，并且是基于对话的，这意味着它们允许用户与人工智能进行“对话”。这使得可以提出一些目前在任何互联网论坛中都没有的问提。此外，借助 ChatGPT 等工具，繁琐的将别人提出的问题和他们收到的答案应用到自己情况中的工作被消除了，因为你可以根据自己的具体情况精确提问，并获得针对自己问题量身定制的答案。人工智能工具易于使用，因为它们以自然语言进行交流；通常，除了英语外，还支持一系列自然语言，包括西班牙语、法语、德语、意大利语和中文。

像 ChatGPT 这样的工具是生成型人工智能的例子，这意味着它们不仅能够编译和呈现已知信息，还能够——看似创造性地——生成新内容并发展新解决方案。结合其能够使用多种编程语言的能力，这些工具在编程中非常有用。它们的应用领域包括：

+   理解外部代码：如果你不理解一段不是自己写的代码（例如来自互联网论坛或博客的代码），可以让别人给你解释一下（“解释以下代码的作用”）。

+   查找资料：你可以像使用语言参考书或教科书一样使用像 ChatGPT 这样的工具。你可以非常具体地询问如何在某种编程语言中使用某个函数，也可以更一般性地询问哪些函数（以及外部插件模块）可以用来解决某个问题。好处是（特别是在前一种情况）如果你不理解答案，你可以随时请求更易懂的解释（或示例）。

+   编写代码：生成性人工智能的一个强大优点是能够编写代码本身（“编写一个 Python 程序，...”）。网络上流传着许多例子，开发者们利用像 ChatGPT 这样的工具，在短时间内、用很少的精力开发出大型应用（例如，整个 Web 平台），并且（据称）通过其商业化运作赚了不少钱。

+   查找和消除程序中的 bug：将代码和错误信息输入 AI 工具，通常能比自己艰苦地翻阅代码更快地找到 bug。◘ 图 [8.5](#Fig5) 展示了一个示例。

+   注释和文档化代码：对于大多数程序员来说，注释和文档化代码（即编写代码如何工作及如何使用的解释）是项繁琐的工作，通常可以由生成性 AI 工具来很好地完成。

生成性人工智能的结果质量通常非常好，尤其对首次使用者来说，给人留下深刻印象。然而，像 ChatGPT 这样的工具并非没有错误。结果始终需要检查，AI 工具编写的代码需要彻底测试。仅此一点，掌握所用编程语言的知识是必不可少的。然而，由于这些系统是基于对话的，并且可以参考之前的输入和输出，你可以指出错误并要求 ChatGPT 进行修正。即使工具没有犯真正的错误，但结果仍然不符合你的想法和要求，你也可以通过与 AI 工具的对话让其“精炼”一次。此外，由于过程的对话性，你可以一步步地开发复杂的程序，这增加了最终得到所需结果的概率。由于 Chat GPT 的基础版本是免费的，强烈建议尝试一下。不要担心这会让你看起来像个业余爱好者，许多专业软件开发人员也使用这种工具来提高他们的编程生产力。![](../images/474412_1_En_8_Chapter/474412_1_En_8_Fig5_HTML.png)

截图展示了一个匿名用户提出的关于代码错误信息的提示，ChatGPT 的响应以段落形式呈现。

图 8.5

使用 ChatGPT 调试

## 8.4 学习新编程语言的路线图

当你学习一门新的编程语言时…… *首先获取必要的工具，特别是所需的编译器或解释器，以及一个可以用来编写代码的工具（代码编辑器或 IDE）。*

+   如果你已经在使用一个代码编辑器或 IDE 来编写其他语言的代码，可以考虑将它用于新语言，因为你已经熟悉它的操作。也许你的工具有适用于新语言的扩展包。

+   如果你还没有使用代码编辑器或集成开发环境（IDE），可以尝试不同的工具。如果你编程语言的工作需要特定功能，比如设计图形界面，或者你想要集中的使用调试工具，建议选择 IDE 而不是纯粹的（代码）编辑器。否则，一个好的代码编辑器，能够调用编译器或解释器，可能就足够了。

+   当你安装一个新的代码编辑工具时，不要急于立刻理解所有功能的复杂性。反正你在最开始只需要其中的相对小部分——至少一开始是这样——才能真正开始工作。首先专注于理解如何打开、编辑和保存代码文件，以及如何运行你的程序。之后，你可以立即开始编程。你会在日常使用过程中顺便学习更多关于你的集成开发环境或代码编辑器的知识。

+   在真正开始学习编程语言之前，了解可用的官方帮助和信息渠道；特别是，为官方函数和语言参考设置浏览器书签。

+   检查一下，ChatGPT 是否支持你的语言，并尝试做一些实验。