© 作者（们），专有许可给 Springer Fachmedien Wiesbaden GmbH，属于 Springer Nature 2024 J. L. Zuckarelli 用 Python 和 JavaScript 学习编程 [`https://doi.org/10.1007/978-3-658-42912-6_20`](https://doi.org/10.1007/978-3-658-42912-6_20)

# `20. 语法、注释、代码风格与文档：如何确保我（以及他人）以后还能理解我的程序？`

Joachim L. Zuckarelli^([1](#Aff2) )(1) 德国慕尼黑 概述

在我们真正开始学习 Python 编程之前，我们首先会了解一下 Python 代码及其最重要的基本元素是什么样的，以及编写代码时必须遵守哪些基本约定。与许多其他编程语言相比，Python 在代码设计上有一个特殊的特点，乍一看，这似乎会剥夺我们作为程序员的一些设计自由，但同时也使我们的生活变得更加简单。

此外，我们还将了解 Python 代码是如何被`注释`和`文档化`的。注释很重要，因为它可以让我们作为开发者以后还能理解自己的代码，特别是在我们想要进一步开发时。文档化用于提供信息，以便其他想要在他们的程序中使用我们代码的开发者能够准确理解如何使用。

在本章中，你将学习：

+   Python 中行缩进的意义

+   如何在 Python 中终止语句，以及如何将语句扩展到多行

+   Python 中变量、函数、方法和模块的标识符通常是如何选择的，以及在选择时有哪些限制

+   如何在 Python 中书写注释

+   什么是文档字符串（docstrings），以及如何使用它们来记录程序代码。

## `20.1 程序代码的设计与命名约定`

### `20.1.1 缩进和代码格式化的一般规则`

我们在 ► 第 [`10.​2`](474412_1_En_10_Chapter.xhtml#Sec2) 节中看到，许多编程语言给予开发者在源代码格式化方面很大的自由。例如，通过选择合适的缩进，可以让程序代码更加清晰。这种设计自由最终源于许多编程语言完全忽略程序代码的格式化。换句话说，格式化对程序的内容没有意义。

在 Python 中是不同的。其他编程语言使用特殊符号来标记代码块的开始和结束（例如，`begin` 和 `end`，或打开和关闭的大括号），而 Python 使用缩进。缩进相同的语句属于同一个代码块。

这里有一个简单的函数示例，你可以传递一个文本和重复次数，它将简单地将文本以大写形式输出到屏幕上，并宣布当前的重复次数。别担心你可能还不理解所有的代码，你将在本书的后面部分明白的。现在这里只关心缩进：

`def` repeat_text(`text: str`, `reps: int`):`text = text.upper()` `for` `x` `in` `range(1, reps+1):` `output = 'Run no.' + str(x) + ': ' + text` `print(output)` `repeat_text('Hello world', 3)`

在用`def`创建函数之后，最后一行调用了这个函数。该程序通过这个函数调用生成如下输出：

`Run No.1: HELLO WORLD` `Run No.2: HELLO WORLD` `Run No.3: HELLO WORLD`

你可以看到，`repeat_text()`函数的代码块是缩进的。`for`循环中执行的代码块也是缩进的，并且它的缩进程度更深，说明它属于`repeat_text()`函数，并且在该函数中属于`for`循环`for x in range(1, reps+1):`。在函数定义结束后，`repeat_text('Hello world', 3)`又回到最左边。这个语句不属于`for`循环的代码块，也不属于函数定义的代码块。

所以，Python中的代码块是通过缩进来限定的（并通过冒号引入，正如你在`def`关键字的函数定义和`for`循环中看到的）。缩进通常使用Tab键或输入四个空格来实现。第二种方法通常更受推荐。为了代码的一致性，你尤其不应在一个程序中混用这两种缩进方式。由于强制缩进，Python代码的可读性非常高，因此设计自由度的丧失是可以接受的。通过这种方式限定代码块，避免了使用括号或其他关键字的需要，尤其是在代码块结束时遗漏这些符号是其他编程语言中常见的错误来源。除了缩进，你在设计代码时完全自由。

然而，在样式指南的形式中，关于如何编写Python代码有一整套建议和推荐。遵循这些建议有助于使代码更具可读性和可理解性。但许多规则非常详细，甚至Python专家也未必总是遵循。官方的样式指南可以在► [python.​org](http://python.org)网站上找到，作为一个`Python Enhancement Proposal`（PEP），其编号为PEP 8。去看看那里也没有坏处。

如果你正在使用`PyCharm`，从“代码”菜单中的方便的“格式化代码”功能可以让你根据PEP 8规则自动格式化代码。此外，`PyCharm`会通过波浪形的灰色下划线和小提示框警告你“违反”PEP 8规则，就像在◘图[20.1](#Fig1)中看到的那样。 ![](../images/474412_1_En_20_Chapter/474412_1_En_20_Fig1_HTML.jpg)

一组程序代码和一个提示框插入的截图。文本字符串和整数`reps`的重复文本在`for`循环语句中一起定义。一个PEP 8块覆盖在程序上。

图 20.1

代码格式化的提示框插入

### `20.1.2`没有分号的语句结束，跨越多行的语句

`Python`一般不需要像分号这样的分隔符在语句末尾。每条语句在行末会自动结束。尽管不建议这样做，因为会减少清晰度，你也可以在`Python`中将几条语句写在同一行中。然而，在这种情况下，你必须用分号分隔每个语句。

相反，也有可能将指令扩展到多行。如果语句非常长，这样做是有意义的。当然，你也可以简单地将语句写在一行中。然而，你可能需要横向滚动才能看到语句的结尾。这是非常不方便的，应该避免。根据`PEP 8`的代码样式建议，代码行不应超过79个字符。然而，有些语句实在太长。那么，应该怎么办呢？

语句可以很容易地在圆括号、方括号或花括号内换行：

`repeat_text('Hello world', 3)repeat_text('Hello World',3)`

我们也可以将上面例子的函数调用分成两行。然而，不允许在字符串`'Hello world'`内部换行！缩进在这里没有规定，因此你可以随意缩进，这可以大大提高程序代码的可读性。

但是你也可以通过在行末放置反斜杠（`\`）来在圆括号、方括号和花括号之外换行：

`x = 'Hello World'print(x)`

然而，这种方法是不被推荐的，应该仅在绝对必要时使用。大多数情况下，换行是因为函数调用中有很多函数参数，而在这种情况下，你无论如何都在圆括号内部。

最后一种包装语句的类型是`docstrings`，或者更一般地说，是用三重引号括起来的字符串（我们将在►节`[20.3](#Sec6)`中更详细地处理`docstrings`）。这些可以跨越多行：

`x = '''这是一个非常长的文本，无法放入一行，因此必须分成几行。'''`

“正常”字符串不能这样做。如果我们让字符串跨越行尾，`Python`解释器会认为我们忘记结束字符串，这会导致错误消息：

`SyntaxError: EOL while scanning string literal`

### `20.1.3`区分大小写和标识符选择

`Python`是区分大小写的，这意味着一般区分大小写。因此，一个名为`age`的变量与变量`AGE`是完全不同的。当然，区分大小写不仅适用于变量，还适用于函数和方法、类、模块和包的标识符。

所有这些元素的标识符可以由字母、数字和`_`组成。然而，它们绝不能以数字开头。`customer_age`因此是一个合法的变量名，`take2`和`_2times4`也是，但`11friends`则不是。以`_`（或两个`__`）开头和/或结尾的标识符在Python中具有特殊意义，我们稍后会详细讨论。一般建议避免以`_`开头或结尾的标识符，并且只在标识符`内`使用下划线，除非你想要与前导或尾随下划线相关联的某种效果。

除了这几条规则外，你可以自由选择你的标识符。然而，有一些约定是许多Python程序员遵循的，尽管违反这些规则不会导致程序代码中的语法错误。遵循这些规则会使你的代码看起来更“pythonic”。例如，类名或其组成部分通常以大写字母开头（例如，`MyClass`），模块名以小写字母开头（例如，`myModule`），变量和函数/方法通常以小写字母开头，不同的组成部分通常用下划线分隔（例如，`my_variable`、`my_function`）。

顺便提一下，你甚至可以在标识符中使用像变音符号这样的特殊字符。Python支持广泛的UTF-8字符集，这使得这一点成为可能。然而，这种标识符并不推荐。至少，与那些母语（和键盘！）不包含这些字符的开发人员交换代码时会变得更加困难。最好坚持使用可以在标准英语键盘上轻松输入的标识符。

当然，你不必遵循所有这些非约束性的约定。但如果你这样做，你的代码看起来会更“Python”，其他开发人员也会更容易与你的代码相处，特别是因为他们可以专注于代码的含义和功能，而不是经常被他们不习惯的标识符样式“卡住”。

## 20.2 注释

正如你已经知道的，注释是程序代码的一部分，它们被解释器简单地忽略，你可以用它们为自己或他人阅读程序代码留下备注和解释。这些注释以井号（`#`）引入。井号右侧的所有内容都被视为注释。注释符号不一定必须位于行的开头。在下面的示例中，你可以看到两种变体，一种在行首，一种在右侧：

`# 我们的第一个小Python程序` `print('Hello world')` `# 屏幕输出`

那些在行中间开始的注释也叫做`内联注释`。它们在Python中不太受欢迎，在大多数（如果不是全部的话）编程语言中也一样，因为它们会使代码稍微难以阅读。如果你使用它们，应该确保在实际代码行的结尾和注释符号之间留出一些（官方推荐：两个）空格。

当然，你也可以通过注释临时“关闭”程序代码，将其移出解释器的处理范围，解释器会忽略注释符号右侧的所有内容。在这种情况下，通常说的是`注释掉`。这正是这个例子中第二个打印语句发生的情况：

`# 我们的第一个小Python程序` `print('Hello World')` `# print('Hello, world')`

注释总是扩展到行尾；Python原则上不支持多行注释。所以，如果你想写多行注释——你有时会需要这样做，因为你的注释应该能够在正常屏幕上完全可读，即使不横向滚动（官方推荐每行最多79个字符）——你必须在每一行前加上额外的注释符号。不过，许多开发环境会为你完成这项工作。如果你使用`PyCharm`，你可以选中你想注释的行，然后点击代码菜单中的“使用行注释”选项（或者按`<CTRL>`和`</>`键组合），`PyCharm`会在每行代码的开头添加注释符号。你也可以使用相同的选项来移除注释符号，解除注释。除此之外，还有一个技巧，你可以用来创建类似真正的多行注释。更多内容请参见下一节。

关于注释的意义和无意义是可以哲学化讨论和争论的，特别是关于何时注释是有帮助的，何时注释只是让代码变得更加冗长，从而降低代码的清晰度的问题。回到几页之前，► Sect. `[10.​3](474412_1_En_10_Chapter.xhtml#Sec3)`，我们学习了许多关于注释程序代码的最佳实践。一般来说，我们可以这么说：注释通常不够，所以尽管写注释；你的“未来自己”在尝试理解你旧代码时会感谢你的！

有时你也会直接在程序代码的适当位置使用注释来记录待办任务。如果你使用`PyCharm`，你可以在这些注释前加上`# TODO`：

`# TODO: 在这里添加更多语言`print('Hello World')print('Hallo Welt')类似地，你可以在适当的代码位置标记和解释那些仍需修复的小错误，使用`# FIXME`。以这种方式开始的注释会被语法高亮特别标出，并且在`PyCharm`中会被特殊处理。`PyCharm`会在一个特殊的侧边栏面板中显示这些注释，这个面板叫做`TODO`，如图◘ [20.2](#Fig2)所示。所有的`TODO`和`FIXME`注释都会显示在这里；双击`TODO`区域中的某一条目，将直接跳转到对应的代码位置。如果你看不到`TODO`面板，可以点击侧边栏中的三个点，查看当前隐藏的区域。 ![](../images/474412_1_En_20_Chapter/474412_1_En_20_Fig2_HTML.jpg)

一张Python项目中9行“Hello World”程序代码的截图。`Todo`面板在底部显示了注释。

图 20.2

`PyCharm`中的TODO面板

如果你愿意，也可以通过`PyCharm`的设置定义你自己的注释类型，类似于`# TODO`和`# FIXME`。然而，在绝大多数情况下，前面提到的这两种特殊注释类型应该足够了。

## 20.3 使用`Docstrings`进行文档编写

除了“真正的”注释，它们总是以注释符号`#`引入之外，还有第二种可能性，可以将信息存储在代码中而不被解释器执行，即通过所谓的`docstrings`。`Docstrings`是用三引号括起来的特殊字符串。考虑以下程序作为示例：

`'''这是我们hello world程序的docstring，即一个甚至跨越多行的docstring。'''print('Hello world!')`

如果你运行这个程序，你将得到输出`Hello world!`。另一方面，`docstring`是不会显示的。

让我们试试其他方法：这次我们不使用三引号的docstring，而是使用一个普通的字符串，类似于`'Hello world!'`，我们在下面输出它。与docstring不同，Python中的普通字符串不能跨越多行程序代码，所以我们把‘注释’放在了一行。现在当你运行这个程序时会发生什么？什么也没变！再次，只有`'Hello world!'`被输出。原因很简单：每当你将文本写入Python程序代码时，正如我们最初用docstring，然后用普通字符串那样，这不会导致屏幕上的任何输出。相反，文本只是被忽略了（技术上不完全正确，但至少没有可见效果）。变量也是如此，正如你将在下一章看到的。如果我们只是简单地将变量名输入程序代码中而没有任何进一步的指令，什么也不会发生。为了显示变量的内容，或者仅仅显示上面示例中的文本，我们必须明确告诉Python输出它。我们通过调用`print()`函数来做到这一点。控制台中有所不同。如果你在那里输入变量的名称并按`<ENTER>`，其内容会被显示。如果你在控制台输入字符串，字符串会立即再次显示在控制台中。

所以，像其他所有字符串一样，docstring如果在程序代码中没有其他指示，是不会在屏幕上显示的。如果是这样，我们不能只使用普通字符串来解释代码吗？是的，这样也可以。然而，docstring有两个特殊属性，使它们特别适合用于文档化程序代码，正如它的名字所示：首先，它们可以跨越多行：我们已经看到了这一点。其次，Python以特殊的方式对待这些docstring。如果它们位于函数、类定义或模块的开始处，它们将作为该函数、类或模块帮助文档的内容。如果你调用`help()`函数（例如，对于`print()`：`help(print)`），你将看到存储在相应程序代码开始处的docstring。

有许多 Python 工具可以处理这些文档字符串，并将其输出为文档形式。Python 自带的帮助系统使用了一个叫做`pydoc`的工具，它会从代码中提取文档字符串，并在调用`help()`时显示它。此外，还有一些其他工具也可以处理文档字符串，例如`autodoc`、`doxygen`和`pydoctor`。其中一些程序是专门为 Python 设计的，其他的一些则允许为不同编程语言自动生成代码文档。这些文档的输出不仅限于 Python 控制台中的文本。许多工具还支持生成 HTML、PDF，甚至 LaTex 格式的文档。为了清晰地结构化文档，一些工具要求文档字符串遵循特定的结构。

当然，聪明的头脑早已考虑过文档字符串应该是什么样子的。对此问题的官方回答可以在`Python 增强提案`（PEP）中的`PEP 257`（《文档字符串规范》）中找到。

与注释不同，文档字符串更多是用于为`其他用户`文档化代码，即解释如何`使用`代码来达到自己的目的，而不是记录代码如何`工作`。通常，注释才是用于记录代码实现细节的地方。我们将在后面的部分回到文档字符串，并在程序中使用它们。

我们还将更深入地了解另一种类型的文档。即`函数注解`，它允许你记录函数参数的预期数据类型，以及程序代码中函数的返回值数据类型。这些注解也会被`pydoc`用于帮助文档，并且可以被其他文档工具处理。

文档字符串和`函数注解`通常是面向除你之外的其他读者，也就是你的代码的`用户`。当编写 Python 代码供其他开发者使用时，重要的是记录下函数的作用、参数的含义，以及使用你代码的开发者可以期待的返回值。他们不希望通过阅读你的代码来了解这些信息。因此，提供文档以便第三方（如果有提供的话）可以“盲目”地使用你的程序代码，并像黑盒一样查看其内部工作原理，这是非常重要的。对于你的代码的用户来说，重要的只是`接口`，即如何使用它，而不是它的详细实现原理。文档字符串和`函数注解`是适合这种目的的工具。

## `20.4 总结`

在本章中，我们探讨了 Python 在格式化程序代码方面的特殊特点，标识符（例如变量和函数/方法）如何/必须进行结构化，以及如何注释和文档化你的程序代码。

你应该从本章中记住以下几点：

+   在Python中，缩进标识了一个连贯的代码块，因此不能随意使用；可以说，Python“强制”程序代码采用易读的格式。

+   语句通常在Python中以行末结束，无需特殊分隔符。

+   语句可以跨越多行，如果换行出现在圆括号、方括号或大括号内部，或者通过反斜杠（`\`）特别标记，虽然后一种换行方式相对较少见。

+   多个语句可以通过分号在一行中分隔。

+   Python在定义变量或标识符时是区分大小写的。

+   标识符可以由字母、数字和下划线组成。

+   与数字不同，字母和下划线也可以出现在标识符的开头。

+   由于标识符开头（以及结尾）的单个和双下划线具有特殊含义，因此一般应避免使用以下划线开头的标识符。

+   变量和函数/方法的标识符通常用小写字母书写，在Python中，如果它们是复合词，其组件之间用下划线分隔。

+   解释代码的注释在Python中总是单行，并由注释符号`#`引入；其右侧的内容不会被解释为程序代码，而是被解释器忽略。

+   `Docstrings`用三重引号括起来，用于在Python中为代码用户提供文档；它们是Python帮助的核心部分，可以通过`help()`调用，并且被众多开发工具进一步处理为各种格式的文档。

+   `Docstrings`可以跨多行。