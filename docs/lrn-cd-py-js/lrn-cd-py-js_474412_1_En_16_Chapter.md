© `作者(s)`，独家授权给`Springer Fachmedien Wiesbaden GmbH`，`Springer Nature`的一部分 2024 `J. L. Zuckarelli`学习使用`Python`和`JavaScript` [https://doi.org/10.1007/978-3-658-42912-6_16](https://doi.org/10.1007/978-3-658-42912-6_16)

# 16. 如何以结构化的方式搜索和修复错误？

`Joachim L. Zuckarelli`^([1](#Aff2) )(1)`慕尼黑，德国概述`

错误是程序员最糟糕的敌人。无论您工作多么小心，错误总会潜入。测试程序以检测和消除错误，因此是编程的重要部分。错误的表现形式可能是程序根本无法运行，执行过程中崩溃，或者即使运行到最后，它仍然无法按预期工作。

可以区分在`开发时`发生的错误，即在编写程序时发生的错误，以及在`运行时`发生的错误，即当程序被执行时发生的错误。

在本章中，您将学习：

+   存在什么类型的错误以及它们的原因是什么

+   如何通过处理异常捕获运行时错误并使其无害

+   在测试程序时如何巧妙地进行

+   什么是调试器

+   调试器的功能，如“`断点`”、“`单步模式`”和“`变量观察/监视`”是什么，以及如何使用它们来理解错误的位置和原因

+   如何使用临时的、额外的输出在没有调试器的情况下诊断程序中的错误。

## 16.1 开发时的错误

在开发时已经发生的错误要么是语法错误，其中程序的“语法”不正确，一个或多个语句不符合“句子结构规则”，要么是算法错误；这些错误是由于程序代码形式上正确，但根本不是程序员想要做或实现的准确实现。

在发生`语法错误`时，编译器或解释器通常会通过中止程序的编译或执行，并提供错误信息来进行帮助。这个错误信息通常会提供关于发生了什么类型的错误以及在代码中的哪个位置（通常通过行号或程序部分的名称）可能是原因的信息。这样的错误可能是由于某个变量没有被声明，如果您在程序中使用该变量，编译器或解释器将在此处失败。有时，错误信息有些难以理解，只有熟悉编程语言内部结构的程序员才能理解编译器/解释器想要表达的意思。在这种情况下，通常在互联网上搜索会有所帮助，因为其他程序员也会对该错误信息感到困惑。您将在`StackOverflow`上找到多种语言的错误解决方案。

`算法`错误通常更难以检测和理解。为此，请使用►节`[16.4](#Sec4)`中描述的调试方法。

## `16.2 运行时错误`

程序执行中的不可预见情况

发生错误的区别在于，开发过程中发生的错误是程序设计时未预见的情况，而运行时的错误则是程序本身原则上能够运行，但在执行时发生了开发者未曾预料到的情况，也因此没有采取相应的预防措施。

这可能是一个例子：程序试图访问一个不存在的文件。这个问题在开发过程中或测试过程中从未发生过，因为程序要访问的文件早已存在。因此，开发者从未想到要为这种情况做出预防措施。一个类似的例子，在实践中非常常见，就是用户输入了程序无法处理的数据。例如，用户输入了一个文本，而程序期待的是一个数字。程序本来运行得很好，但现在它尝试用文本进行计算，导致崩溃。在测试时，程序员每次程序要求输入时都输入了数字。因此，他从未遇到过因为非数字输入导致程序崩溃的情况，也因此没有采取预防措施去测试用户输入，并在输入非数字时拒绝它。

仅在运行时发生的错误通常是由一种可能发生但在开发时未预见到的情况引起的。在理想条件下，程序可以顺利运行。

诀窍是在开发过程中尽可能捕获所有的错误来源。例如，程序应该测试用户输入的计算数据是否为数字，如果不是则拒绝该输入。同样，它还应该检查用作除数的数字变量是否为`0`，因为除以零当然会立即引发错误。程序想要访问的文件是否存在也可以进行检查，如果文件不存在，则调整程序流程。

对可能的错误进行预判是费时的，但却很重要，尤其是在为他人编写程序时。用户可能无法查看程序代码，或者缺乏技术理解，对错误的容忍度较低，特别是当他们为该程序付费时。

使用`Try-Catch`结构捕获错误

许多编程语言通过特殊的语言结构支持程序中的错误处理。基本的思想是，错误通过`异常`来反映。异常不过是当某种类型的错误发生时触发的事件。在这种情况下，程序员通常会说异常是“抛出的”。

按照“抛出”的类比，这些异常可以被“捕获”并处理。例如，在打开文件时，如果要读取的文件不存在，则可能会发生异常。在这种情况下，程序不会终止，而是继续执行程序的另一部分，这部分正是为这种情况而设计的。

在我们的伪代码中，这种结构看起来像这样：

`Try`// 打开文件并读取数据 `Catch`// 显示错误信息 `End`

所以，你`尝试`执行程序的某个部分；如果成功，程序继续执行`End`之后的部分。但如果发生异常，`Catch`关键字后的代码会首先执行。一些编程语言允许你在这样的结构中捕获不同的异常，并对每个异常作出不同的反应。通常，这涉及提供一个特殊的异常对象，其属性可以用来提供有关发生的异常的更多细节，以便你可以根据异常的情况调整你的响应。

那么，`Try-Catch`结构与一种不使用该结构的做法有什么不同呢？后者通过在尝试打开文件之前检查文件是否存在，来避免错误。在后一种做法中，错误的可能来源被提前检查，可能导致错误的操作根本不会执行。而使用`Try-Catch`结构时，在执行操作之前并没有进行检查，取而代之的是直接执行操作并遇到错误。唯一的区别是，错误不会导致程序崩溃或出现无法控制的行为。相反，错误会在发生后（即异常被抛出后）以完全受控的方式进行处理。这种方法的优势在于，你不需要提前知道具体会出什么问题。例如，虽然文件存在，但由于用户权限不足，文件仍然无法读取。这种错误也会通过我们的`Try-Catch`结构捕获，而不需要我们显式地考虑它。这种看似实用的方法的危险之处，当然在于它让人们减少了对潜在错误来源和最佳响应的思考。

因此，一个更好的方法是尽可能提前捕获所有潜在的问题和异常，单独处理它们，然后最后在程序中包括一个通用的`Try-Catch`结构，用于处理那些没有单独处理的异常。

## `16.3 测试`

鉴于可能出现的各种错误来源，`测试`当然是成功的关键。`测试`、`测试`和再次`测试`。`测试`几乎是一门独立的学科，存在许多不同的方法和测试类型。事实上，`测试员`在软件开发中甚至是一种职业描述。在一些公司，`开发人员`和`测试员`是配对工作的。考虑到`测试`的重要性，还有专门的工具来开发测试，有时甚至可以自动执行这些测试，记录结果，并为项目管理提供支持，以便消除错误。

当然，你不必费这么大的劲。然而，`测试`是很重要的。在框中，你会找到一些关于更好`测试`的建议。

提示

+   想想用户是如何使用你的程序的，并尝试这些`用例`。

+   想想所有可能出错的情况，也就是用户可能如何错误地使用程序。

+   将程序暴露于“极限”条件下。在开发过程中，你倾向于总是使用那些程序运行完美的简单示例，因为这自然是你所希望的：开发过程中少遇到问题。要反其道而行之，成为你自己程序的`魔鬼代言人`。

+   分段测试`并`在上下文中测试。单独测试代码片段（例如一个函数）可以使调试更容易，因为在出现错误时，你大致知道问题的原因所在。然而，有时在完全运行程序并让不同的代码片段交织时，也会发生无法预见的交互。因此，你应该始终采取两种方法，既进行分段测试，也进行完整程序上下文中的测试。

## `16.4 调试方法`

如果你注意到程序中有某些地方不工作，你就开始寻找错误。围绕查找和修复漏洞的活动称为`调试`。

这里基本上有两种方法；要么你使用“内建工具”，特别是程序流程中的合适辅助输出，要么你使用特殊工具，称为`调试器`。后者通常是编程语言集成开发环境的一部分，且便于使用。然而，也有命令行调试器。

基本上，调试涉及两个问题：

+   确定`错误发生的位置`

+   确定`错误发生的原因`。

并不总是能够先找到错误发生的位置，然后再回答为什么会出错。有时你首先意识到错误发生的原因，然后必须寻找导致错误的代码。为了回答这两个问题，基本上有以下工具可供使用：`输出`

你可以临时`添加额外输出`到程序中，等调试完成后再将其移除。这些输出可以帮助你了解程序的哪些部分已经执行。例如，如果你遇到程序崩溃的问题，而不知道程序到底停在了哪里，你可能想临时插入一些代码，产生额外的输出。每次这样的输出出现时，你就知道程序至少已经执行到了这一点，没有崩溃。有时也不太清楚某些条件（比如`if-then`结构）或循环是否完全执行。此时，包含一个相应的输出有助于确定位置，只有当`If-Then`结构或循环中的程序代码被执行时，这个输出才会触发。

然而，你不仅可以使用临时的额外输出来确定程序代码当前执行的部分，还可以检查程序流程中某些变量的值。理解变量的内容通常有助于诊断问题。

`断点`

如果你正在使用调试器，你可以设置`断点`。通过断点，当你启动程序时，它只会执行到这个断点为止。之后，你可以决定是否继续运行，或者在这个点终止程序。同样地，如果你追踪一个程序崩溃，并且程序能够运行到断点而没有崩溃，那么问题出现在断点之后。

单步模式

另一个在使用调试器时常见的选项是以单步模式执行程序。这意味着一次只执行一个程序指令。只有当你按下特定的键或键组合时，下一条程序语句才会被执行。IDE会在程序代码中图形化地显示最后执行的语句。这也使得你可以很容易地确定程序在哪一点停止。然而，如果你的程序中有频繁重复的循环，在单步模式下逐步执行这些循环会非常繁琐。在这种情况下，你应该在循环之后设置一个断点，让程序运行到那里，然后从那里开始继续单步执行。至少，如果错误不在循环本身，这样可以节省大量的按键操作。然而，如果问题出在循环内，你将不得不逐步执行循环，并检查循环中可能使用的任何变量的值。

变量观察与断点：结合断点或在单步模式下运行程序，还有一个许多调试器支持的功能，`变量观察`。这个功能允许你查看，甚至有时更改，变量的当前内容。所以，如果你的程序已经到达一个断点，你可以查看某些变量当前的值。在单步模式下，这使得你能够追踪变量的值如何从一个程序语句变化到下一个。◘ 图 [16.1](#Fig1) 显示了我们简单的摄氏-开尔文转换示例中的变量观察。一个断点已在程序的第60行设置。程序会执行到这一行。接下来要执行的指令是第60行的指令，即你设置断点的位置（该行前有一个红点标记）。 ![](../images/474412_1_En_16_Chapter/474412_1_En_16_Fig1_HTML.jpg)

`Delphi`中测试项目窗口的截图。它包含一组带有变量`Celsius`、`Kelvin`和`real`的程序代码，这些变量经过一个过程并最终结束。

图 16.1

`Delphi`中带有变量观察的断点示例

## 16.5 学习一门新编程语言的路线图

当你学习一门新的编程语言时……

你将会发现：

+   你可以使用的调试工具有哪些，以及如何访问它们（`命令行工具`，`IDE`中的集成），

+   是否，以及如果可以的话，如何设置和移除断点，

+   是否，以及如果可以的话，如何在单步模式下执行程序，

+   是否，以及如果可以的话，如何监控变量的内容。
