© 作者(s)，独家授权给Springer Fachmedien Wiesbaden GmbH，属于Springer Nature的一部分 2024J. L. Zuckarelli《学习使用Python和JavaScript编程》[https://doi.org/10.1007/978-3-658-42912-6_26](https://doi.org/10.1007/978-3-658-42912-6_26)

# 26. 调试与错误处理：如何以结构化的方式查找和修复错误

Joachim L. Zuckarelli^([1](#Aff2) )(1)慕尼黑，德国概述

错误是日常编程的一部分，虽然令人不愉快，但遗憾的是无法避免的事实。因此，为了总结我们对Python基础的学习，我们将讨论如何查找、分析和处理错误。

本章你将学习：

+   如何通过在程序代码中适当的检查来使程序更稳健，例如防止用户输入错误

+   如何通过异常捕捉运行时错误，并如何有序地处理这些错误

+   如何使用*PyCharm*的调试工具在开发过程中查找和分析错误

## 26.1 运行时的错误处理

### 26.1.1 通过有针对性的检查捕捉错误

在► 第[16](474412_1_En_16_Chapter.xhtml)章中，我们定义了*运行时错误*，即仅在具体程序执行的情况下才会出现的错误。的确，有些应用场景中，代码能够完美实现预定目标且没有错误；这些场景正是开发时的重点。换句话说，程序是基于这些场景进行测试的。然而，在执行过程中可能会出现一些程序*不*按预期运行的情况。尤其是在程序执行失控，程序“崩溃”时，即以错误终止（且不重新启动程序）后无法继续使用。

这种错误的常见原因之一是变量类型转换的问题。考虑以下例子：

**from** math **import** sqrtx_str = input('请输入一个整数：')x_int = int(x_str)print(sqrt(x_int))

程序从用户处读取一个数字，并计算其平方根。使用的是**math**模块中的**sqrt()**函数。

由于**input()**函数总是返回字符串，因此用户输入必须先转换为浮动变量，即浮点数，使用常规类型转换（如果你不再熟悉此操作，请回顾► 第[21.5](474412_1_En_21_Chapter.xhtml#Sec12)节）。如果你现在启动程序并输入例如25，输出将是平方根，也就是5。程序看起来似乎没有错误，至少在我们测试的应用场景中没有错误。但如果用户输入的不是数字而是字符串（例如**'hello'**）呢？我们会立即收到Python的一个错误信息：

x_float = int(x_str)**ValueError: 无法将字符串转换为浮点数：'hello'。**

当然，可以通过首先在**if**语句中检查用户输入是否为数字，轻松捕获错误。我们的程序可以像这样写，例如：

**from** math **import** sqrtx_str = input('请输入一个正整数：')**if** x_str.isnumeric():x_int = int(x_str)print(sqrt(x_int))**else**:print('您的输入 "', x_str,'" 不是一个正整数！', sep='')

通过这种方式，我们“免疫”了程序对用户输入错误的敏感性。这使得程序更加“健壮”，现在它可以处理更多可能在现实世界中发生的场景，而不会崩溃。

也许你已经识别出另一个可能的错误来源：负数的输入。我们似乎没有捕获这种“错误输入”。然而，实际上我们已经做到了，因为**isnumeric()**检查字符串是否仅包含数字。字符串中包含的十进制分隔符或负号会自动导致字符串不被视为数字。这样会触发我们自定义的错误信息，因此**sqrt()**函数永远不会接收到负数。令人恼火的是，Python本身没有一个函数来确定字符串是否包含任何形式的数字，即可能包含符号、十进制分隔符和指数的数字。因此，我们在这里简化了，只允许输入正整数。

### 26.1.2 Try-Except 语句

不是所有在运行时可能出现的问题都能像上述示例那样明确描述，以便我们用条件来捕获它们。例如，在打开文件进行写入时，可能会有多种原因导致打开失败。例如，如果文件已经存在，它可能是只读的，或者磁盘可能是只读的，或者磁盘上没有足够的空间来写入文件。

现在，当然，最好尽可能捕获这些潜在的错误源，以便能够准确地告诉用户是什么导致了错误，从而帮助他解决问题，例如，去除写保护或释放磁盘上的足够空间。事实上，即使通过有针对性的检查消除了某些可能的错误原因，仍然会有其他潜在的错误源被忽视或无法预见，特别是在处理像文件系统这样复杂的操作时。因此，Python中有另一种处理错误的方式，即使用*Try-Except 语句*，我们在►节[16.​2](474412_1_En_16_Chapter.xhtml#Sec2)中学习过。这个语句由关键字**try**、**except**、**else**和**finally**组成，后两者是可选的。

这样，我们的程序就可以像这样写：

x_str = input('请输入一个数字：')**try**:x_float = float(x_str)print(sqrt(x_float))**except**:print('您的输入 "', x_str,'" 不是一个数字！', sep='')

关键字**try**后面跟着一个代码块，其中的语句是“尝试”执行的。如果执行过程中没有错误，程序会继续执行。如果执行失败并且出现错误，紧跟着**except**关键字的代码块将会被执行。然而，如果一切按计划运行，**except**代码块将会被跳过，程序会在其后继续执行。在这里，我们现在可以输入带有小数点分隔符的分数以及负数。请输入一个负数！会发生什么呢？你会看到错误信息**'Your input is not a number!'**。这当然不对；问题出在别的地方，具体来说是取平方根时出现问题。程序因为你试图对一个负数取平方根而终止，并报错。Try-Except结构会捕获*所有*可能发生的错误，包括由于**sqrt()**函数的负数参数而导致的错误。

现在我们有两种选择：要么我们将错误信息表述得更为通用一些（“发生了一个错误”），但这显然对用户没有什么帮助，要么我们尝试更清楚地区分错误的原因。这可以通过*异常类*来实现。在Python中，像许多其他编程语言一样，错误被称为“异常”，也就是程序出现不按预期运行的情况。现在，异常类处理的是*某一类*错误（即异常）。例如，异常类**ZeroDivisionError**处理的是除法中除数为0的异常。

顺便提一下，错误的异常类也会显示在Python的错误信息中。这样，你就可以确定需要处理的异常类是哪一种。在我们的例子中，**except**关键字可以帮助我们显式捕获特定类型的异常。然而，在我们的例子中，这个帮助是有限的，因为无论是尝试将一个不包含数字的字符串转换为**float**变量，还是计算负数的平方根，都会导致相同的异常类**ValueError**。但现在假设我们将程序扩展，加入一行代码来计算输入数字的倒数。这样，我们就可以更明确地区分两种可能的异常类：

x_str = input('请输入一个数字：')**try**:x_float = float(x_str)root = sqrt(x_float)reciprocal = 1/x_float**except** ValueError:print('你的输入 "', x_str, '" 不是一个数字或是一个负数！', sep='')**except** ZeroDivisionError:print('不能计算0的倒数！')**except**:print('其他错误！')**else**:print('平方根:', root)print('倒数:', reciprocal)

在这个变体中，我们分别捕获 **ValueError** 和 **ZeroDivisionError** 类型的异常，因此可以发出更具体的错误信息。此外，你还会注意到与我们之前使用的 Try-Except 结构相比，有两个进一步的不同之处。首先，除了两个 **except** 关键字（每个都处理特定的异常类）之外，你还会看到一个没有指定异常类的 **except**。这种结构确保了处理任何*其他*不属于上述两种异常类的错误。其次，你会看到一个 **else** 块；它包含的语句只有在没有抛出异常的情况下才会执行（在程序员术语中称为“抛出”异常）。

当然，**print** 语句也完全可以包含在 **try** 代码块中。在这种情况下，只有在没有异常发生时，它们才会被执行。然而，一般来说，我们会尽量将 **try** 块保持尽可能小，以便明确标示出你担心可能引发异常的“危险”操作。

关键字 **try**、**except** 和 **else** 必须始终按此顺序使用。**else** 是可选的，因此可以省略。

我们没有考虑关键字 **finally**，它可以可选地跟在 **else** 代码块后面，并且其代码块包含的语句无论是否发生异常都会被执行，*无论如何*。如果在 **except** 块内，当前函数通过 **return** 退出，或者当前循环通过 **break** 退出，那么 **finally** 的使用就显得特别重要。整个 Try-Except 结构后的语句将不再执行，但 **finally** 代码块中的语句会执行。只有在这些语句执行完毕后，函数或循环才会退出。

26.1 [15 min]

编写一个程序，接受用户输入一个数字，一个运算符（加法、减法、乘法、除法）以及另一个数字，然后执行描述的算术运算并显示结果。程序应尽可能地健壮，能够应对执行过程中可能发生的所有错误。

! 26.2 [15 min]

任务 26.1 中的程序可能有一种替代的实现方式，它展示了类似的健壮性，但不使用 **try**…**except** 结构？

## 26.2 开发过程中的故障排除

在开发过程中，当使用像 *PyCharm* 这样的集成开发环境时，有几个非常方便的调试工具。最重要的包括 *断点*、*变量和表达式监视* 以及程序代码的 *逐步执行*。这里我们将跳过一个稍微高级一些的话题——自动化测试。自动化测试可以定义某段代码（例如一个函数）期望的结果，然后自动检查当前的函数代码是否真的产生了这个结果。这样，测试就完全是自动化的，不需要手动执行。支持这种测试的 Python 库包括 *unittest* 和 *pytest*。

### 26.2.1 断点

程序执行的停止标志

断点是对程序行的特殊标记，它使得程序只执行到该行，然后停止执行。之后可以重新启动程序执行，所有变量都会恢复到断点停止时的值。

断点可以非常有用，例如，用来测试程序中的某个错误是在哪个点被触发，导致程序崩溃。如果程序能够顺利执行到断点而没有报错，那么错误的原因肯定不在断点上方的代码部分。如果你在 If-Else 结构的代码块中设置了断点，你可以轻松判断这个结构的分支是否真的被执行了，即相应的条件是否满足。如果程序停止了，说明条件满足；如果程序没有停止并一直执行到结束，说明条件显然没有被满足。你还可以利用断点暂停程序执行，查看程序中使用的变量的内容；这可以通过 *监视* 实现，接下来我们将更详细地讨论这一点。

设置和移除断点 在开始正式调试之前，首先必须设置一个断点。为此，请点击代码编辑器中输入区域旁边的边距条，在那里你还可以看到行号。一个红色标记会出现，表示断点的设置。你可以在◘ 图 [26.1](#Fig1) 中看到这一点。再次点击同一位置可以移除断点。当然，如果需要，你也可以在程序中的不同位置设置多个断点。![](../images/474412_1_En_26_Chapter/474412_1_En_26_Fig1_HTML.jpg)

代码片段包括读取目录、启动文件和退出的输入。它有21行，并突出显示了第十三行，代码为 dir_存在 = true。

图 26.1

在 *PyCharm* 中设置了断点的代码

现在你可以在调试模式下执行程序。这可以通过点击工具栏中的甲虫图标（◘ 图 [26.2](#Fig2)），或点击附加在调试控制台左侧的相同图标，或者通过右键点击代码编辑器并选择“调试”选项，或者按下组合键 <SHIFT>+<F9> 来实现。请注意，如果你使用普通的运行功能来运行程序（例如，使用工具栏中的绿色箭头按钮），它将*不会*以调试模式运行！这意味着程序将不会在断点处停下。如果你想调试程序，必须以调试模式启动它。![](../images/474412_1_En_26_Chapter/474412_1_En_26_Fig2_HTML.jpg)

PyCharm 工具栏的截图显示了一组图标。下拉列表的开头显示文件启动器 1。

图 26.2

*PyCharm 工具栏*，带有调试图标（箭头图标右侧的甲虫）

在程序到达断点后，执行会首先暂停。在 PyCharm 应用窗口的下部会显示*调试*控制台。*调试*控制台，正如你在 ◘ 图 [26.3](#Fig3) 中所见，实际上只是一个带有一些特殊功能的*运行*控制台。程序执行总是在断点所在行的*之前*暂停。你可以通过点击*调试*区域水平工具栏中的*恢复程序*图标，或按键盘上的 <F9> 键来恢复程序执行。然后程序将继续运行，直到下一个断点处，或者如果没有其他断点，程序将一直运行到结束。![](../images/474412_1_En_26_Chapter/474412_1_En_26_Fig3_HTML.jpg)

调试控制台的截图显示了四行文本，顶部显示了 Python 程序和 Python 代码的位置。

图 26.3

*PyCharm* 中的调试控制台

你可以随时使用红色的“停止”符号停止程序，这个符号可以在*调试*区域的工具栏中找到，或者在*PyCharm* 应用的标题栏中找到。然后程序会完全重置，即在下一次以调试模式启动时，程序会从头开始运行，并在执行过程中再次停在第一个断点处。

通过右键点击在代码行旁边的红色圆形断点图标，你可以为该断点添加条件。例如，在我们在 ◘ 图 [26.1](#Fig1) 中的示例中，我们可以输入条件 **isdir(directory)==True**。这样，程序在调试模式下仅会在变量 **directory** 确实是一个目录时才会在断点处停下。否则，程序将像断点不存在一样继续执行。

### 26.2.2 变量内容的显示和观察表达式的使用

你会注意到，当断点被触发时，*调试*区域会从*控制台*标签切换到名为*线程与变量*的标签。在这个区域的右侧，你可以看到程序到目前为止使用的变量及其值。如果你点击代码编辑器中的变量名，变量的值也会直接显示在小弹出窗口中（◘ 图[26.4](#Fig4)）。![](../images/474412_1_En_26_Chapter/474412_1_En_26_Fig4_HTML.jpg)

一张截图显示了*线程与变量*标签下的一组变量。它展示了变量choice、dir exists、directory、list di和start file的值。左侧面板显示了主线程。

图26.4

显示代码行后面和鼠标悬停时弹出的变量内容

然而，调试器不仅仅允许你显示变量的内容。你还可以基于变量构造完整的表达式，然后在断点处显示它们的值。由于你监控这些表达式的值，它们也被称为*观察表达式*。将你想要观察的表达式输入到*调试*区域*线程与变量*标签右侧顶部的编辑框中，然后按<ENTER>键。例如，你可能想检查变量**directory**是否包含目录**c:\mydir**。在右侧会出现一个新的条目，表达式为**directory == "c:\\mydir\\"**。一旦你运行程序并且它在调试模式下触及断点，表达式的值将显示出来，如你在◘ 图[26.5](#Fig5)中所见。当然，在构造观察表达式时，你也可以利用Python函数。![](../images/474412_1_En_26_Chapter/474412_1_En_26_Fig5_HTML.jpg)

一个调试控制台窗口的截图。它包括了4行Python代码。

图26.5

*线程与变量*标签中的观察表达式

手动显示变量内容

调试器提供了非常实用的功能，可以根据变量或表达式监视它们的值。然而，通常一个更简单的方法就足以通过显示变量和表达式的值来支持调试：使用**print()**函数输出值！因此，只需在程序中的相关位置插入**print()**语句，你将在*运行*控制台中看到相应的输出。简单得不能再简单了！与断点一样，你当然可以利用这些输出检查程序的某些部分是否被执行。只是不要忘记在调试后移除这些输出语句。你的程序用户会为此感谢你。

### 26.2.3 逐步执行

尤其在处理手表时，但也可以用来确定错误发生的准确位置，一种名为*逐步执行*的调试功能非常有帮助。它按行逐步执行程序，就像在每一行代码上设置了一个断点一样。

当程序达到断点时，你可以开始逐步执行。从那里继续逐步执行，点击 *调试* 区域工具栏中的“Step Over”按钮（◘ 图 [26.6](#Fig6)）或按 <F8> 键。这将执行程序的下一行。再次点击按钮或按 <F8> 会继续执行每点击一次的下一行。这样，你可以逐步执行程序并观察其执行情况。如果想退出逐步执行，点击红色的“停止”图标，或按 <CTRL>+<F2>，就像使用断点时一样。![](../images/474412_1_En_26_Chapter/474412_1_En_26_Fig6_HTML.jpg)

截图显示了“线程和变量”选项卡下的一组变量。它展示了目录、选择、dir_exists、list_dir 和 start_file 的值。左侧面板指示主线程。

图 26.6

使用 Step Over 逐步执行程序

## 26.3 小结

在本章中，我们讨论了 Python 如何通过检查程序中的关键状态并适当处理异常（运行时错误），来处理 *运行时* 错误，以及如何利用调试工具在 *开发时* 预先分析这些错误。

一定要记住本章中的以下要点：

+   通过巧妙地检查关键条件，你可以让程序更具鲁棒性，应对不正确的输入或其他常规程序执行无法保证的情况。

+   运行时错误在 Python 中通过异常表示。

+   可能会产生异常的语句可以被包装在 Try-Except 构造中；它会“尝试”执行语句，并在抛出（“触发”）异常时提供使用自己程序代码进行错误处理的可能性。

+   Try-Except 构造的最简单形式是：**try:** ***code_block*** **except:** ***code_block***；此外，可以明确指定要捕获的异常，这样就可以根据抛出的异常定义不同的错误处理程序，适用于相同的代码段。

+   集成开发环境（IDE），如 *PyCharm*，提供了一些开发期间的错误分析手段；这些手段包括断点（程序代码执行被暂时中止的地方）、监视（在程序运行时显示变量的内容）和逐步执行（由开发者显式触发程序执行下一条语句）。

## 26.4 习题解答

练习 26.1 一个简单的程序可能是这样写的：number1 = input("数字 1：") op = input("运算符（+，-，*，/）：") number2 = input("数字 2：") **try**:**if** op == "+"：result = float(number1) + float(number2) **else**:**if** op == "-"：result = float(number1) - float(number2) **else**:**if** op == "*"：result = float(number1) * float(number2) **else**：result = float(number1) / float(number2) print("结果：", number1, " ", op, " ", number2, ": ", result, sep="") **except**: print("计算时出错：", number1, " ", op, " ", number2, ".", sep="")

要保护的程序部分只需要用一个大的 Try-Except 结构包裹起来。如果在程序执行过程中发生错误，用户将收到一个通用的错误信息。如果关键程序部分（例如将类型为 **str** 的数字输入转换为 **float**）在单独的 Try-Except 结构中执行，那么可以提供更精确的错误描述。程序的其余部分将被执行在前一个 Try-Except 结构的 **except** 块中，这样最终就会形成这些结构的多重嵌套，虽然不容易阅读，但至少可以为用户提供更精确的错误原因分析。

练习 26.2

使用 Try-Except 结构的替代方法——至少在这里的这些情况中——是通过使用适当的条件显式地捕获错误。在下面的程序编写中，检查了一些这样的条件。如果出现错误条件，**bool** 变量 **error** 会被设置为 **True**；另外，**str** 变量 **message** 会填充适当的错误信息。在程序的最后，会检查程序是否没有错误地运行完毕（**error == False**）；如果是这样，变量 **message** 会被赋值为计算的结果。最后，只需将 **message** 的内容输出给用户，它将包含计算结果或错误信息。

这里请注意我们用来检查变量 **number1** 和 **number2** 在通过 **input()** 读取后是否真的包含数字的技巧。**str** 方法 **isdigit()** 用来检查一个 **str** 变量是否只包含数字。当然，用户可能输入了一个小数点（即小数分隔符）。因此，我们首先用 **replace()** 将其去除。我们还检查小数点在字符串中是否最多出现一次，因为如果小数点出现多次，我们就会得到一个无效的“数字”。

所以，正如你所看到的，即使使用条件，你也可以捕获许多错误。然而，这并不是对所有错误都有效。例如，在处理文件时，使用条件来检查所有可能的错误原因是困难的（例如，如果你想从文件中读取，检查文件是否存在）。在这些情况下，使用 **try**…**except** 结构是个好主意。