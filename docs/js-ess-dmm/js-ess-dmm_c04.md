第四章

# `控制JavaScript流程`

`在本章中`

![子弹](images/check.png) `设置代码以做决策`

![子弹](images/check.png) `理解代码循环`

![子弹](images/check.png) `设置代码循环`

在默认的脚本流程中，浏览器一次处理`script`元素或外部JavaScript文件中的代码。浏览器读取并执行第一条语句，然后读取并执行第二条语句，以此类推，直到没有更多JavaScript可供读取和执行。

这种逐条执行的流程似乎合理，但它的局限性极大。如果你希望代码测试某个条件，然后根据测试的结果跳转到特定代码块，该怎么办？如果你希望代码多次重复某些语句，并在每次重复中发生一些变化，该怎么办？进行测试的代码和重复执行的代码都属于控制JavaScript流程的范畴。在本章中，你将探索这一引人入胜且强大的主题。 ## `使用if语句进行决策`

一个智能脚本会对其环境进行测试，然后根据每个测试的结果决定接下来要做什么。例如，假设你已经声明了一个变量，稍后在表达式中用作除数。在使用该变量之前，你应该测试它以确保它的值不是`0`。

最基本的测试是简单的真/假决策（也可以被视为是是/否或开/关决策）。在这种情况下，你的程序查看某个条件，确定它当前是`true`还是`false`，并相应地采取行动。比较和逻辑表达式（在[第3章](c03.xhtml)中介绍）在这里发挥了重要作用，因为它们始终返回`true`或`false`的结果。

在JavaScript中，简单的真/假决策是通过`if`语句处理的。你可以使用`single-line`语法：

`if (expression) statement;`

或者`block`语法：

`if (expression) { statement1; statement2; … }`

在这两种情况下，`expression`是一个返回`true`或`false`的比较或逻辑表达式，而`statement(s)`表示如果`expression`返回`true`要执行的JavaScript语句或语句。如果`expression`返回`false`，JavaScript会跳过这些语句。

![提示](images/tip.png) 这里是一个很好的地方，可以指出JavaScript将以下值视为`false`的等价物：`0`，`""`（即空字符串），`null`和`undefined`。其他所有值都被视为`true`。

![记住](images/remember.png) 这是您第一次遇到JavaScript的花括号（`{`和`}`），请花一点时间理解它们的作用，因为它们经常出现。花括号包围您希望JavaScript视为单个实体的一条或多条语句。这个实体本身是一种语句，因此整个组合——花括号和它们包含的代码——称为`*块语句*`。此外，任何由语句（例如`if`）后跟块语句组成的JavaScript结构称为`*复合语句*`。并且，为了让您保持警惕，请注意包含花括号的行不以分号结束。

您使用单行或块语法取决于当`*expression*`返回`true`结果时要运行的语句。如果您只有一个语句，可以使用任一语法。如果您有多个语句，则使用块语法。

考虑以下示例：

``if (totalSales != 0) { const grossMargin = (totalSales - totalExpenses) / totalSales; }``

这段代码假设之前脚本已计算总销售额和总支出，这些值分别存储在`totalSales`和`totalExpenses`变量中。代码现在计算毛利率，定义为毛利（即销售额减去支出）除以销售额。代码使用`if`来测试`totalSales`变量的值是否不等于零。如果`totalSales != 0`表达式返回`true`，则执行`grossMargin`计算；否则，什么都不发生。此示例中的`if`测试是合理的，因为它确保计算中的除数——`totalSales`——永远不为零。## 使用if…else语句分支

使用`if`语句进行决策为您的JavaScript工具箱增添了一种强大的新武器。然而，`if`的简单版本存在一个重要限制：`false`结果仅跳过一个或多个语句；它不会执行自己的任何内容。在许多情况下，这很好，但有时您需要在条件返回`true`时运行一组语句，而在结果为`false`时运行另一组语句。要处理这些情况，您需要使用`if…else`语句：

``if (*expression*) { *statements-if-true* } else { *statements-if-false* }``

`*expression*`是一个比较或逻辑表达式，返回`true`或`false`。`*statements-if-true*`表示当`*expression*`返回`true`时，您希望JavaScript运行的语句块，`*statements-if-false*`表示当`*expression*`返回`false`时，您希望执行的语句块。

作为示例，考虑以下代码：

``let discountRate; if (currMonth === "December") { discountRate = 0.2; } else { discountRate = 0.1; } const discountedPrice = regularPrice * (1 – discountRate);``

