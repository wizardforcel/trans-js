© 作者，Springer Fachmedien Wiesbaden GmbH 独家许可，Springer Nature 2024 J. L. Zuckarelli 《使用 Python 和 JavaScript 学习编程》[`https://doi.org/10.1007/978-3-658-42912-6_22`](https://doi.org/10.1007/978-3-658-42912-6_22)

# `22. 用户界面：如何输入和输出数据？`

Joachim L. Zuckarelli^([1](#Aff2) )(1)慕尼黑，德国 概览

我们已经广泛讨论了程序中数据的组织方式，即使用的变量和对象。现在是时候讨论如何从用户那里接收数据并将其输出回去了。为此，在本章中我们将首先讨论最简单的输入和输出方式，即通过 `控制台`。之后，我们将通过 `图形用户界面`（GUI）使我们的程序看起来更加吸引人。我们不仅将通过一个完整的应用程序示例更深入地了解如何使用 GUI，还将有机会在练习中编写你自己的第一个 GUI 应用程序。最后，我们将讨论如何与 `文件` 打交道，这在实际操作中非常重要。

在本章中你将学习：

+   如何将信息输出到控制台以及如何在控制台中查询用户

+   如何使用 Python 库 `tkinter` 为你的程序提供图形用户界面

+   可用的控件有哪些，它们如何配置、放置以及在界面上排列

+   如何在程序代码中响应用户通过界面触发的事件（例如，点击按钮时）

+   如何从文件中读取数据以及如何向文件写入数据。

## `22.1 控制台中的输入和输出`

在前面的章节中，我们已经看到两个最重要的函数，它们用于在 Python 控制台中输入和输出数据，`input()` 和 `print()`。

`输入`

`input(prompt)` 显示一个提示并允许用户从键盘输入，通过按下 `<RETURN>` 或 `<ENTER>` 键来完成输入。然后，`input()` 会将输入作为返回值返回，并始终以字符串形式返回。这一点很重要，特别是当你期望输入的内容是数字，之后用于计算时。在这种情况下，你必须首先显式地将 `input()` 的返回值转换为数字，正如我们在 ► 第 `21.5` 节 中所做的那样。

`输出`

输出信息的最重要工具是`print()`函数。它可以用于打印一个或多个对象。如果要打印多个对象，可选的字符串参数`sep`决定了输出中各个对象之间如何分隔；默认情况下，这些对象通过空格字符分隔。可选的`end`参数控制输出的结束部分；除非另行指定`end`，否则会在输出的末尾添加换行符。换行符由转义序列`'\n'`表示（用于*新行*），我们已经在► Sect. [11.​2.​2](474412_1_En_11_Chapter.xhtml#Sec4)中与字符串一起学习过这个内容。当然，我们也可以在想要输出的字符串中直接使用这些转义序列：考虑以下小程序作为例子：

`user = input('用户名：') pwd = input('密码：') print('欢迎，', user, '!\n你的密码是：', pwd)` 在这里，我们从用户那里读取用户名和密码，然后输出总共四个对象：

+   字符串`'欢迎，'`

+   字符串变量`user`

+   字符串`'!\n 你的密码是：'`（注意：这个字符串在感叹号后面包含了换行符！）

+   字符串变量`pwd`。

如果你现在调用程序并输入`peter`和`889X!z5`作为用户名和密码，你将看到以下输出：欢迎，`peter`！你的密码是：`889X!z5`

用户名`peter`和感叹号之间的空格看起来有点不太美观。这是由于`sep`参数的默认值为空格。正因为如此，要输出的两个对象，即变量`user`和以感叹号开头的字符串，被空格隔开了。为了避免此类问题，建议控制空白字符的输出，并将`sep`参数设置为空字符串，这样`print()`函数就不会自动输出分隔符。此时，`print()`的调用方式可以是这样的：

`print('欢迎，', user, '!\n你的密码是：', pwd, sep = '')`

如果你将此与上面的调用进行对比，你会发现我们在每个需要输出空格的地方插入了一个空格，并且为`sep`参数提供了一个空字符串。请注意，`sep`参数必须始终使用其名称调用，否则`print()`函数无法判断最后一个字符串是否仍然属于要输出的对象，或者它是否具有特殊含义，即它已经代表了*函数的下一个参数*，就像在我们这个例子中一样。因此，我们将`sep`作为*关键字参数*来调用。更多内容请参见► Sect. [23.​1.​2](474412_1_En_23_Chapter.xhtml#Sec3)。

当然，通过`print()`打印的对象不一定只有字符串。实际上，您可以使用`print()`打印几乎任何对象，甚至可以在同一个`print()`调用中包含不同类型的对象，即不同类的对象。这也适用于您自己定义的类。那么这怎么实现呢？比如，`print()`是如何知道如何显示一个`Product`类型的对象的呢？答案很简单：Python中的类可以有一个特殊的`__str__()`函数。当该类的对象需要输出时，`print()`会调用这个函数。作为类的开发者，您可以指定对象应该如何表示。您只需要定义一个`__str__()`方法即可。我们将在►节[23.2](474412_1_En_23_Chapter.xhtml#Sec6)中看一个例子。

22.1`[5分钟]`

指定三种不同的方式，将三条字符串表达式`'First line'`、`'Second line'`和`'Third line'`输出到连续的三行中。

## 22.2`使用Tkinter创建图形用户界面`

### 22.2.1`概述`

命令行程序或Python控制台程序并不是每个人的“茶”。尤其是如果您为非技术用户开发软件时，您根本无法绕过图形用户界面。因此，在本节中，我们将讨论如何用可管理的工作量在Python中设计图形用户界面，并如何为其添加程序功能。Python中有多种设计图形用户界面的方法。例如，使用`Streamlit`库，您可以使用Python创建动态网页，并且这些网页也可以托管在Web服务器上。本章我们将重点讨论在本地客户端（例如您的计算机）上运行的应用程序。

以图形计算器为例，您将看到，通过仅仅几行代码，您就可以编写一个有用的、功能完备的程序，拥有一个不强迫用户坐在黑色控制台前并固执地跟随给定程序流程的吸引人界面。本章最后将有一个练习，您将在其中开发自己的简单文本编辑器，允许您打开、编辑和保存文本文件。

有许多不同的库和框架用于开发图形界面。它们中的许多都是跨平台的，这意味着您用它们开发的程序可以在不同的计算机（有时是移动）操作系统上运行。我们将使用的一个常用库是`tkinter`。方便的是，它是Python的标准库，因此我们不需要安装额外的东西。`tkinter`是基于`Tk`的，这是一种用于图形用户界面的跨平台库，最初是在1990年代初期用一种名为`Tcl`的编程语言开发的。`Tcl`主要因`Tk`库而流行。这是因为它不仅适用于Tcl本身，而且适用于大量其他编程语言，包括Python。

Python提供了一个名为`tkinter`的包，它最终是一种与`Tk`的“连接”。要使用`Tk`库，Python调用一个Tcl解释器，该解释器也是标准Python安装的一部分。因此，实际上，您间接地使用了另一种编程语言，但您不需要理解Tcl语法或自己调用Tcl解释器。相反，您可以在Python中工作，并使用常规的Python语法。在必要时，Python会将您的语句“翻译”成Tcl代码并调用Tcl解释器。关于`Tk`的实用之处在于，一旦您理解了这个库的工作原理，您可以快速在支持`Tk`的其他编程语言中开发自己的图形用户界面——而这些语言有不少——而不会遇到任何重大转换困难。

在下一部分中，我们将编写一个简单的`Hello World`程序，该程序将在屏幕上打开一个窗口。之后，我们将仔细查看用户界面的各种图形控件，即`widgets`，如按钮、输入框和复选框。之后，我们只需再缺少两个组件。我们需要将这些元素按我们希望的方式排列在界面上，以便获得所需的界面外观。最后，我们必须将控件与背后的程序代码连接起来，以便它们能对用户的操作做出适当反应。这使我们拥有编写具有适当图形界面的Python程序所需的一切，比如我们将在`tkinter`介绍结束时开发的计算器。但让我们先从小事开始！

### 22.2.2 你好，Tkinter！

创建一个新的Python文件，包含以下程序代码并运行该程序：

`from tkinter import win = Tk() win.title('Hello World Program') win.geometry('900x500') win.mainloop()` 打开一个窗口，外观类似于◘ 图 [22.1](#Fig1)。![](../images/474412_1_En_22_Chapter/474412_1_En_22_Fig1_HTML.jpg)

窗口中显示的文本为“Hello world program”的截图。

图 22.1

一个`Hello World`程序与`tkinter`

窗口仍然非常空，但在接下来的部分中这一点将很快改变。

如果仔细查看代码，你会发现它以`import`语句开始。这是必要的，以使模块 `tkinter` 可用。你不必担心此时`import`语句的具体结构，因为我们将在► 第23.3节（[链接](474412_1_En_23_Chapter.xhtml#Sec7)）中更详细地讲解模块的导入。此时，了解`import`语句使得`tkinter`模块的类，特别是`Tk`类，能在我们的程序中使用就足够了。

我们在程序中创建了`Tk`类的一个实例，即对象`win`，它是我们应用程序的主窗口。通过方法`title('titletext')`和`geometry('dimensions')`，我们设置了两个重要的属性：窗口的标题和窗口的尺寸（像素）。然后，使用`mainloop()`方法，我们将窗口显示在屏幕上，并开始事件处理；我们的程序现在可以响应用户的操作了。我们的第一个`tkinter`程序完成了！很简单，对吧？不过，用户仍然无法做太多事情。所以，我们需要控件，允许用户进行输入并触发操作。这些控件在`Tk/tkinter`中被称为`*widgets*`。我们将在下一部分讨论它们。

### 22.2.3 图形控件（Widgets）

在这一部分，我们将看一些重要的控件。以第一个控件——按钮为例，你将看到控件是如何创建的，以及它们在创建时（或稍后）如何调整其属性。

#### 22.2.3.1 按钮（类 `Button`）

按钮作为`tkinter`中的`Button`类内建。它们用于让程序的用户触发操作。像所有控件一样，它们可以通过其构造方法轻松创建。将上一个部分的程序扩展以包含此构造调用，代码将如下所示：

`from tkinter import win = Tk() win.title('Hello World Program') win.geometry('900x500') mybutton = Button(win, text = 'Press me') mybutton.pack() win.mainloop()`

`Button()` 构造方法接收一个窗口作为函数参数，该窗口是我们希望放置按钮的地方，在我们的例子中是 `win`。可以指定按钮的设计选项；在我们的示例中，我们通过 `text` 选项给按钮命名为“Press me”。当然，我们在创建按钮后仍然可以修改按钮的属性，*但是*这些属性并不是 `Button` 类的普通可编辑属性，而是通过一个名为 `config()` 的特殊方法来修改的。与构造函数类似，`config()` 方法接受键值对，其中键是要修改的选项名称，值是要分配给它的值。例如，如果我们想要修改按钮的宽度，我们可以按如下方式调整 `width` 选项：

`mybutton.config(width = 50)`

也可以对 `text` 选项进行相同的操作，即按钮的标签。

修改选项的第二种方法是像访问字典一样访问它们，字典的键就是选项名称：

`mybutton['width'] = 50`

那么，问题是有哪些设置选项可用呢？要找出这些，你应该查看 `tkinter` 类的帮助文档。为此，首先需要从 `tkinter` 模块中导入 `Button` 类（或者像下面所做的那样导入所有类）到控制台中（记住：你的 Python 程序和控制台使用的是不同的命名空间；即使你已经在 Python 程序中导入了该模块，也不意味着你可以在控制台中直接使用它。因此，在调用 help 函数之前，你仍然需要在控制台中执行一次 `import` 语句）：

`>>>` 从 `tkinter` 导入 `>>>` help(`Button`)

帮助文本最上方显示了以下信息：

| 标准选项 || activebackground, activeforeground, anchor, | background, bitmap, borderwidth, cursor, | disabledforeground, font, foreground | highlightbackground, highlightcolor, | highlightthickness, image, justify, | padx, pady, relief, repeatdelay, | repeatinterval, takefocus, text, | textvariable, underline, wraplength || 小部件特定选项 || command, compound, default, height, | overrelief, state, width

如你所见，一方面有许多 `标准选项` 是大多数小部件通用的，另一方面则有一些仅适用于按钮的特殊选项。不幸的是，帮助文档没有描述每个选项控制的内容以及这些选项如何使用。此外，`tkinter` 包的“官方”文档（► [https://​docs.​python.​org/​3/​library/​tk.​html](https://docs.python.org/3/library/tk.html)）的帮助有限，尤其是对于初学者而言。然而，互联网上有许多页面以通俗易懂的方式解释了这些功能，目前例如 ► [https://​www.​tutorialspoint.​com/​python/​tk_​button.​htm](https://www.tutorialspoint.com/python/tk_button.htm)。

◘ 表格 [22.1](#Tab1) 显示了大多数控件（如果不是所有控件）的一些选项的概览。该表格还解释了编码颜色和使用字体格式的过程，这些可以在 `tkinter` 中许多地方使用。表格 22.1

`tkinter` 控件的标准属性

| Option | Type | Meaning |
| --- | --- | --- |
| `activebackground/activeforeground` | `Str` | 控件激活时（例如点击按钮时）控件的颜色（背景）或其上的文本颜色（前景）。像 `tkinter` 中所有的颜色一样，你可以指定多个预定义的颜色常量之一（例如 `'green'` 或 `'purple'`；你可以快速在互联网上找到这些颜色常量的列表），或者使用红绿蓝（RGB）编码值，格式为 `'#RRGGBB'`，其中 `RR`、`GG` 和 `BB` 分别表示颜色的红色、绿色和蓝色部分的十六进制编码值。最好的做法是使用互联网上的转换器将十进制值转换为十六进制系统。红色的值（R = 255，G = 0，B = 0）将变为 `'#FF0000'`，因为 `FF` 在十六进制系统中表示数字 255。 |
| `background/foreground` | `Str` | 控件的默认颜色（背景）或其上的文本颜色（前景）。 |
| `border` | `Int` | 控件边框的厚度，单位为像素（`border=0` 表示没有边框）。 |
| `cursor` | `Str` | 当鼠标指针悬停在控件上时，鼠标光标的形状；例如 `'hand2'`（手形）、`'watch'`（沙漏）、`'cross'`（十字）、`'left_ptr'`（“正常”鼠标指针，左上角为箭头）。互联网上也有一些列出了可用的指针样式。 |
| `font` | `Font` | 控件的字体格式；如果你想偏离默认字体，必须添加一个额外的 `import` 语句，然后使用 `Font()` 构造函数创建一个新的 `Font` 对象：`from tkinter.font import font = Font(family = 'Times', size = 36, weight = 'bold', underline = 1)` 之后，新的 `Font` 对象 `font` 可以被赋值给控件的 `font` 选项：`mybutton['font'] = font` `family` 是字体标识符（例如 `Helvetica`，`Courier`）。`weight` 区分 `'bold'` 和 `'normal'`。此外，你还可以使用 `slant` 选项（在上面的示例中未使用），用来设置文本为斜体或非斜体（`'normal'`）。`overstrike`，它可以像 `underline` 一样取值为 1 和 0（或 `True` 和 `False`），用于删除文本。你可以通过 `config()` 方法修改你的 `Font` 对象，就像修改控件一样：`font.config(weight = 'normal')` 这种方式做的更改会自动影响*所有*最初将现已更改的 `Font` 对象分配给其 `font` 选项的控件。 |
| `padx`, `pady` | `int` | 控件中文本（或图像）的缩进，左/右（`padx`）或上下（`pady`）。 |
| `relief` | `str` | 控件的 3D 表现形式。这里可能的值有：`'raised'`（凸起，默认值）、`'sunken'`（凹陷）、`'flat'`、`'groove'`（凹边）和`'ridge'`（简单边框，否则为平的） |
| `text` | `str` | 控件的标签文本 |

◘ 表 22.2（#Tab2）列出了 `special` 按钮选项的一些内容。在接下来的章节中，关于其他小部件，你会找到类似的表格，列出该小部件的最重要特定属性。表 22.2

按钮小部件的特殊属性

| 选项 | 类型 | 含义 |
| --- | --- | --- |
| `command` | `function` | 用户点击按钮时执行的函数。我们将在 ► 第 22.2.5 节 中详细介绍事件处理 |
| `default` | `int` | 如果 `default = 1`，则按钮是默认按钮（当用户按 `<ENTER>` 键时触发） |
| `height/width` | `int` | 按钮的高度/宽度。如果按钮上显示文本，则以字母高度为单位；如果显示图片，则以像素为单位。如果未指定，则宽度和高度会自动计算 |
| `state` | `str` | 按钮可以设置为 `'normal'`（可点击）或 `'disabled'`（灰显）。如果按钮当前被点击，`state` 的值将是 `'active'` |

我们刚才已经看到一些选项，它们部分像字典一样工作。因此，你也可以使用 `keys()` 方法来读取键，从而得到选项的名称。如果在创建小部件实例后，你在程序代码中加入 `print(mybuttons.keys())` 语句，当你运行程序时，控制台会显示所有可用选项的名称。如果你调用没有参数的 `config()` 方法，你会得到包含所有名称-值对的完整字典。你也可以这样输出：`options = switch.config()` `print(options)`

通常，像 `relief` 选项中的小写字符串值（例如 `'sunken'`）也可以通过预定义的常量来控制，这些常量通常是大写的，例如我们示例中的 `SUNKEN`。但在接下来的内容中，我们将常常使用字符串而不是常量。如果你想使用常量，可以在硬盘的 `tkinter` 目录中查找 `constants.py` 文件，其中定义了这些常量。要使用它们，请在程序中添加以下导入语句：

`from tkinter.constants import *`

到目前为止，我们甚至没有提到 `pack()` 方法的调用，这是我们偷偷加入程序中的一行代码。这个语句首先使按钮在屏幕上可见（注释掉这一行，再次运行程序看看会发生什么！）。使它可见与小部件在图形界面上的布局密切相关。我们将在 ► 第 22.2.4 节 中更详细地讨论这个问题。此时，我们需要做的只是调用 `pack()`，使控件在界面上显示出来。

#### 22.2.3.2 菜单（`Menu` 类）

菜单可以通过`tkinter`非常容易地设计。为了实现这一点，我们首先为窗口创建一个新的菜单栏，即上例中的`Tk`对象`win`。在`tkinter`中，菜单栏由`Menu`类表示。要将菜单栏附加到的窗口已作为参数传递给该类构造函数的调用。相反，我们通过`Tk`对象的`menu`选项显式地将新的菜单栏分配给窗口，这样它就能在之后显示出来：

`menubar_top = Menu(win)` `win.config(menu = menubar_top)`

如你所知，除了在最后的语句中调用`Tk`对象的`config()`方法外，我们还可以利用一个实际的事实，即`tkinter`的控件部分像字典一样工作，它们的选项因此也可以像字典的键值对一样访问。因此，我们本可以写成：

`win['menu'] = menubar_top`

现在，你的应用程序有了菜单栏，但在这种状态下启动程序时，菜单栏还不会显示出来。首先，我们需要添加单独的下拉菜单，这些菜单将为用户提供展开和折叠的功能。这些下拉菜单也是`Menu`类的对象，我们可以通过调用类的构造函数来创建。不过，这一次，我们不会直接将新的（下拉）菜单附加到窗口`win`，而是将其附加到我们已有的菜单栏`menubar_top`上：

`file_menu = Menu(menubar_top, tearoff = 0)`

选项`tearoff=0`会使菜单“固定”在窗口上。如果你省略此选项或将其设置为`tearoff=1`，菜单的第一项将显示为虚线。如果点击此项，菜单将从其固定位置分离，并在自己的窗口中显示出来，可以随意在屏幕上移动（试试看！）；这种行为通常是你希望禁用的。

现在我们可以开始通过`add_command(label = label)`向菜单中添加新的命令项：

`file_menu.add_command(label = '打开...')file_menu.add_command(label = '保存')file_menu.add_separator()file_menu.add_command(label = '关闭')`

通过使用`Menu`对象的`add_separator()`函数，我们在菜单中创建一个水平分隔线，以便更清晰地组织我们的菜单项。除了`add_command()`和`add_separator()`，还有两种其他类型的菜单项，`add_checkbutton()`和`add_radiobutton()`。这两种菜单项允许用户进行设置，如以下示例所示。当前的设置（即菜单选项是否被选中）可以随时从传递给`add_checkbutton()`函数的`variable`选项所绑定的变量中读取。

`file_menu.add_checkbutton(label = '自动保存', variable = auto_save)`

到目前为止，我们的菜单——与单独的菜单项不同——根本没有显示名称。我们通过调用菜单栏对象的`add_cascade()`函数来更改这一点，它还确保菜单实际上作为下拉菜单显示在我们的菜单栏上：

`menubar_top.add_cascade(label = '文件', menu = file_menu)`

如果你现在按这样启动程序，一个程序窗口将会打开，窗口中有一个带有“文件”菜单的菜单栏。当然，我们也可以继续在菜单栏上放置更多的下拉菜单。

`add_...()`函数，例如`add_command()`，可以通过多种选项调用，许多选项可以在◘表[22.1](#Tab1)中找到。例如：

`file_menu.add_command(label = 'Save', background='#FF0000')`将添加一个带有红色背景的菜单项“保存”，语句`file_menu.add_command(label = 'Save', state='disabled')`则会显示一个禁用（灰显）的菜单项。当然，你仍然可以在创建菜单后修改它。使用`delete(index_from, index_to)`可以根据数字索引删除菜单项。使用`entryconfig(index, option=value)`可以更改由`index`定义的菜单项的`option`（例如`state`用于启用/禁用）。你可以使用`entrycget(index, option)`查询选项。因此，要显示第二个菜单项的标签（`label`选项），你可以使用语句`print(file_menu.entrycget(1, 'label'))`（索引从0开始，就像在Python中一样！）。

如果你想稍后插入一个菜单项，可以使用函数`insert_...(index, option)`，其中`...`代表相应的元素（例如`command`、`separator`、`checkbox`），就像使用`add_...()`一样。该菜单项将插入到由`index`指定的菜单项之后。

我们的菜单现在看起来相当漂亮，但它没有任何功能：点击菜单命令不会触发任何操作。这是因为在我们调用下拉菜单对象`file_menu`的`add_command()`时，我们遗漏了一个重要的`command`选项，正是这个选项让我们能够指定一个函数，在用户点击菜单项时被调用。在这个函数中，我们将放置与菜单项相关的程序代码。我们将在►第[22.2.5](#Sec19)节中详细处理这些事件处理程序。在此处，我们将完全专注于创建一个具有视觉吸引力的界面。

如你所见，在`tkinter`中处理菜单并不复杂，但需要多个不同的步骤。因此，这里再次概述了你需要做的事情，以便为你的程序提供一个菜单：

1.  1.

    使用构造函数`menubar = Menu(window)`创建菜单栏。

1.  2.

    将菜单栏添加到窗口中：`window['menu'] = menubar`。

1.  3.

    创建一个新的下拉菜单，你希望将其放置在菜单栏上：`pd_menu = Menu(menubar)`。

1.  4.

    向新的下拉菜单中添加菜单项，即命令（使用`add_command()`）、偏好选项（使用`add_checkbox()`或`add_radiobutton()`）或分隔符（`add_separator()`），例如：`pd_menu.add_command(label = 'Title of command')`。请注意，稍后为了给菜单项添加功能，我们会在此处加入`command = event_function`选项。

1.  5.

    将新的下拉菜单附加到菜单栏，并为其指定一个在菜单栏中可见的标题：`menubar.add_cascade(label = 'Title of menu', menu = pd_menu)`。

在本节中，我们已经介绍了如何创建应用程序菜单作为程序中的主菜单。然而，`Menu` 对象也可以用来在窗口的任何位置打开弹出/上下文菜单，这得益于 `post(x, y)` 函数，但这超出了本节对 `tkinter` 的简要介绍。

#### 22.2.3.3 输入字段（类 `Entry` 和 `ScrolledText`）

单行输入框：`Entry`

输入字段用于接收用户的文本输入。在 `tkinter` 中，单行（小部件类 `Entry`）和多行文本输入（小部件类 `ScrolledText`）之间有区分。我们将在本节中更详细地了解这两者。

`Entry` 类型的小部件可以通过构造函数非常容易地创建并分配给窗口，在我们的例子中，仍然分配给 `Tk` 对象 `win`。

`myentry = Entry(win)` `myentry.pack()`

和之前的按钮一样，我们调用 `pack()` 方法将控件显示在窗口中。在► 第 [22.2.4](#Sec15) 节中，我们将更详细地探讨如何影响控件在窗口中的排列。

在◘ 表格 [22.3](#Tab3) 中，你将找到小部件最重要属性的概述，你可以通过字典索引 `input['option']` 或（但仅限于写入）通过 `input.configure(option=value)` 以通常的方式访问这些属性。表格 22.3

`Entry` 小部件的特殊属性

| 选项 | 类型 | 说明 |
| --- | --- | --- |
| `justify` | `str` | 输入框中文本的对齐方式，`'left'`（左对齐，默认值），`'center'`（居中）或`'right'`（右对齐） |
| `selectbackground` | `str` | 文本选择的背景颜色 |
| `selectforeground` | `str` | 文本选择的字体颜色 |
| `show` | `str` | 显示的字符（替代输入的字符）；例如可以用于密码输入 |
| `width` | `int` | 输入字段的宽度（以字符为单位，而非像素） |

你可以随时使用 `get()` 方法获取当前在 `Entry` 字段中的文本，例如：

`my_text = input.get()`

当然，你也可以编辑文本。这可以通过 `insert(index, string)` 方法实现。`index` 指定要插入的位置（从0开始计数），`string` 指定要插入的文本。因此，一开始你可以从

`input.insert(0, 'A first text in the input field.')` 可以预设输入字段的文本。你可以简单地在 `insert()` 方法中指定 `'end'`、`'insert'` 或 `'anchor'`，而不是使用真实的位置索引。这样文本会插入到末尾（`'end'`）、当前位置（`'insert'`）或当前选择的开头（如果当前有选择，则插入在开头，否则直接在文本开头）。例如，你可以使用语句 `input.insert('end', 'End of text.')` 来将文本追加到末尾。同样，你可以使用 `delete(*****from_index*****, ** ***to_index*****)` 方法删除文本。如果你省略可选参数 `to_index`，只会删除索引为 `from_index` 的字符。

使用 `icursor(*****index*****)` 可以将光标放置在文本中的特定位置，更确切地说，是在指定的 `index` 字符之后。然而，请注意，在 `tkinter` 中字符计数是从 1 开始的，这与 Python 的习惯不同。如果你将数字 0 指定为 `index`，则光标会放在第一个字符之前。这种计数方法适用于所有使用字符索引的地方。

为了使光标在文本中实际可见，你必须给予控件焦点，即使它成为你窗口中当前活动的控件。你可以像对待所有其他小部件一样，使用 `focus()` 方法做到这一点。

最后，方法`selection_range(*****from_index*****,** ***to_index*****)`允许你选择文本。同样，你可以使用`insert()`中已知的特殊常量`'end'`、`'insert'`和`'anchor'`。你可以使用`selection_get()`查询当前选中的文本，方法`selection_present()`在文本被选中时返回`True`。

`Entry`还允许你使用剪贴板。你可以使用方法`clipboard_append(*****text*****)`将文本添加到剪贴板；使用`clipboard_get()`检索剪贴板的内容，使用`clipoard_clear()`清空剪贴板。

多行输入：`ScrolledText`

如果要编辑更长的文本，小部件`ScrolledText`是一个不错的选择。要使用它，必须首先从`tkinter`包的`scrolledtext`模块中导入类`ScrolledText`：

`from` tkinter.scrolledtext `import` ScrolledText

在许多方面，`ScrolledText`小部件的行为与`Entry`小部件完全相同。你所学到的关于`Entry`的内容大部分可以直接应用于`ScrolledText`（区别在于`justify`和`show`选项、`icursor()`方法和插入位置`'anchor'`不可用）。

由于`ScrolledText`允许多行输入，因此文本位置也可以按照行/列方案进行定位是合乎逻辑的。例如，如果我们想删除从第二行第五个字符开始的所有文本，可以使用下面的方法调用。如果之前使用构造方法`ScrolledText()`创建的小部件命名为`st`：

`st.delete(2.4,'end')`

请注意，在`Entry`中有一个单一索引的位置，现在出现了一个分数：`2.4`。然而，这个数字是一个编码的行/列规范。它表示：第二行，第五个字符。因此，尽管在行内字符从0开始计数（`4`因此指的是第五个字符），我们在`tkinter`中已经习惯的行计数从1开始！`2.4`因此指的是`第二`行，但指的是`第五`个字符。

`ScrolledText`小部件比`Entry`小部件强大得多。例如，它本身允许使用`edit_undo()`和`edit_redo()`方法来撤销或重做编辑操作（该小部件的`undo`选项必须事先设置为`True`）。`ScrolledText`还允许您为文本区域分配名称（称为`tags`），然后使用`tags`访问和编辑文本区域。这样，您可以例如以不同的颜色突出显示不同的文本区域。因此，如果您想开发一个具有语法高亮功能的文本编辑器，`ScrolledText`小部件不是一个坏的起点。

#### 22.2.3.4 文本输出（标签）

标签是显示在应用程序窗口中的静态文本。它们通常不提供用户任何交互选项，而是用于显示信息或描述控件的功能（如果这些控件没有自己的标签，例如按钮）。

您可以如下创建并显示标签小部件：

`label = Label(win, text = 'Here is a fixed text')` `label.pack()` ◘ 表 [22.4](#Tab4) 显示了一些标签的重要属性。此外，当然还有大多数小部件提供的标准属性，这些属性列在◘ 表 [22.1](#Tab1)中，而标签最显著的特性无疑是`text`选项，即在标签上显示的文本。在示例中，我们在调用构造函数时直接设置了文本，但当然，像所有其他属性一样，它也可以通过`label.configure(text =` `new_text` `)`或`label['text'] =` `new_text`轻松更改。

`Label`小部件的特殊属性

| 选项 | 类型 | 说明 |
| --- | --- | --- |
| **anchor** | **str** | 文本的位置和方向。使用方位词的英文缩写进行描述，例如`'ne'`表示*东北*，即右上角；可能的规格包括：`'n'`（顶部中心）、`'ne'`（右上角）、`'e'`（右中心）、`'se'`（右下角）、`'s'`（底部）、`'sw'`（左下角）、`'w'`（左中心）、`'nw'`（左上角）以及另外的`'center'`（水平和垂直居中） |
| **width** | **int** | 标签的宽度（以字符为单位）。如果未指定，标签的宽度将足够容纳要添加的文本 |
| **wraplength** | **int** | 标签中文本被换行的字符数。如果未指定，则不会换行 |

#### 22.2.3.5 `Check Buttons`和`Radio Buttons`

`Check`按钮（或`checkbox`）和`radio`按钮用于给用户提供多种设置/选项的选择。`checkbox`允许用户选择多个不同的设置/选项，而`radio`按钮仅允许用户一次选择一个设置/选项。

`Check`按钮和`radio`按钮在`tkinter`中由同名类表示。让我们首先创建两个`radio`按钮：

`selection_var = IntVar()` `selection_opt1 = Radiobutton(win, text = 'Option One', variable = selection_var, value = 1)` `selection_opt2 = Radiobutton(win, text = 'Option Two', variable = selection_var, value = 2)` `selection_opt1.pack()` `selection_opt2.pack()`

首先，考虑`radio`按钮本身的构造函数调用：在这里，像往常一样，我们首先将我们的窗口对象`win`（类型为`Tk`）传递给`radio`按钮，并显示作为选择选项的文本。除此之外，还有两个参数，`variable`和`value`。

对于`variable`参数，我们将一个变量`selection_var`赋值给它，`selection_var`是在代码段开始时创建的，作为`IntVar`类的实例。`IntVar`是`tkinter`附带的几个特殊变量类之一。它不仅仅是一个普通的`int`变量。这个变量的特别之处在于，当我们将它赋值给`radio`按钮构造函数的`variable`参数时，它始终反映我们的`radio`按钮集的当前状态，即指示当前选择了哪个`radio`按钮选项。我们通过`Radionbutton()`的`value`参数定义`selection_var`在选择特定`radio`按钮时所取的值。因此，如果用户点击“Option Two”`radio`按钮，`selection_var`的值为2。如果用户点击“Option One”，`selection_var`的值为1。`IntVar selection_var`会在`radio`按钮的选择状态变化时自动更新。

这非常方便；但是，在查询值时需要记住一个特殊之处：如果你执行`print(selection_var)`，则会在运行控制台输出以下内容：`PY_VAR0`

但这不是变量的值。这是因为`selection_var`不是一个普通的`int`变量。我们必须使用它的`get()`方法查询它的值，尽管这需要一些适应。以下语句将成功：

`print(selection_var.get())`

类似地，有一个方法`set()`，可以改变`IntVar`变量的值。由于我们通过构造函数`Radiobutton()`的`variable`参数将变量`selection_var`链接到单选按钮，这也改变了单选按钮之间的选择。

`selection_var.set(2)`我们会自动选择分配值为2的单选按钮，即“左侧”单选按钮。相同的效果可以通过调用相应单选按钮实例的`select()`方法来实现：`select_left.select()`

因为我们将`IntVar`变量`selection_var`作为`variable`选项`to both radio buttons`，`tkinter`知道这两个单选按钮属于同一组，因此只能`one of them`被选中。所以请务必将相同的变量作为`variable`选项分配给属于同一“选择组”的单选按钮！

`Check buttons`的功能与单选按钮非常相似，当然不同的是，这里可以同时选择多个复选框，因为这两个复选框可以彼此独立选择。而对于单选按钮，如果按钮1被选中，按钮2就不能被选中，两个复选按钮则不再只有两种状态，而是四种不同的状态（两者都选中、都不选中、只选中第一个按钮、只选中第二个按钮）；一个的状态因此不再依赖于另一个按钮的状态。因此，你还需要两个不同的`IntVar`变量作为构造函数`Checkbutton()`的`variable`参数：

`selection_var1 = IntVar()` `selection_var2 = IntVar()` `selection_opt1 = Checkbutton(win, text = 'Option One', variable = selection_var1)` `selection_opt2 = Checkbutton(win, text = 'Option Two', variable = selection_var2)` `selection_opt1.pack()` `selection_opt2.pack()`

你可能已经注意到，在`Checkbutton()`构造函数中，我们不再有`value`参数。默认情况下，状态变量`variable`在复选框被选中时取值`True`，未被选中时取值`False`。不过，使用可选参数或控件选项`onvalue`和`offvalue`，如果需要，可以更改此值。

◘ 表[22.5](#Tab5)给出了`Radiobutton`和`Checkbutton`类型的控件最重要的特殊属性的概述，超出了◘ 表[22.1](#Tab1)中列出的标准选项。

`Checkbutton`和`Radiobutton`控件的特殊属性

| 选项 | 类型 | 意义 |
| --- | --- | --- |
| `indicatoron` | `Bool` | 如果为`False`，则显示一个真正的按钮，而不是圆形（单选按钮）或方形（复选按钮）选择元素，选中单选按钮/复选按钮时，按钮会看起来被按下 |
| `selectcolor` | `str` | 圆形（单选按钮）或方形（复选按钮）选择元素的背景颜色 |

#### 22.2.3.6 选择列表 (`Listbox`)

选择列表，表示为`tkinter`类`Listbox`，允许从一组文本条目中进行（单项或多项）选择。在使用`Listbox()`类构造函数创建列表框并使用`pack()`方法将其显示在窗口中后：

`mylistbox = Listbox(win)` `mylistbox.pack()` 我们可以开始向列表框中添加项目。为此，我们使用`insert(index, entry, ...)`方法：`mylistbox.insert('end', 'Beverly', 'Thomas', 'Marc', 'Jimmy', 'Cathy')`

`insert()`方法与`Entry`控件的同名方法有一些相似之处：`index`首先指定要插入元素的数字索引，它是插入位置的“后面”；与`Entry`的`insert()`方法一样，值`'end'`也可以指定，确保将条目添加到列表的末尾。也可以通过同时添加多个条目来扩展列表。请注意，列表条目的索引从0开始，这与Python的典型做法一致（不同于`Entry`控件中字符的索引，但与多行`ScrolledText`控件的“列索引”一致）。

同样，类似于`Entry`，您可以使用`delete(index_from, index_to)`方法从列表框中删除列表条目。在`Entry`控件中，此方法会删除`Entry`字段中的单个字符，也就是字符串，因此是一个“字符列表”。

通过调用`selection_set(index_from, index_to)`方法，您可以像用户选择条目一样选择列表框中的条目。

在`delete()`和`selection_set()`中，`index_to`是一个可选参数，也就是说，在调用方法时可以省略该参数。

就像您可以使用`selection_set()`选择一个（或多个）条目一样，您可以应用`selection_includes(index)`来检查由`index`表示的列表元素是否当前已被选中。

最后，使用`selection_clear()`可以清除列表框中的当前选择。

您可以使用`length()`方法来确定列表条目的数量，而`get(index_from, index_to)`允许您读取一个或多个条目的文本。如果您使用可选参数`index_to`并指定一个范围，您将获得一个`tuple`，其中包含指定列表条目的文本条目作为返回值。

◘ 表格[22.6](#Tab6)列出了您可以按照现在熟悉的方式自定义的`Listbox`控件的一些重要选项。表格22.6

`Listbox`控件的特殊属性

| 选项 | 类型 | 说明 |
| --- | --- | --- |
| `activestyle` | `str` | 指定活动条目（即当前具有焦点的已选条目）应该如何在视觉上突出显示；可能的值有`underline`（文本下划线）、`dotbox`（带点线的轮廓框）和`none`（不突出显示），其中`underline`为默认值 |
| `height` | `int` | 列表框的高度，但以条目数来度量，而不是像素；默认值为10。如果您有超过`height`中设置的条目数并希望确保`index`位置的条目被显示，您可以调用`see(index)`方法；该方法会滚动列表框，以确保`index`条目无论如何都能显示出来 |
| `selectmode` | `str` | 指定一次可以选择多少条目以及它们必须如何相关；可能的选项有：`single`（可以通过点击条目选择一个条目），`browse`（可以通过点击或按住鼠标按钮并移动鼠标来选择一个条目），`multiple`（可以选择多个条目，点击条目会选择它，如果之前没有选中它，则选中它，如果已经选中则移除它）和`extended`（可以通过按住<CTRL>或<SHIFT>键同时点击来选择多个条目）；默认值是`multiple`，这对于Windows用户来说有些不常见 |

此外，你当然也可以使用我们在◘表格[22.1](#Tab1)中看到的标准选项。这些属性中的许多也可以应用于`listbox`中的`individual items`。为此，请使用`itemconfig(index, option=value)`方法。例如，要给第三个项设置一个绿色背景，你可以执行以下语句：`mylistbox.itemconfig(2, background='#ED5036')`

在◘表格[22.6](#Tab6)中，你将再次看到可以取多个值的选项的情况，例如`activestyle`。鉴于`tkinter`的文档情况相当复杂，问题自然出现了，哪些表达式是被允许的。你仍然不知道各个值的作用，但可以通过反复试验很快找出。所以，第一步要做的关键是理解你到底有哪些选项。这里有一个简单的技巧：你可以故意引发一个错误。为此，请考虑以下代码：

`mylistbox['activestyle'] = 'xxx'`

在这里，我们尝试将值`xxx`赋给`activestyle`选项，这很可能不是该选项的有效表达式。如果我们运行含有此语句的程序，我们会得到一条错误消息，而这正是我们在此案例中试图实现的目标。在我们的例子中，得到的错误是：

`Traceback (most recent call last):` `File "C:/Users/MyUser/Desktop/Documents/tkinter_hello_world.py", line 138, in <module>` `names['activestyle']='xxx'` `File "C:\Users\MyUser\AppData\Local\Programs\Python\Python37-32\lib\tkinter\__init__.py", line 1489, in __setitem__` `self.configure({key: value})` `File "C:\Users\MyUser\AppData\Local\Programs\Python\Python37-32\lib\tkinter\__init__.py", line 1482, in configure` `return self._configure('configure', cnf, kw)` `File "C:\Users\MyUser\AppData\Local\Programs\Python\Python37-32\lib\tkinter\__init__.py", line 1473, in _configure` `self.tk.call(_flatten((self._w, cmd)) + self._options(cnf))` `_tkinter.TclError: bad activestyle "xxx": must be dotbox, none, or underline`

这里的关键部分在于最后一行。在那里，错误消息列出了可能的值，现在你可以轻松地一一尝试。

#### `22.2.3.7 消息/决策对话框（类messagebox）`

有时你可能希望以某种方式提醒用户，让他们注意到你的消息。或者你可能希望强迫用户立即做出决定，例如在保存文件时是否覆盖它。在所有这些情况下，`message box`是一个不错的选择。

你可以借助`tkinter`模块的`messagebox`创建一个消息框。因为`messagebox`与我们迄今为止遇到的大多数控件不同，它“打包”在自己的模块中（与`ScrolledText`一样），我们必须首先导入它包含的类。我们在这里简单使用星号通配符来导入`messagebox`模块中包含的所有类：

`from tkinter.messagebox import *`

然后，使用`showinfo(title, message)`，`showwarning(title, message)`和`showerror(title, message)`函数，我们可以显示一个消息框，根据消息类型（信息、警告或错误）每个都有不同的图标。这里是一个警告消息的示例：

`showwarning('注意','输入的年龄必须大于0。')`

你还可以通过在调用相应函数时指定额外的选项来定制消息框的设计。可选的选项有`icon`（应该显示哪个图标？），`type`（应该显示哪些按钮？）和`default`（哪个按钮应该预选，以便在用户按下<ENTER>键时触发）。

`icon`选项可以取值为`'info'`、`'warning'`、`'error'`和`'question'`。前三个是`showinfo()`、`showwarning()`和`showerror()`函数也使用的图标，而`'question'`则显示一个问号图标。像图标一样，用户可用的按钮组合也可以通过常量来指定，在这种情况下，`'ok'`（*确定*按钮）、`'okcancel'`（*确定*和*取消*）、`'yesno'`（*是*和*否*）、`'yesnocancel'`（*是*、*否*和*取消*）、`'retrycancel'`（*重试*和*取消*）以及`'abortretryignore'`（*取消*、*重试*和*忽略*）。例如，如果我们想显示一个小对话框，询问用户是否要覆盖文件，并提供*是*、*否*和*取消*按钮，我们可以创建一个合适的消息框，代码如下：

`feedback = showwarning('确认', '你真的要覆盖文件吗？', icon='question', type='yesnocancel', default='yes')print(feedback)`

从这个例子中可以看出，尽管我们使用的是`showwarning()`函数，默认显示感叹号图标，但通过指定`icon`选项，我们可以覆盖默认行为。

该函数返回一个小写字母字符串，包含被点击按钮的标签，在我们的示例中是`'yes'`、`'no'`或`'cancel'`。这个函数的返回值对于能够根据用户的输入做出相应反应非常重要。

与我们在前几节中查看的控件不同，消息框不是我们需要创建实例的类。相反，它只是`messagebox`模块中的一个函数。文件对话框也是如此，我们将在下一节中讨论。

#### 22.2.3.8 文件打开/保存对话框

如果你希望让用户选择打开文件或保存文件，`tkinter`模块中的`filedialog`可以让你轻松地在程序中使用“打开文件”和“另存为”这两个标准对话框。

首先，我们需要导入该模块。为了简化，我们导入模块中包含的所有类和函数，就像在前一节中导入`messagebox`模块一样：

`from tkinter.filedialog import *`

之后，可以使用`askopenfilename()`或`asksaveasfilename()`函数调用打开或保存文件的对话框。在以下示例中，我们选择一个文件进行打开，并在（运行）控制台中打印结果：

`filename = askopenfilename(defaultextension='txt', filetypes=[('文本文件', '*.txt'), ('所有文件', '*.*')], title='打开文件...', initialdir='C:\\Windows')print(filename)`

这些函数返回所选文件的名称（包括路径）。如果用户在对话框中取消选择而没有选择文件或输入文件名，则返回一个空字符串。如上例所示，您可以通过一些选项来控制对话框的行为。`filetypes`是一个列表（注意方括号！），其中每个元素是一个元组，包含描述和文件扩展名；用户可以预先选择定义的文件类型。`title`选项控制对话框标题；`initialdir`是对话框打开时默认显示的目录；路径中的反斜杠（`\`）必须写两次，单个反斜杠会被Python解释为转义字符；如果您不熟悉转义字符，请返回► Sect. [11.​2.​2](474412_1_En_11_Chapter.xhtml#Sec4)。

顺便提一下：你可能在上一节中对`messagebox`模块产生过疑问，为什么在这里我们没有像其他小部件那样使用类，而是调用像`showwarning()`或`askopenfilename()`这样的函数。答案是：因为这种方式对我们来说最简单！这些函数会在后台创建必要的类实例。由于我们只关心结果，这里指的是文件名，并且不想真正处理对话框（类）实例，因此只要一个合适的函数提供我们文件名并省去了自己创建类实例的麻烦，就足够了。当然，其他小部件的情况是不同的，它们会一直存在于我们的应用程序窗口中，且我们稍后还会与它们一起工作。

#### `22.2.3.9 其他小部件`

除了我们在前几节中看到的小部件外，设计程序界面时还有许多其他控件可以使用，例如`Canvas`（绘图区域）、`Spinbox`（带有上下箭头的输入框用于调整值）、`Treeview`（元素的层次显示；从`tkinter.ttk`模块导入）、`Notebook`（选项卡上的控件显示；也在`tkinter.ttk`模块中）、`Progressbar`（在`tkinter.ttk`模块中），仅举几例。对于可以添加到许多控件（如菜单项、按钮）中或用作背景（例如主应用窗口背景）的图像，还有`PhotoImage`类。

正如您所看到的，`tkinter`还有很多东西值得探索！唯一的缺点是相对较差的文档，至少对于上述提到的`tkinter.ttk`模块的小部件而言。有较多或少足够的“官方”文档（目前可用地址为► [https://​docs.​python.​org/​3/​library/​tkinter.​ttk.​html](https://docs.python.org/3/library/tkinter.ttk.html)）。不过，通常进行自己的互联网搜索往往是最佳选择。幸运的是，您通常可以快速找到所需的内容，因为许多程序员在您之前已经有过类似的问题！

### 22.2.4 控件的排列（几何管理器）

在前面的部分中，我们认识了一些控制元素，允许用户通过界面控制程序。为了构建一个视觉上吸引人且易于使用的界面，各种控制元素必须放置在它们应该在界面上的位置。

为了在表面上安排控件，`tkinter`提供了三种*几何管理器*，我们将在接下来的部分中更详细地处理它们。这三者都遵循不同的基本原则来定义控件在表面上的位置。根据您应用程序最适合的定位方式，您可以选择相关的几何管理器。

三个几何管理器是：

+   `Pack`：`Pack`简单地将控件一个接一个地放置，或者一个在另一个下面。在前面的部分中，我们已经通过调用小部件的`pack()`方法来使用这个几何管理器。这使得小部件一个在另一个下面被放置，并将它们居中于可用空间。

+   `Grid`：`Grid`心理上将表面上的可用空间划分为行和列的网格，并允许控件放置在该网格的每个“单元格”中。`Grid`非常适合构建复杂的界面，并且应该足以满足大多数目的。

+   `Place`：`Place`根据其*绝对*“坐标”位置来定位元素，这些坐标以像素为单位，或*相对*（以窗口宽度/高度的比例来测量）于窗口的左上角。

#### 22.2.4.1 `Pack`

当我们仔细查看各种小部件时，我们使用了`pack()`方法以确保这些小部件实际显示在我们的程序界面上。然而，这些小部件不仅被显示出来，而且当然也在窗口中同时定位，一个在另一个下面。这正是几何管理器`Pack`所做的：顾名思义，它“打包”各种控件，可以是垂直的“堆叠”（这是默认方向），也可以是水平的“行”。元素在表面上出现的位置主要取决于其前驱在堆叠（在垂直对齐的情况下）或行（在水平对齐的情况下）中的大小。

举个例子，假设我们有一个用于输入密码的程序界面：

`from` `tkinter` `import` `win = Tk()win.title('Demonstration of the Geometry Managers')win.geometry('500x100')prompt = Label(win, text = 'Please enter your password:')pwd = Entry(win)login = Button(win, text = 'Login')pwd['show'] = '*'pwd['width'] = 20pwd.focus()`

我们创建了三个小部件：一个名为`prompt`的`label`用来显示提示信息，一个输入框`pwd`用来保存密码，以及一个登录按钮用来确认密码输入。然后，我们配置输入框`pwd`隐藏密码输入，只显示输入字符的星号。我们还将其宽度设置为20个字符，并赋予它焦点，这样用户可以直接开始输入。接下来，像之前一样，我们调用`pack()`方法，让`pack`几何管理器将小部件放置在界面上。为了确保控件彼此并排显示，而不是像默认情况那样堆叠在彼此下面，我们使用`side`选项调用`pack()`，该选项接受常量`'left'`、`'right'`和`'bottom'`作为控件定位方向的值，默认值为`'top'`：

`prompt.pack(side = 'left')pwd.pack(side = 'left')login.pack(side = 'left')win.mainloop()你可以在◘ 图 [22.2](#Fig2)中看到结果。小部件现在紧挨着彼此。通过使用`padx`（以及垂直方向的`pady`），我们可以为每个小部件的左右添加一些间距（`padding`），例如：![](../images/474412_1_En_22_Chapter/474412_1_En_22_Fig2_HTML.jpg)

显示一个标题为“几何管理器演示”的窗口截图，下面是一个密码框，旁边放置了一个登录按钮。

图 22.2

使用`pack(side = LEFT)`排列小部件

`pwd.pack(side = 'left', padx = 5)`

另外两个重要的选项可以用来更详细地控制`pack()`的行为：`expand`，它可以取值`1`和`0`，或者`True`和`False`，决定`pack`几何管理器是否应使用它所能使用的全部宽度。在我们的示例中，这就是整个窗口的宽度。如果我们改变所有三个小部件的默认设置，并告诉`pack()`使用全部宽度（`expand=1`），即：

`prompt.pack(side = 'left', expand = 1)pwd.pack(side = 'left', expand = 1)login.pack(side = 'left', expand = 1)`，结果如◘ 图 [22.3](#Fig3)所示。![](../images/474412_1_En_22_Chapter/474412_1_En_22_Fig3_HTML.jpg)

一个名为“几何管理器演示”的窗口截图。下面是一个密码输入框，登录按钮与其保持一定距离。

图 22.3

带有 `expand` 选项的小部件布局

这仍然是“打包”小部件，但每个小部件有更多的空间。在每个小部件可用的空间内，控件默认居中，但可以通过额外的 `anchor` 选项轻松调整，具体规格为`'n'`、`'ne'`、`'e'`、`'se'`、`'s'`、`'sw'`、`'w'`、`'nw'`和`'center'`（默认）。这些选项与 `Label` 小部件相同（参见 ◘ 表 [22.4](#Tab4)）。

此外，我们还可以告诉 `pack()` 最大程度地扩展小部件在可用空间中的占据，这对于某些用途非常有用，但有时看起来会比较奇怪。为此，我们将 `fill` 选项设置为常量之一：`'x'`（水平扩展）、`'y'`（垂直扩展）或 `'both'`（水平和垂直都扩展）。以下示例正是这样做的，我们让输入框在水平方向上扩展，登录按钮则在两个方向上都扩展以占据可用空间，最终呈现出 ◘ 图 [22.4](#Fig4) 中看到的界面：![](../images/474412_1_En_22_Chapter/474412_1_En_22_Fig4_HTML.jpg)

一个名为“几何管理器演示”的窗口截图。下方是一个延伸的密码输入框，登录按钮与其保持一定距离。

图 22.4

带有不同选项的小部件布局

`prompt.pack(side = 'left', fill = 'x', anchor = 'w')` `pwd.pack(side = 'left', expand = 1, fill = 'x', padx = 5, anchor = 'w')` `login.pack(side = 'left', expand = 1, fill = 'both', anchor = 'w')`

如本示例所示，通常需要不断调整 `pack` 选项如 `side`、`fill`、`expand`、`anchor` 和 `padx/pady`，直到找到合适的布局。稍微有些经验后，你可以实现你在纸上或数字上画出的界面结构。

#### 22.2.4.2 网格布局

`Pack` 尝试将控件并排“打包”，而 `grid` 几何管理器则将应用程序窗口视为一个由 `行` 和 `列` 组成的 `网格`。控件可以在网格内自由定位。网格中的每个“单元格”使用从 0 开始的 Python 风格的索引来定位。

请参考上一节中使用的密码输入示例：

`from tkinter import` `win = Tk()` `win.title('几何管理器演示')` `win.geometry('500x100')` `prompt = Label(win, text = '请输入您的密码：')` `pwd = Entry(win)` `login = Button(win, text = '登录')` `pwd['show'] = '*'` `pwd['width'] = 20` `pwd.focus()`

在下一步中，我们使用 `grid(row =` `row`, `column =` `column)` 方法将提示和输入框并排放置，登录按钮位于输入框下方：

`prompt.grid(row = 0, column = 0)` `pwd.grid(row = 0, column = 1)` `login.grid(row = 1, column = 1)` `win.mainloop()` 结果如◘图 [22.5](#Fig5)所示。![](../images/474412_1_En_22_Chapter/474412_1_En_22_Fig5_HTML.jpg)

一个窗口截图，标题为“几何管理器的演示”。其中有一个密码输入框，下面放置了一个登录按钮。

图 `22.5`

使用 `grid()` 安排小部件。

如你所见，输入框和按钮显示在同一列中，即第 1 列（即第二列）。几何管理器调整单元格的大小，使小部件正好适合其中。在单元格中，控件默认是居中的（垂直居中——以及如按钮示例所示的水平居中）。

然而，小部件在单元格中的对齐方式可以通过使用 `sticky` 选项轻松影响。如之前多次所见，`sticky` 是一种方向指定方式。`sticky = 'w'` 意味着小部件应当对齐到“西边”，即单元格的左边缘。同时，也可以使用四个方向来调整小部件的宽度，使其即使比单元格小，仍能完全填充单元格。例如，`sticky = 'we'` 使得小部件在其单元格中，单元格宽度由上面行中较宽的输入框决定，从“西到东”延伸，即跨越整个单元格的宽度。

你可以在◘图 [`22.6`](#Fig6) 中看到结果。![](../images/474412_1_En_22_Chapter/474412_1_En_22_Fig6_HTML.jpg)

一个窗口截图，标题为“几何管理器的演示”。其中有一个密码输入框，下面正下方放置了一个登录按钮。

图 `22.6`

使用 `grid()` 和按钮的 `sticky = 'we'` 选项来安排小部件。

然而，有时这并不足够，你可能希望某个小部件跨越多个列或多个行。在这种情况下，`rowspan` 和 `columnspan` 选项可以派上用场，它们分别指定跨越的行数或列数。

`login.grid(row = 1, column = 0, sticky = 'we', columnspan = 3)` 这样，我们的按钮就会从提示框的左边缘延伸到输入框的右边缘。`padx` 和 `pady` 选项（从 `pack()` 中已经知道）允许你分别指定左右和上下的间距，这样通常会使显示效果更加均衡，如◘图 [`22.7`](#Fig7)所示，在该例中使用了 `padx` 和 `pady` 值为 5。![](../images/474412_1_En_22_Chapter/474412_1_En_22_Fig7_HTML.jpg)

一个窗口截图，标题为“几何管理器的演示”。其中有一个密码输入框，下面放置了一个距离较远的登录按钮。

图 `22.7`

使用 `grid()` 和 `padx`、`pady` 选项安排小部件。

应用窗口中网格的总大小取决于你放置的最远位置的小部件。在我们的例子中，网格有两列和两行；如果我们使用`widget.grid(row = 0, column = 2)`将小部件放置到输入框的右侧，那么就会添加第三列。Grid是一个非常流行的几何管理器，因为它能够让你以最小的努力设计出有效的界面，同时提供直观的定位方式。在►第[`22.2.6`](#Sec20)节中，我们将开发一个完整的`tkinter`应用程序，那里也会使用`Grid`。

#### `22.2.4.3 Place`

第三种、最后一种可能也是最少使用的几何管理器是`Place`。`Place`用于将小部件放置在一个绝对位置，该位置由`x`和`y`坐标指定，或者放置在一个相对位置。相对位置意味着，位置是相对于窗口的左上角，按照窗口宽度或高度的百分比来测量的。语句

`login.place(relx = 0.5, rely = 0.5)`将`login`按钮精确地放置在窗口的正中央，也就是距离窗口左上角50%窗口宽度（`relx`）和50%窗口高度（`rely`）。更准确地说：按钮的`左上角`被放置在那里。通过`anchor`选项（从`pack()`已知），还可以指定另一个角作为定位的“锚点”。同样，角落是通过地理方向指定的，例如`'se'`表示东南角，也就是右下角。小部件的大小也可以指定，可以通过`width`和`height`选项进行绝对指定，或者通过相对大小指定。在这种情况下，可以使用`relwidth`和`relheight`将宽度或高度指定为窗口宽度或高度的百分比。

指定相对位置和大小的优点在于，当窗口大小发生变化时，小部件的位置和大小会自动适应，这一效果也可以通过几何管理器`pack`和`grid`实现（尽管使用后者时稍显繁琐），但当使用`place`进行绝对位置指定时，就无法实现这一点。

### 22.2.5 事件

`tkinter`小部件的命令选项

到目前为止，我们已经组合了响应式界面，但它们基本上没有任何功能。当你点击我们的按钮或菜单项时，什么也不会发生。现在，情况将发生变化。

一些小部件，如`Button`或`Menu`，本身带有一个功能，可以在控件被用户“触发”时调用该功能。考虑一下现在广为人知的开尔文与摄氏度之间的转换。一个带有图形界面的简单转换器可能像这样：

`from` `tkinter` `import` `def convert():lb_result['text'] = 'Conversion result: ' + str(round(float(en_kelvin.get()) - 273.15, 2)) + ' °C.'`def closeapp():quit()win = Tk()win.title('Kelvin-Celsius Conversion')win.geometry('400x150')menu_top = Menu(win)win.config(menu = menu_top)actionmenu = Menu(menu_top, tearoff = 0)actionmenu.add_command(label = 'Convert', command = convert)actionmenu.add_separator()actionmenu.add_command(label = 'Close', command = closeapp)menu_top.add_cascade(label = 'Action', menu = actionmenu)lb_input = Label(text = 'Temperature in Kelvin:')en_kelvin = Entry()bt_convert = Button(win, text = 'Convert', command = convert)lb_result = Label(width = 30)lb_result.pack()en_kelvin.pack()bt_convert.pack(pady = 10)lb_result.pack(pady = 10)win.mainloop()`用户界面的程序如图`◘ 图 22.8`所示。![](../images/474412_1_En_22_Chapter/474412_1_En_22_Fig8_HTML.jpg)

窗口截图标题为“Kelvin-Celsius 转换”。输入字段下方有一个转换按钮。

`图 22.8`

`Kelvin to Celsius converter`

与前面的部分相比，这一次我们在调用按钮构造方法`Button()`时使用了`command`选项来添加菜单项`add_command()`。`command`选项被赋值为一个函数，称为`事件处理程序`或`回调函数`，每当用户触发该控件时，该函数会被自动调用。例如，如果我们的“转换”按钮被点击，`convert()`函数会被自动调用。我们在程序中较早之前定义了`convert()`函数（函数定义必须在赋值给`command`选项之前）；它简单地执行转换并在`lb_result`标签上打印结果。注意，在将事件处理函数分配给`command`选项时，函数名后面没有指定圆括号。这是因为`command`选项仅仅传递函数`对象`；你会记得在Python中，函数也是对象——只有在定义函数（如你将看到的）或调用函数时，我们才需要包括圆括号，而不是当我们指的是函数对象本身时。

绑定事件处理程序 `tkinter` 知道另一种更强大的方式来响应事件。这是通过使用小部件方法 `bind()` 来实现的。通过语句 `bt_convert.bind('<button-1>', convert)`，我们本可以实现与上面`Button()`构造器中的 `command` 选项相同的效果。`bind(event, eventhandler_function)`方法将事件处理函数绑定到一个事件。因此，从此之后，我们的事件处理`mainloop()`会监视是否触发事件，并在事件发生时调用事件处理函数。字符串`'<Button-1>'`表示按下了左键/主要鼠标按钮（顺便提一下，右键鼠标按钮是`'<Button-3>'`，中间按钮是`'<Button-2>'`）。除了这些按钮事件外，还有多种事件可以绑定事件处理程序；以下是一些示例：

+   `<DoubleButton-1>`：左键双击。

+   `<Enter>` 和 `<Leave>`：用户将鼠标指针移入或移出控件区域。

+   `a`，`b`，`c`，...：按下了相应的字母键。

+   `<Key>`：按下了任意字母键。

+   `<F1>`，...：触发了相应的功能键。

+   `<Escape>`，`<BackSpace>`（删除），`<Delete>`，`<Tab>`（制表符），`<Return>`（回车或回车键），`<Shift_L>`（Shift），`<Control_L>`（Ctrl），`<Alt_L>`（Alt），`<End>`，`<Home>`，`<Left>`（左箭头），`<Up>`（上箭头），`<Right>`（右箭头），`<Down>`（下箭头），`<Print>`，`<Insert>`：按下了相应的特殊键。

键盘组合也可以通过这种方式表示：例如，如果你想绑定一个函数到同时按下`<CTRL>`和`S`的事件，你只需要指定`'<Control_L>S'`作为事件。

让我们更仔细地看看我们使用`bind()`绑定到事件的事件处理程序。这些函数会自动传递一个`Event`类型的参数。因此，我们需要调整之前为按钮的`command`选项分配的事件处理程序，例如，因为这些事件处理程序不需要任何参数。这个变化很小，但可以避免运行时错误：

`def` convert(ev = `None`):`lb_result['text']` = '转换结果: ' `+` str(round(float(`en_kelvin.get()`) - 273.15, 2)) `+` ' °C.'

我们不需要对`Event`对象`ev`做任何处理，但事件处理程序函数必须提供这个参数。通过为参数提供默认值（即`None`），我们还使得该函数可以用于菜单项“转换”的`command`选项，因为它在调用时不会传递参数。所以，事件处理程序必须能够处理在有参数和没有参数两种情况下被调用的情况。

那么，这个事件对象的内容是什么呢？事件对象提供了一些关于事件的信息，特别是：

+   `x`, `y`：鼠标位置（相对于窗口左上角）触发事件的位置（对于点击事件特别重要）。

+   `widget`：触发事件的小部件。

+   `char`：被按下的字符键（对于`<Key>`事件尤其重要）。

顺便提一下：您还可以直接将事件绑定到应用程序窗口，在我们的案例中是`Tk`对象`win`。如果某个小部件触发了事件，系统会首先自动检查该小部件是否绑定了事件处理程序。如果没有，则会检查“下一个更高”的对象，在我们的案例中是应用程序窗口，是否有此事件的事件处理程序。从这个意义上说，事件处理程序的存在是从“具体到一般”进行检查的；事件处理程序形成了一种层级结构。

### 22.2.6 示例：计算器应用程序

在本节中，我们将使用`tkinter`开发一个简单的计算器。计算器应能处理四种基本算术运算，并允许将计算结果复制到剪贴板。您可以在◘图`[22.9](#Fig9)`中查看结果。![](../images/474412_1_En_22_Chapter/474412_1_En_22_Fig9_HTML.jpg)

一个计算器应用程序窗口的截图。下面是一个输入框，数字为`96.54`，并有一个数字键盘和数学运算符。

图`22.9`

计算器应用程序的界面

现在让我们逐步查看代码：

1`from`tkinter`import`2`from`tkinter.font`import`3`from`functools`import`456`# 定义按钮的事件处理函数`7`def`digit_operator_press(digit_operator):`8`display['text'] = display['text'] + digit_operator`91011`def`delete_press():`12`display['text'] = ''`131415`def`copy_press():`16`win.clipboard_clear()`17`win.clipboard_append(display['text'])`181920`def`plusminus_press():`21`display['text'] = '-' + display['text']`222324`def`equal_press():`25`display['text'] = str(eval(display['text']))`262728`# 定义<ENTER>键的事件处理函数`29`def`enter_press(ev):`30`equal_press()`313233`# 创建应用窗口`34`win = Tk()`35`win['background'] = '#000000'`36`win.title('计算器')`37`win.geometry('268x470')`38`win.resizable(height=False, width=False)`3940`# 定义按钮和显示器的字体`41`digit_font = Font(family = 'Arial', size = 18)`42`display_font = Font(family = 'Arial', size = 24,`43`weight = 'bold')`4445`# 创建显示器`46`display = Label(text = '',`47`background = '#000000',`48`foreground = '#00FF00')`49`display['width'] = 1350`display['font'] = display_font`51`display['height'] = 252`display['anchor'] = 'e'`5354`# 定义按钮`55`delete_op = Button(win,`56`text = '删除',`57`width = 9,`58`height = 1,`59`font = digit_font,`60`foreground = '#FFFFFF',`61`background = '#4C4E4F',`62`command = delete_press)`63`plusminus_op = Button(win,`64`text = '+/-',`65`width = 4,`66`height = 1,`67`font = digit_font,`68`foreground = '#FFFFFF',`69`background = '#4C4E4F',`70`command = plusminus_press)`71`copy_op = Button(win,`72`text = '复制',`73`width = 4,`74`height = 1,`75`font = digit_font,`76`foreground = '#FFFFFF',`77`background = '#4C4E4F',`78`command = copy_press)`79`digit1 = Button(win,`80`text = '1',`81`width = 4,`82`height = 2,`83`font = digit_font,`84`command = partial(digit_operator_press,'1'))`85`digit2 = Button(win,`86`text = '2',`87`width = 4,`88`height = 2,`89`font = digit_font,`90`command = partial(digit_operator_press, '2'))`91`digit3 = Button(win,`92`text = '3',`93`width = 4,`94`height = 2,`95`font = digit_font,`96`command = partial(digit_operator_press, '3'))`97`digit4 = Button(win,`98`text = '4',`99`width = 4,`100`height = 2,`101`font = digit_font,`102`command = partial(digit_operator_press, '4'))`103`digit5 = Button(win,`104`text = '5',`105`width = 4,`106`height = 2,`107`font = digit_font,`108`command = partial(digit_operator_press, '5'))`109`digit6 = Button(win,`110`text = '6',`111`width = 4,`112`height = 2,`113`font = digit_font,`114`command = partial(digit_operator_press, '6'))`115`digit7 = Button(win,`116`text = '7',`117`width = 4,`118`height = 2,`119`font = digit_font,`120`command = partial(digit_operator_press, '7'))`121`digit8 = Button(win,`122`text = '8',`123`width = 4,`124`height = 2,`125`font = digit_font,`126`command = partial(digit_operator_press, '8'))`127`digit9 = Button(win,`128`text = '9',`129`width = 4,`130`height = 2,`131`font = digit_font,`132`command = partial(digit_operator_press, '9'))`133`digit0 = Button(win,`134`text = '0',`135`width = 9,`136`height = 2,`137`font = digit_font,`138`command = partial(digit_operator_press, '0'))`139`divide_op = Button(win,`140`text = '/',`141`width = 4,`142`height = 2,`143`font = digit_font,`144`foreground = '#FFFFFF',`145`background = '#10a605',`146`command = partial(digit_operator_press, ' / '))`147`multiply_op = Button(win,`148`text = '*',`149`width = 4,`150`height = 2,`151`font = digit_font,`152`foreground = '#FFFFFF',`153`background = '#10a605',`154`command = partial(digit_operator_press, ' * '))`155`minus_op = Button(win,`156`text = '-',`157`width = 4,`158`height = 2,`159`font = digit_font,`160`foreground = '#FFFFFF',`161`background = '#10a605',`162`command = partial(digit_operator_press, ' - '))`163`plus_op = Button(win,`164`text = '+',`165`width = 4,`166`height = 2,`167`font = digit_font,`168`foreground = '#FFFFFF',`169`background = '#10a605',`170`command = partial(digit_operator_press,' + '))`171`point_op = Button(win,`172`text = ',',`173`width = 4,`174`height = 2,`175`font = digit_font,`176`command = partial(digit_operator_press, '.'))`177`equal_op = Button(win,`178`text = '=',`179`width = 10,`180`height = 1,`181`font = digit_font,`182`foreground = '#FFFFFF',`183`background = '#0570A6',`184`command = equal_press)`185186`# 定义回车键的事件处理函数`187`win.bind('<Return>', enter_press)`188189`# 将按钮放置到界面`190`display.grid(row = 0, column = 0, columnspan = 5,`191`sticky = 'news')`192`delete_op.grid(row = 1, column = 0, columnspan = 2,`193`sticky = 'news')`194`plusminus_op.grid(row = 1, column = 2, sticky = 'news')`195`copy_op.grid(row = 1, column = 4, sticky = 'news')`196`digit1.grid(row = 2, column = 0, sticky = 'news')`197`digit2.grid(row = 2, column = 1, sticky = 'news')`198`digit3.grid(row = 2, column = 2, sticky = 'news')`199`digit4.grid(row = 3, column = 0, sticky = 'news')`200`digit5.grid(row = 3, column = 1, sticky = 'news')`201`digit6.grid(row = 3, column = 2, sticky = 'news')`202`digit7.grid(row = 4, column = 0, sticky = 'news')`203`digit8.grid(row = 4, column = 1, sticky = 'news')`204`digit9.grid(row = 4, column = 2, sticky = 'news')`205`digit0.grid(row = 5, column = 0, columnspan = 2,`206`sticky = 'news')`207`point_op.grid(row = 5, column = 2, sticky = 'news')`208`divide_op.grid(row = 2, column = 4, sticky = 'news')`209`multiply_op.grid(row = 3, column = 4, sticky = 'news')`210`minus_op.grid(row = 4, column = 4, sticky = 'news')`211`plus_op.grid(row = 5, column = 4, sticky = 'news')`212`equal_op.grid(row = 6, column = 0, columnspan = 5,`213`sticky = 'news')`214215`

我们首先从`tkinter`模块导入所有类。此外，我们的计算器的“显示”部分将使用特殊字体，因此我们还从`font`模块导入所有内容。我们需要最后一个导入语句，以简化事件函数，这些函数将响应用户的数字输入。稍后会详细讲解。

第6至30行：按钮的事件处理函数

这些是响应不同用户操作的事件函数。我们将在最后详细介绍这些函数，但首先我们想先看一下界面。了解界面后，也更容易理解事件处理函数是如何工作的。

第33至38行：应用程序的窗口

我们的计算器应该有一个黑色背景，并且窗口大小是固定的，用户不能更改。

第40至52行：字体和显示

接下来，我们定义了两种字体，`digits_font`用于计算器键上的数字，`display_font`用于计算器的显示部分。显示本身具有绿色前景和黑色背景色。通过`display['anchor'] = 'e'`，我们将其内容对齐到“东边”，即右对齐。

第54至184行：创建按钮

接下来，我们为窗口`win`创建按钮，这些按钮具有多个属性，具体包括它们的标签（`text`）、宽度和高度（以文本字符为单位）、字体（`font`）、前景色（`foreground`）和背景色（`background`），以及用户点击按钮时调用的事件处理函数（`command`）。

对于事件处理函数，我们使用一个小技巧，避免为每个数字和每个运算符编写单独的事件处理函数。我们只定义了一个事件处理函数，命名为`digit_operator_press()`，并传入一个参数，即相应的数字或运算符。但`tkinter button`对象的`command`选项必须传入一个函数对象，而不能传入带参数的函数调用。因此，我们使用`functools`模块中的`partial`函数来创建一个函数对象，其中参数已经“预先嵌入”。由于`partial()`的返回值是一个类似于`function`对象的对象，但它已经包含了参数值，因此我们可以将这个返回值作为按钮的`command`选项的值。

第186至187行：`<ENTER>`键的事件处理函数

为了使得不仅通过点击界面上的等号按钮触发计算，还能通过按键盘上的`<ENTER>`键触发计算，我们将一个事件处理函数（第29至30行）绑定到按下`<ENTER>`键的事件上，函数的作用仅仅是调用当点击等号按钮时触发的事件处理函数（第24至25行）。我们仍然需要分开这两个事件处理函数，因为处理按钮点击的事件处理函数默认会接收一个事件对象作为参数，即使我们不处理它，也必须接受这个参数。

考虑到这些，让我们快速看看其他的事件处理函数：

+   `digit_operator_press()`（第6–8行）：事件处理程序将被点击的数字或算术运算符作为参数传递。按下的按钮的值简单地附加到显示区域中现有的内容上。

+   `delete_press()`（第11–12行）：清空显示区域的内容。

+   `copy_press()`（第15–17行）：首先清空剪贴板，然后将显示区域的当前内容追加到剪贴板中。`clipboard_clear()`和`clipboard_append()`这两个函数用于此目的，它们都由`Tk`类方便地提供，因此也可以用于我们的窗口对象`win`。

+   `plusminus_press()`（第20–21行）：当按下加减按钮时，我们简单地在当前显示内容前面添加一个减号。严格来说，我们应该检查是否已经存在一个减号，然后将其移除。但就像处理其他输入一样（例如，我们不检查用户是否连续输入两个运算符），我们在这一点上让自己轻松一些，并依赖用户的常识。

+   `equal_press()`（第24–25行）：这是之前提到的事件处理程序，当用户请求计算结果时被调用。在这里，我们使用`eval()`函数，它会评估一个Python表达式并返回其结果。在我们的案例中，Python表达式就是用户输入并显示在计算器显示区域的数字和运算符的序列。然而，`eval()`也可以用于执行作为字符串参数传递的完全任意的Python代码。

第189–213行：将按钮放置在界面上。

现在我们只需要将显示区域和按钮放置在界面上。为此，我们需要`grid`几何管理器，因此我们使用`grid()`方法来为各个控件指定它们在网格中的位置，具体通过指定它们的`row`和`column`号。通过`columnspan`选项，我们可以使某些元素横向扩展跨越多个网格单元，例如显示区域。通过`sticky`选项的值`news`（`north + east + west + south`），我们指定各自网格单元中的元素应完全扩展，即填充整个单元。

第215–216行：事件循环。

使用`mainloop()`我们开始处理计算器的事件。从现在起，用户界面会通过调用相应的事件处理程序来响应用户的输入。

## 22.3 处理文件

在Python中处理文件非常简单。这个过程分为三个步骤，和大多数其他编程语言类似：

1.  1.

    文件被打开（可能在第一时间被创建）。

1.  2.

    文件被处理（它被读取、写入或追加）。

1.  3.

    文件在所有工作完成后关闭。

打开文件：文件由`文件对象`表示。我们使用标准的Python函数`open(filepath, mode)`来创建文件对象。参数`mode`描述了文件要以何种编辑模式打开。模式的可能值包括：

+   `"w"`: 文件以`写入`模式打开。文件指针被设置到文件的开始位置。文件的现有内容将被完全替换。如果文件不存在，它将被新建。此模式下无法从文件读取内容。

+   `"a"`: 文件以`追加`模式打开。文件指针被放置在文件的末尾。写入到文件的内容将被附加到文件末尾。此模式下无法从文件读取内容。

+   `"r"`: 文件以`读取`模式打开。文件指针被设置到文件的开始位置。此模式下无法向文件写入内容。

+   `"r+"`: 文件以`读取`和`写入`模式打开。

注意，如果你在Windows系统上工作，你必须用另一个反斜杠来`转义`路径中分隔符的反斜杠，否则Python会将它们视为对`后续字符`的转义尝试，并为其分配特殊的控制功能（如果你不再熟悉转义，回去复习►第[11.2.2节](474412_1_En_11_Chapter.xhtml#Sec4)）。例如，如果我们想在`C:\Programming`目录中以写入模式打开`test.txt`文件，我们首先让`open()`函数创建一个相应的文件对象（为了简化起见，我们称之为`file`）：`file = open("C:\\Programming\\test.txt", "w")`

该对象具有许多属性，帮助我们更好地理解它的特征：`file.name` 返回文件的完整路径，`file.mode` 返回文件的打开模式。此外，可以使用 `file.readable()` 和 `file.writable()` 方法来确定文件是否可读和/或可写，每个方法返回一个 `bool` 值。

编辑文件

要`写入`文件，文件对象提供了 `write(text)` 和 `writelines(lines)` 方法。

`write()` 只是将`一个`字符串写入文件，除非 `text` 末尾包含换行符转义序列 `\n`（例如 `"This is a newline\n text"`），否则不会自动添加换行符。

相比之下，`writelines()` 会写入`多个`作为数组传递的字符串；该函数名有些误导，因为 `writelines()` 也不会在每个字符串末尾写入换行符。因此，如果你希望每个字符串后面有换行符，你需要手动添加：

`lines = ["line 1\n", "line 2\n"] file.writelines(lines)`

每个写入方法都会返回写入的字符数作为返回值。

要从文件中*读取*，可以使用 `read()`、`readline()` 和 `readlines()` 函数。`read()` 读取*整个*文件内容并将其作为字符串返回。通过一个可选参数，可以读取*一定数量的字符*（从文件指针当前位置开始计算）。文件指针从文件开头开始，并随着每次读取操作相应移动。请参见以下示例文件：

第一行一行 还有一行 最后一行

使用 `read(3)`，在打开文件后（此时文件指针位于文件开头），我们首先会读取字符串 `"Lin"`。之后，文件指针位于 `"line"` 的 `"e"` 上。接着，`read(19)` 将返回接下来的 19 个字符，即 `"e number one\nOne mo"`。请注意，换行符也算作一个字符，且是*正好一个*字符（尽管它在转义序列中表示为 `\n`，由两个字符组成）。此时，重新读取后，文件指针位于 `"more"` 的 `"r"` 上。

`readline()` 和 `readlines()` 函数与 `read()` 的处理方式不同；它们分别读取一行或多行*内容*。`readline()` 总是读取精确的下一行，而 `readlines()` 则读取所有行或传递的行数（作为可选参数），并返回一个*字符串数组*。因此，`readline()` 和 `readlines(1)` 的方法调用有所不同，`readline()` 调用的结果是一个 `str` 值，而 `readlines()` 返回一个数组，在此案例中仅包含一个字符串元素。

如果文件指针不在行的开头，而是在行的中间（例如在上面调用 `read(3)` 后），那么 `readline()` 和 `readlines()` 将从文件指针当前位置的字符开始读取。此时，行的开头（在本例中是已经用 `read()` 读取的前三个字符）将不再被读取。

在读取时，你可以使用`seek(*****characterindex*****)`将文件指针设置到由`characterindex`指定的字符位置，计数从文件的开始处。文件对象的`tell()`方法返回文件指针的当前位置。

顺便提一句：如果你以`"r+"`模式（读 *和* 写）打开文件，实际上可以使用同一个文件对象进行这两项操作。然而，写入始终是在文件的末尾进行，读取则是在文件指针的当前位置进行，其行为与以`"r"`模式打开文件时相同。

关闭文件

编辑完文件后，用`***file*****.close()`方法关闭它。文件对象将继续存在，但其属性`***file*****.closed`将变为`True`，表示该对象不再可用于读写。然而，由于文件对象仍然携带文件路径作为其`name`属性，你可以简单地“重新激活”它：

`file = open(file.name, "r")` 22.2 [15 min]

编写一个程序，要求用户输入文件的名称（包括完整路径）。然后，按用户指定的百分比显示文件内容的预览。预览显示中应删除换行符，使显示尽可能紧凑。

## 22.4 练习：开发一个简单的文本编辑器

以下练习结合了你在本章中学到的许多内容，用来开发一个有用的小应用。

任务是用`tkinter`编程开发一个简单的文本编辑器。该编辑器应允许你创建新文件或打开现有文件，然后编辑并保存文件，无论是以当前名称还是新名称保存。同时，用户应该能够将文本复制到剪贴板并从剪贴板粘贴。编辑器的命令应通过菜单或按钮栏选择。

你需要使用来自`tkinter`模块`scrolledtext`的小部件`ScrolledText`。因此，即使你使用`from tkinter import *`导入了`tkinter`模块的其他小部件，也请确保在导入中包含`from tkinter.scrolledtext import ScrolledText`这一行。

充分测试你的程序！

完成此任务的预估时间为120分钟。你应该在一个安静的地方集中精力进行这项开发工作。如果任务仍然显得太具挑战性，不要花费几个小时尝试自己开发编辑器，而是阅读样本解决方案中的代码，先试着理解它，而不要参考解决方案中的解释性备注。

## 22.5 总结

在本章中，我们学习了如何通过控制台输入和输出数据。我们还研究了如何在Python中实现图形用户界面，以便用户能够方便地与程序进行交互。

确保从本章中记住以下几点：

+   在Python控制台中，你可以使用内置的Python函数`print(object)`来打印对象。

+   可以使用`input(prompt)`方法向用户请求信息，该方法总是返回用户输入的字符串（因此如果需要，必须将用户输入转换为其他类型）。

+   图形用户界面（GUI）可以通过`tkinter`库轻松实现，`tkinter`是 Python 标准库的一部分。

+   一个`tkinter`程序通常包含以下几个部分：使用同名构造函数创建一个`Tk`对象，创建和配置控件（小部件），定义控件的布局（使用几何管理器），并启动事件处理（`Tk`对象的`mainloop()`方法）。

+   `tkinter`图形用户界面中的最重要控件（小部件）包括`Button`（按钮）、`Menu`（菜单）、`Entry`（文本输入框）、`Label`（文本显示框）、`Checkbutton`（多选框）、`Radiobutton`（单选框）和`Listbox`（列表框，支持单选或多选文本条目）。

+   `tkinter`（更具体地说，是`tkinter`模块的`filedialog`）提供了一些常用的标准对话框：`messagebox`（有多个变体，显示不同的图标和按钮）用于显示文本消息；`askopenfilename()`和`asksaveasfilename()`用于在打开或保存文件时查询文件路径。

+   控件通过选项进行配置；一些选项（但不是它们的值！）几乎所有控件都有（例如，`background`颜色和`font`），而其他选项则是特定于某个控件的。

+   所有控件都有`config(*****option*** **=** ***value*****, ...)`方法，可以用来设置选项的值。此外，这些选项也可以通过`widget['option']`的方式访问，就像访问字典一样。

+   控件通过几何管理器在程序界面上进行排列；`tkinter`有三个几何管理器：`pack`（将控件直接排列在彼此旁边或下方）、`grid`（沿着一个虚拟网格排列）和`place`（通过指定相对于参考点的坐标来排列），它们分别通过每个控件的`pack()`、`grid()`和`place()`方法调用。

+   要从文件读取或写入数据，首先需要使用内置的 Python 函数`open(*****filename*****, **mode**)`打开文件；该函数返回一个`File`对象。

+   编辑文件的模式有`r`（读取）、`w`（写入）、`a`（追加）和`r+`（读写）。

+   `File`对象的`read()`和`readlines()`方法以及`write()`和`writelines()`方法可以用来从文件中读取或写入数据。

+   `File`对象的`close()`方法在处理完成后关闭文件。

## 22.6 练习题解答

练习 22.1 `# 第一个选项：三条 print() 命令（每条命令自动以 \n 结尾） print('第一行') print('第二行') print('第三行') # 第二个选项：一个字符串，行之间由 \n 转义符分隔 print('第一行\n第二行\n第三行') # 第三个选项：输出三个字符串对象，使用 \n 转义符作为分隔符 print('第一行', '第二行', '第三行', sep = '\n')` 练习 22.2

程序可能如下所示：

`filename = input("请输入文件名（包括路径）：") percent = input("要预览的内容百分比" + "（整数，例如 10 表示 10%）：") previewfile = open(filename, "r") contents = previewfile.read() previewfile.close() content = contents.replace("\n", "") length_total = len(content) length_preview = int(length_total * int(percent) / 100) print("### 预览：", length_preview, "个字符，共", length_total, "个字符 ###") print(content[0:length_preview], "\n####\n")`

文件首先以读取模式（`"r"`）打开，并通过`read()`读取其全部内容。然后，文件可以关闭，因为字符串变量`content`现在包含了整个文件的内容，我们将继续处理这些内容。在通过使用字符串方法`replace()`移除换行符转义序列`\n`清理内容后，我们在最后一条语句中选择所需的字符数，这个字符数是根据用户指定的预览百分比计算出来的，并将其显示在屏幕上。选择字符串中的字符时，必须确保选择的范围是整数。我们通过使用`int()`将结果作为整数变量存储来实现这一点，以计算预览长度。

编程任务`文本编辑器`在文本编辑器的开发过程中，当然有许多不同的变体。这里呈现的解决方案的用户界面可以在◘ `图 22.10` 中看到。 ![](../images/474412_1_En_22_Chapter/474412_1_En_22_Fig10_HTML.jpg)

一个截图，窗口标题为`我的个人文本编辑器`。窗口顶部有一些按钮，如`新建`、`打开`和`保存`。在下面的字段中给出了三行文本，分别为`第一行`、`另一行`和`最后一行`。

`图 22.10`

我们文本编辑器的`用户界面`

代码如下所示：

1 **从** tkinter **导入** *2 **从** tkinter.filedialog **导入** *3 **从** tkinter.scrolledtext **导入** ScrolledText45 *# 定义按钮和菜单的事件处理函数*67 **定义** new_press():8 **全局** filename9 text.delete(1.0, 'end')10 filename = ''11 status['text'] = '未保存的新文件'121314 **定义** open_press():15 **全局** filename16 fname = askopenfilename(defaultextension = 'txt',17 filetypes = [('文本文件', '*.txt'),18 ('所有文件', '*.*'),],19 title = '打开....',20 initialdir = 'C:\\Windows')21 textfile = open(fname, 'r')22 text.delete(1.0, 'end')23 text.insert(1.0, textfile.read())24 textfile.close()2526 status['text'] = '文件 "' + fname + '" 已打开。'27 filename = fname282930 **定义** saveas_press():31 **全局** filename32 fname = asksaveasfilename(defaultextension = 'txt',33 filetypes = [('文本文件', '*.txt'),34 ('所有文件', '*.*'),],35 title = '另存为...',36 initialdir = 'C:\\Windows')37 textfile = open(fname, 'w')38 textfile.write(text.get(1.0, 'end'))39 textfile.close()4041 status['text'] = '文件 "' + fname + '" 已保存。'42 filename = fname434445 **定义** save_press():46 **全局** filename47 textfile = open(filename, 'w')48 textfile.write(text.get(1.0, 'end'))49 textfile.close()5051 status['text'] = '文件 "' + filename + '" 已保存。'525354 **定义** copy_press():55 selection = text.selection_get()56 text.clipboard_clear()57 text.clipboard_append(selection)585960 **定义** paste_press():61 text.insert(text.index('insert'), text.clipboard_get())626364 **定义** copy_press_key(event):65 copy_press()666768 **定义** paste_press_key(event):69 paste_press()707172 **定义** quit_press():73 win.quit()747576 *# 创建应用窗口*77 win = Tk()78 win.title('我的个人文本编辑器')79 win.geometry('760x490')80 win.resizable(height = True, width = True)818283 # 设置菜单栏84 menubar = Menu(win)85 win.config(menu = menubar)8687 file_menu = Menu(menubar, tearoff=0)88 edit_menu = Menu(menubar, tearoff=0)8990 menubar.add_cascade(label = '文件', menu = file_menu)91 menubar.add_cascade(label = '编辑', menu = edit_menu)9293 file_menu.add_command(label = '新建',94 command = new_press)95 file_menu.add_command(label = '打开...',96 command = open_press)97 file_menu.add_command(label = '保存',98 command = save_press)99 file_menu.add_command(label = '另存为...',100 command = saveas_press)101 file_menu.add_separator()102 file_menu.add_command(label = '退出',103 command = quit_press)104105 edit_menu.add_command(label ='复制',106 command = copy_press)107 edit_menu.add_command(label ='粘贴',108 command = paste_press)109110111 # 创建控件元素112 new_button = Button(win,113 text = '新建',114 height = 3,115 width = 16,116 command = new_press)117 open_button = Button(win,118 text = '打开...',119 height = 3,120 width = 16,121 command = open_press)122 save_button = Button(win,123 text = '保存',124 height =3,125 width = 16,126 command = save_press)127 saveas_button = Button(win,128 text = '另存为...',129 height = 3,130 width = 16,131 command = saveas_press)132 seplabel = Label(win,133 text='',134 height =3,135 width= 3)136 copy_button = Button(win,137 text = '复制',138 height = 3,139 width = 16,140 command = copy_press)141 paste_button = Button(win,142 text = '粘贴',143 height = 3,144 width = 16,145 command = paste_press)146147 text = ScrolledText(win)148 text.bind('<Control-c>', copy_press_key)149 text.bind('<Control-v>', paste_press_key)150151152 *# 设置状态栏*153 status = Label(win,154 text = '没有文件打开。',155 anchor = 'w',156 background = '#FFEFC4')157 filename = ''158159160 *# 将按钮放置到界面*161 new_button.grid(row = 0, column = 0, sticky = 'news')162 open_button.grid(row = 0, column = 1, sticky = 'news')163 save_button.grid(row = 0, column = 2, sticky = 'news')164 saveas_button.grid(row = 0, column = 3, sticky = 'news')165166 seplabel.grid(row = 0, column= 4, sticky = 'news')167 copy_button.grid(row = 0, column = 5, sticky = 'news')168 paste_button.grid(row = 0, column = 6, sticky = 'news')169170 text.grid(row = 1, column = 0, columnspan = 7, pady = 10,171 sticky = 'news')172173 status.grid(row = 2, column = 0, columnspan = 7,174 sticky = 'news')175176177 *# 事件循环*178 win.mainloop()

一旦清楚了界面由哪些组件构成，我们将详细了解事件处理程序是如何工作的。

第76到80行：`应用程序窗口`

`win`窗口被创建并作为`Tk`对象进行缩放。它应该可以被用户调整大小。

第83到108行：`菜单设置`

为`win`窗口创建了一个新的菜单栏，并在菜单栏上放置了两个下拉菜单，`file_menu`和`edit_menu`。菜单项随后逐渐添加到菜单中。

第111到149行：`创建剩余控件`

这里创建了按钮和文本输入框。此外，事件处理程序被绑定到文本输入框的两个事件上，用来处理按下键组合`<CTRL>+<C>`（复制）和`<CTRL>+<V>`（粘贴）。

第152到157行：`准备状态栏`

我们创建了一个标签作为黄色的状态栏，当前打开的文件名称会显示在上面。

第160到174行：`将控件放置到界面上`

控件通过使用`grid`几何管理器在用户界面上排列，以便它们完全填充各自的“网格单元格”（`sticky = 'news'`，即`north east west south`）。

第177到178行：`事件循环`

`mainloop()`开始了我们编辑器的事件处理。这使得用户界面能够对用户的输入作出反应。

`事件处理器`（第5到73行）

+   `new_press()`: 通过首先删除`ScrolledText`字段的内容来创建一个文件；从第1行（文本小部件中的行号从1开始）第0列（列号从0开始）删除到末尾。可以使用常量`END`来代替字符串`'end'`。

    全局变量`filename`通过`global filename`语句确保访问权限（否则在`new_press()`中会创建一个同名的`local`变量），并重新初始化为空字符串，状态栏的文本也随之更新。

+   `open_press()`: 在这里，我们使用`askopenfilename()`函数来获取我们要打开的文件路径。然后，文件以读取模式通过`open()`打开，使用`read()`读取的内容被放入我们的文本框中，之后文件再次通过`close()`关闭。

+   `save_as_press()`和`save_press()`：对于保存，我们基本上和打开一样；不过文件是以写入模式打开的，以便`write()`方法可以将我们通过`ScrolledText`小部件的`get()`方法获取的文本写入编辑器。在`save_as_press()`中，我们通过`tkinter`的`asksaveasfilename()`函数来询问文件名，而在`save_press()`中，我们使用已经在使用的文件名来保存文件。因此，只有在文件已经打开或`ScrolledText`小部件的内容已经保存到文件时，这才有效。

+   `copy_press()`和`paste_press()`，`copy_press_key()`和`paste_press_key()`：在复制文本时，我们首先使用`ScrolledText`小部件的`selection_get()`方法获取所选文本，然后用`clipboard_clear()`清空剪贴板，最后用`clipboard_append()`方法将要复制的文本插入到剪贴板。

    在插入文本时，我们首先确定当前插入位置，即在我们的`ScrolledText`小部件中的光标位置，使用`index('insert')`，然后获取剪贴板内容，使用`clipboard_get()`将其插入到该位置。

    `copy_press_key()`和`paste_press_key()`函数是我们绑定到按键事件的（第148/149行），它们调用我们之前讨论的事件处理程序，但它们是必要的，因为通过`bind()`绑定到事件的事件处理程序作为参数传递了一个事件对象。因此，这些事件处理程序必须提供一个参数，而我们通过`command`选项绑定到按钮和菜单项的事件处理程序则不需要任何参数。