这段代码计算了一个商品的折扣价，折扣取决于当前月份是否为十二月。代码假设之前脚本已经设置了当前月份（`currMonth`）和商品的原价（`regularPrice`）。在声明了`discountRate`变量后，`if…else`语句会检查`currMonth`是否等于十二月。如果是，`discountRate`被设置为`0.2`；否则，`discountRate`被设置为`0.1`。最后，代码使用`discountRate`的值来计算`discountedPrice`。

![提示](images/tip.png)`if…else`语句在每个代码块内缩进后会更容易阅读，就像我在示例中所做的那样。这种缩进让你可以轻松识别在结果为`true`时哪个块会执行，结果为`false`时哪个块会执行。我发现四个空格的缩进足够，但许多程序员更喜欢使用两个空格或制表符。## 理解代码循环的价值

有些人可能会说，程序员唯一真正的目标应该是完成任务。只要代码能够产生正确的结果，或者按照正确的顺序执行正确的任务，其他一切都显得多余。或许是这样，但`真正的`程序员知道，编程的真正目标不仅仅是完成任务，更是以`尽可能高效`的方式完成任务。高效的脚本运行更快，编码时间更少，而且通常（不是总是，但通常）更容易阅读和排错。

引入编程效率的最佳方式之一是避免重复发明轮子。例如，考虑以下代码片段：

`let sum = 0; let num = prompt("输入一个数字:", 1); sum += Number(num); num = prompt("输入一个数字:", 1); sum += Number(num); num = prompt("输入一个数字:", 1); sum += Number(num); document.write("你输入的数字总和是 " + sum);`

这段代码首先声明了一个名为`sum`的变量。代码通过`prompt`方法提示用户输入一个数字（默认值为`1`），将输入的值存储在`num`变量中，然后将该值加到`sum`上，接着重复两次此提示和加法操作。（注意我使用了`Number`函数，这可以确保`prompt`返回的值被当作数字处理，而不是字符串。）最后，三次输入的数字总和会显示给用户。

除了稍显无用外，这段代码还充满了低效，因为大多数代码都由以下两行重复出现三次：

`num = prompt("输入一个数字:", 1); sum += Number(num);`

如果你只在代码中写一次这两条语句，然后用某种方式让JavaScript根据需要重复这些语句，不会更高效吗？

是的，完全可以，值得庆幸的是，不仅可以这样做，而且JavaScript还提供了多种方法来执行这种所谓的`looping`。我将在本章余下的部分探讨这些方法。 ## 使用`while`循环

JavaScript循环结构中最简单的就是`while`循环，它使用以下语法：

`while (expression) { statements }`

在这里，`expression`是一个比较或逻辑表达式（即返回`true`或`false`的表达式），只要它返回`true`，就会告诉JavaScript继续执行块中的`statements`。

从本质上讲，JavaScript对`while`循环的解释是这样的：“好吧，只要`expression`保持为`true`，我就会继续执行循环语句，但一旦`expression`变为`false`，我就退出循环。”

下面是`while`循环如何工作的详细说明：

1.  评估`while`语句中的`expression`。

1.  如果`expression`为`true`，继续执行第3步；如果`expression`为`false`，跳到第5步。

1.  执行块中的每一条语句。

1.  返回第1步。

1.  退出循环（即执行`while`块之后的下一条语句）。

以下代码演示了如何使用`while`重写上一节中显示的低效代码：

`let sum = 0; let counter = 1; let num; while (counter <= 3) { num = prompt("请输入一个数字：", 1); sum += Number(num); counter += 1; } document.write("你输入的数字总和为 " + sum);`

为了控制循环，代码声明了一个名为`counter`的变量并将其初始化为`1`，这意味着`counter <= 3`的表达式为`true`，因此代码进入块，执行提示和求和操作，然后递增`counter`。这个过程会重复，直到第三次循环时，`counter`被递增为`4`，此时`counter <= 3`的表达式变为`false`，循环结束。

![提示](images/tip.png) 为了让你的循环代码尽可能易读，始终对`while`块中的每个语句使用两个或四个空格的缩进。对于本章后面我提到的`for`和`do…while`循环也是如此。

当你确切知道想要循环的次数时，`while`语句不是最好的选择。对于这种情况，应该使用接下来会介绍的`for`语句。`while`语句最好的用法是在你的脚本中有一些自然出现的条件，可以将其转化为比较表达式。一个很好的例子是当你要求用户输入值时。你通常希望不断提示用户，直到他们点击取消按钮。设置这种情况最简单的方法是将提示语句包含在一个`while`循环中，代码如下：

`let sum = 0; let num = prompt("请输入一个数字或点击取消：", 1); while (num != null) { sum += Number(num); num = prompt("请输入一个数字或点击取消：", 1); } document.write("你输入的数字总和为 " + sum);`

第一个`` `prompt` ``方法会显示一个对话框，如[图4-1](#c04-fig-0001)所示，用于获取初始值；然后将其存储在`` `num` ``变量中。

![Paulmcfederies网页快照。消息框显示，输入一个数字或点击取消。下面提供了取消和确定选项。](images/9781394263219-fg0401.png)

[图4-1：](#rc04-fig-0001) 设置你的`` `while` ``表达式，使得当用户点击取消按钮时，提示停止。

然后，`` `while` ``语句检查以下表达式：

`` `num != null` ``

这里可能发生两件事：

+   如果用户输入了一个数字，表达式将返回`` `true` ``，循环继续。在这种情况下，`` `num` ``的值会加到`` `sum` ``变量中，系统会提示用户输入下一个数字。

+   如果用户点击取消，`` `prompt` ``返回的值是`` `null` ``，因此表达式变为`` `false` ``，循环停止。## 使用for循环

尽管`` `while` ``是最直接的JavaScript循环，但迄今为止最常见的类型仍然是`` `for` ``循环。当你考虑到（如你将要看到的）`` `for` ``循环的语法比`` `while` ``循环稍微复杂时，这个事实有点令人惊讶。然而，`` `for` ``循环在一件事上表现出色：当你确切知道要重复多少次某一组语句时，循环效果最好。这在所有类型的编程中都非常常见，因此`` `for` ``在脚本中如此常用也就不足为奇了。

一个典型的`` `for` ``循环的结构如下所示：

`` `for (let `*counter*` = `*start*`; `*counterExpression*`; `*counterUpdate*`) { `*statements*` }` ``

这里有很多内容，我将一一讲解：

+   `` `counter` ``：一个数字变量，用作`` *循环计数器* ``。循环计数器是一个数值，用于计算过程已经通过循环的次数。（请注意，只有在这是第一次在脚本中使用该变量时，才需要使用`` `let` ``。）

+   `` `start` ``：`` `counter` ``的初始值。这个值通常是1，但你可以根据脚本的需要使用任何合适的值。

+   `` `counterExpression` ``：一个比较或逻辑表达式，用于确定循环的执行次数。这个表达式通常将`` `counter` ``的当前值与某个最大值进行比较。

+   `` `counterUpdate` ``：一个改变`` `counter` ``值的表达式。这个表达式会在每次循环之后被评估。大多数情况下，你会使用`` `counter` `` `` += 1 `` 来递增计数器的值。

+   `` `statements` ``：你希望JavaScript在每次循环中执行的语句。

当JavaScript遇到`` `for` ``语句时，它会穿上for循环的“衣服”，并按照以下七个步骤执行：

1.  将`` `counter` ``设置为`` `start` ``。

1.  在`` `for` ``语句中评估`` `counterExpression` ``。

1.  如果`` `counterExpression` ``为`` `true` ``，继续执行步骤4；如果`` `counterExpression` ``为`` `false` ``，跳过到步骤7。

1.  执行块中的每条语句。

1.  使用`` `counterUpdate` ``来递增（或其他操作）`` `counter` ``。

1.  返回到步骤2。

1.  退出循环（即，执行`for`块之后发生的下一条语句）。

作为示例，下面的代码显示如何使用`for`来重写本章早些时候显示的低效代码：

`let sum = 0; let num; for (let counter = 1; counter <= 3; counter += 1) { num = prompt("输入一个数字:", 1); sum += Number(num); } document.write("你数字的总和是 " + sum);`

这是迄今为止最有效的版本，因为`counter`变量的声明、初始化和增量都在`for`语句中完成。

![记住](images/remember.png) 为了尽量减少脚本中声明的变量数量，始终尝试在所有`for`循环计数器中使用相同的名称。字母`i`到`n`通常用于编程中的计数器。为了更清晰，你可能更喜欢使用完整的单词，如`count`或`counter`。

这是一个稍微复杂的示例：

`let sum = 0; for (let counter = 1; counter < 4; counter += 1) { let num; let ordinal; switch (counter) { case 1: ordinal = "first"; break; case 2: ordinal = "second"; break; case 3: ordinal = "third"; } num = prompt("请输入第" + ordinal + "个数字:", 1); sum += Number(num); } document.write("平均值是 " + sum / 3);`

本脚本的目的是询问用户三个数字，然后显示这些值的平均值。`for`语句设置为循环三次。（注意`counter < 4`与`counter <= 3`是相同的。）循环块首先使用`switch`来确定`ordinal`变量的值：如果`counter`为1，则`ordinal`被设置为`"first"`；如果`counter`为2，则`ordinal`变为`"second"`；以此类推。这些值使脚本能够在每次循环中自定义`prompt`消息（查看[图4-2](#c04-fig-0002)）。在每次循环中，用户输入一个数字，该值被添加到`sum`变量中。当循环退出时，平均值被显示。

![paulmcfederies网页的快照。消息框显示，输入第一个数字。下面提供取消和确认选项。](images/9781394263219-fg0402.png)

[图4-2:](#rc04-fig-0002) 此脚本使用当前的`counter`变量值来自定义提示消息。

也可以使用`for`进行倒计数。你可以通过使用减法赋值运算符而不是加法赋值运算符来实现：

`for (let *counter = start*; *counterExpression*; *counter -= 1*) { *statements* }`

在这种情况下，必须将`counter`变量初始化为你想要用于循环计数器的最大值，并使用`counterExpression`将`counter`的值与要用来结束循环的最小值进行比较。

在以下示例中，我使用递减计数器询问用户按逆序对他们的前三种CSS颜色进行排名：

``for (let rank = 3; rank >= 1; rank -= 1) { let ordinal; let color; switch (rank) { case 1: ordinal = "first"; break; case 2: ordinal = "second"; break; case 3: ordinal = "third"; } color = prompt("你的第" + ordinal + "最喜欢的CSS颜色是什么?", ""); document.write(rank + ". " + color + "<br>"); }``

`for`循环通过将`rank`变量从`3`递减到`1`来运行。每次循环都会提示用户输入一个最喜欢的CSS颜色，并将该颜色写到页面上，当前的`rank`值被用于创建一个逆序排列的列表，如[图4-3](#c04-fig-0003)所示。

![paulmcfederies网页的快照。逆序排列的列表是，3. 木瓜奶油色，2. 柠檬雪纺色，1. 巧克力色。](images/9781394263219-fg0403.png)

[图4-3:](#rc04-fig-0003) `rank`变量的递减值用于创建一个逆序列表。

![Tip](images/tip.png) 没有理由要求`for`循环的计数器只能递增或递减。你实际上可以使用任何表达式来调整循环计数器的值。例如，假设你希望循环计数器只遍历奇数`1`、`3`、`5`、`7`和`9`，这里有一个`for`语句可以做到这一点：

``for (let counter = 1; counter <= 9; counter += 2)``

表达式`counter += 2`使用加法赋值运算符，告诉JavaScript每次循环时将`counter`变量增加`2`。  

JavaScript有第三种也是最后一种循环类型，我将其留到最后讨论，因为它并不是你会经常使用的。为了理解何时使用它，考虑以下代码片段：

``let sum = 0; let num = prompt("请输入一个数字或点击取消:", 1); while (num != null) { sum += Number(num); num = prompt("请输入一个数字或点击取消:", 1); }``

这段代码需要第一个`prompt`语句，以便可以评估`while`循环的表达式。用户可能不想输入*任何*数字，可以通过点击第一个提示框中的取消按钮来避免输入，从而绕过循环。

这看起来合情合理，但如果你的代码要求用户至少输入一个值呢？以下展示了一种方法来修改代码，确保循环至少执行一次：

``let sum = 0; let num = 0; while (num !== null || sum === 0) { num = prompt("输入一个数字；完成后点击取消:", 1); sum += Number(num); } document.write("你的数字总和是 " + sum);``

这里的变化是代码将`sum`和`num`都初始化为`0`。将两者初始化为`0`确保`while`表达式 — `num !== null || sum === 0` — 在第一次循环时返回`true`，因此循环至少会执行一次。如果用户立即点击取消，`sum`仍然是`0`，所以`while`表达式 — `num !== null || sum === 0` — 仍然返回`true`，循环会再次执行一次。

这种方法效果很好，但你也可以转向JavaScript的第三种循环类型，它专门处理这种情况。它被称为`do…while`循环，它的一般语法看起来像这样：

```do { statements } while (expression);```

在这里，`statements`代表每次循环执行的语句块，而`expression`是一个比较或逻辑表达式，只要它返回`true`，就告诉JavaScript继续执行循环中的`statements`。

这种结构确保JavaScript至少执行一次循环语句块。为什么？仔细看看JavaScript如何处理`do…while`循环：

1.  执行语句块中的每一个语句。

1.  在`while`语句中评估`expression`。

1.  如果`expression`为`true`，返回到步骤1；如果`expression`为`false`，继续执行步骤4。

1.  退出循环。

例如，下面展示了如何使用`do…while`来重构我之前展示的提示和求和代码：

```let sum = 0; let num; do { num = prompt("输入一个数字；完成后点击取消:", 1); sum += Number(num); } while (num !== null || sum === 0); document.write("你的数字总和是 " + sum);```

这段代码与我在本节之前展示的`while`代码非常相似。真正改变的只是`while`语句及其表达式被移到了语句块之后，因此循环必须在评估表达式之前至少执行一次。
