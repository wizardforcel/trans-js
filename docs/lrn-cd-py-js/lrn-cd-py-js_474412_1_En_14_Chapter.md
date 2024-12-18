© 作者（们），独家许可Springer Fachmedien Wiesbaden GmbH，Springer Nature旗下出版，2024年 J. L. Zuckarelli 用Python和JavaScript学习编程 [`https://doi.org/10.1007/978-3-658-42912-6_14`](https://doi.org/10.1007/978-3-658-42912-6_14)

# 14. `如何控制程序流并使程序对用户行为和其他事件作出反应？`

Joachim L. Zuckarelli^([1](#Aff2) )(1) 慕尼黑，德国 概述

程序必须能够灵活地对新情况作出反应，例如当用户输入内容或点击按钮时。根据用户的输入或点击的按钮，程序会执行不同的指令。实际上，程序会分支到不同的路径。这种流程控制方式使得程序具有动态性。

本章将学习以下内容：

+   如何根据条件分支到程序的不同部分

+   如何制定这样的条件，并检查它们是否被满足

+   如何制定由多个子条件组成的复杂条件

+   有哪些方法可以简单明了地测试一系列结构相似的条件

+   如何在无法预知事件何时会在程序流中被触发的情况下（例如点击按钮时）对事件作出反应

## 14.1 为什么需要程序流程控制

在前面的章节中，你已经了解了如何接收用户数据、处理数据并输出处理结果。然而，如果仅用工具箱中的那些工具来编写程序，程序的可能性将非常有限，从而降低其实用性，因为程序流程将完全僵化。它将`*总是*`从一个输入开始，然后`*总是*`按照`*完全相同的方式*`进行处理，最后其结果`*总是*`以`*相同的形式*`返回给用户。实际上，我们很难接受这种僵化的程序。想象一下，你在汽车的导航系统中输入一个新的目的地。导航系统会计算出到该目的地的最佳路线，但一旦你不小心偏离了这条路线，导航系统却依然坚持原来的路线，即使你已经不在那条路上了。你需要的是帮助，以便返回原来的路线，或者从当前位置开始找到一条全新的路线。如果你设置了导航系统避开收费公路，但系统完全忽略了这一指令，直接把你引导到第一条收费高速公路上，那么导航系统的行为就显得很奇怪。你完全可以认为这是导航系统的故障。

所以，我们需要的是一个能对事件作出反应（`“驾驶员离开建议路线”`）并考虑条件（`“驾驶员希望避开收费公路”`）的程序。

在这两种情况下，程序的某些部分仅在相应事件发生或条件得到满足时才会执行。程序根据当前情况及其他相关情况`branches`到代码的不同部分。本章将讨论这种类型的程序`flow control`。

## 14.2 流控制的形式

在实践中，程序的流控制通常通过使用`If-(then-)Else构造`来实现：`if`某个条件满足，`then`执行某个操作，`otherwise`执行其他操作。

被检查的条件也可以是`复杂条件`，由几个子条件组成。在我们的导航系统示例中，这样的复杂条件可能是：“如果‘避免收费公路’被设置为`true`，并且下一个转弯通往收费公路，则在任何情况下都不推荐走这个转弯。”另一个例子是：“如果下一个出口不是收费公路`OR`允许驶入收费公路，则推荐下一个出口。”在这里，两个部分条件通过`AND`或`OR`连接，这两者都是逻辑运算符。

有时你需要检查一系列相似的条件，例如，如果用户输入一个数字，每个数字会引发不同的反应。条件在结构上总是相同的，即“输入等于数字`X`”，而当满足某个特定条件时执行的程序代码可能因输入的数字而大相径庭。此类条件的使用案例可以通过`If-Else`构造来实现，但这通常会导致复杂的代码，难以阅读（因此也难以维护）。因此，许多编程语言知道`Switch-Case构造`，可以用来以非常简单明了的方式实现对相似条件的检查。

程序流并不总是线性的，因此在经过一系列明确定义的指令后，你到达一个检查条件的点，然后根据检查结果分支到程序的一个或另一个部分。非线性程序流的最重要原因是用户。例如，在图形用户界面上，用户可以从多个不同的程序功能中选择，并可以相对自由地决定在何时使用哪个功能以及以何种顺序使用。这意味着用户决定了程序的流，而程序不能仅仅是对一长串指令的顽固处理，而必须以某种方式更灵活地结构化。这种流控制引导我们到`events`的概念和在许多编程语言中使用的事件驱动编程范式。

我们在本章其余部分将处理这些流控制元素，包括`If-Else`构造、用于它们的条件、多个子条件链接成更复杂的整体条件、`Switch-Case构造`和事件控制。

## 14.3 `If-Else构造`

想象一下，我们正在为在线银行软件工作，即运行银行在线银行网站的程序。在这里，我们处理一个账户余额查询。如果用户的账户透支了，即账户余额为负数，用户应该收到警告。

一个仅仅执行此操作的程序可能如下所示：

`balance = query_balance()` **如果** `balance < 0` **则** `show("警告：您的账户余额为负！")` `show("当前余额：$", balance)`

这里我们首先将**`query_balance()`**函数的值赋给一个变量**`balance`**。我们假设这个函数返回当前账户余额的十进制数值。在将账户余额保存到变量后，我们使用**`If balance < 0`**检查账户余额是否为负。如果是，警告信息将被显示，我们通过**`show()`**函数实现。然后，使用**`show("当前余额：$", balance)`**输出账户余额本身，即变量**`balance`**的内容。请注意，无论账户是否透支，这条语句总是会执行。只有在账户余额为负时，跟在**`then`**关键字后的警告信息才会显示。之后的所有语句都会在任何情况下执行。

假设账户余额为`$1000`，在这种情况下，我们程序的输出将是：

当前余额：`$1000`

然而，如果账户透支了，例如余额为`-$280`，用户将收到以下输出：

`警告：您的账户余额为负！` 当前余额：`$-280`

在这个简单的例子中，你可以非常清楚地看到程序如何分支并执行某些部分——在我们的例子中，只有满足某个条件时，才会执行警告。

在下一步中，我们扩展程序，使其还显示透支额度剩余多少，假设如果账户透支，则透支额度为`$500`。如果账户余额大于`0`，即账户有盈余，则不显示任何关于透支额度的消息。我们程序的扩展可以是这样的：

`balance = query_balance()` **如果** `balance < 0` **那么** **开始** `show("注意：您的账户余额为负数！")` `overdraftrest = 500 + balance` `show("您还剩余 $", overdraftrest, " 的透支额度。")` **结束** `show("当前余额：$", balance)`

为了映射透支余额，我们创建了一个名为**`overdraftrest`**的变量，并将`$500`与**`balance`**的总和赋值给它。如果账户余额为负（只有在这种情况下程序的这一部分才会执行），则总和就是透支额度中剩余的金额。

与前面的例子不同，在这里检查账户是否透支的代码后面跟着`多个`语句，这些语句被包含在一个代码块中，位于`开始`和`结束`关键字之间。我们已经在►第[13.1节](474412_1_En_13_Chapter.xhtml#Sec1)中学习过关于函数的代码块。代码块中的所有语句只有在条件`balance < 0`满足时才会执行。语句`show("当前余额：$", balance)`，用于输出当前账户余额，它不属于代码块，因此无论账户是透支还是有盈余，都会始终执行。在许多编程语言中，如果代码块只有一行，`开始`和`结束`的分隔符（在我们的伪代码中）也可以省略，就像我们在上面的例子中做的那样。

让我们再来看一下账户余额为`-$280`的例子。在这种情况下，我们的程序现在会产生以下输出：

`注意：您的账户余额为负数！` `您还剩余 $220 的透支额度。` `当前余额：$-280`

在账户余额为`1000`的情况下，输出会相应地减少：

`当前余额：$1000`

现在假设我们还想在账户余额为正（或等于`0`）时显示一些内容，例如 `您的账户有盈余。`

这一点可以很容易地通过我们到目前为止学到的方法来实现：

`balance = query_balance()` `如果` `balance < 0` `那么` `开始` `show("注意：您的账户余额为负数！")` `overdraftrest = 500 + balance` `show("您还剩余 $", overdraftrest, " 的透支额度。")` **结束** `如果` `balance >= 0` `那么` `开始` `show("您的账户有盈余。")` **结束** `show("当前余额：$", balance)`

然而，如果我们考虑到条件`balance < 0`和`balance >= 0`互为反向，即两者共同覆盖了所有可能的情况，这可以更容易地实现。在这种情况下，我们可以不明确地写出第二个条件：

`balance = query_balance()` `If` `balance < 0` `Then` `Begin` `show("Attention: Your account balance is negative!")` `overdraftrest = 500 + balance` `show("You still have $", overdraftrest, " left of your overdraft facility.")` `End` `Else` `Begin` `show("Your account is in credit.")` `End` `show("Current balance: $", balance)`

在这里，关键字`Else`告诉我们，代码块现在开始执行，只有当上面的条件（`balance < 0`）不满足时才会执行，也就是说，如果账户余额大于或等于0。我们因此有两个代码块：一个在`If account < 0 Then`和`End`之间，另一个在`Else`和`End`之间。每次程序执行时，只有*一个*代码块会被运行。所以，程序在这一点上进行分支。如果条件`If balance < 0`被满足，程序首先继续，显示警告信息，计算透支余额并显示它。然后它遇到`Else`。由于第一个条件已经满足，`Else`代码块会被跳过，程序继续执行`Else`代码块后的下一条语句，在我们的例子中是`show("Current balance: $", balance)`。

If-Else结构的流程示意图如图◘ `[14.1](#Fig1)`所示。![](../images/474412_1_En_14_Chapter/474412_1_En_14_Fig1_HTML.jpg)

一个If-Else结构的示意图。输入提供给条件，条件被分类为未满足或已满足。接下来是`else`和`if`代码块。

图 14.1

If-Else结构的流程图

大多数编程语言都有这种If-Else结构。这些结构的形式通常非常相似。为了说明这一点，我们来看一下如何在三种不同的编程语言中解决上面的问题。

首先是C/C++：

`if`(balance < 0){`printf`("Attention: Your account balance is negative!");`float` overdraftrest = 500 + balance;`printf`("You still have $%f left of your overdraft facility.", overdraftrest);} `else`{`printf`("Your account is in credit.");}`printf`("Current balance: $%f", balance);

接下来是Python示例：

`if` balance < 0:`print`("Attention: Your account balance is negative!")overdraftrest = 500 + balance`print`("You still have ", overdraftrest, " left of your overdraft facility.") `else`:`print`("Your account is in credit.")`print`("Current balance: $", balance);

最后是`Visual Basic for Applications (VBA)`：

`If` balance < 0 `Then` `MsgBox` ("Attention: Your account balance is negative!")overdraftrest = 500 + balance`MsgBox` ("You still have " & overdraftrest & " left of your overdraft facility.") `Else` `MsgBox` ("Your account is in credit.") `End If` `MsgBox` ("Current balance: $" & balance) 如果比较这三个例子，你会首先注意到它们的基本结构相似。所有三种语言都有If-Else结构。实现的区别仅在于细节：

+   `关键词`：在所有三种语言中，`if`和`else`关键字都存在。然而，只有在`VBA`中才会显式地写出`then`。

+   `条件`：C/C++ 要求条件写在括号内，而另外两种语言则不需要。然而，括号并不会造成任何问题；我们将在下面学习为什么。

+   `代码块`：在代码块的划分上存在显著的差异。代码块是当条件满足时（`if-case`）或不满足时（`else-case`）执行的部分：在 `C/C++` 中，使用大括号来标记代码块的开始`和`结束。而在 `Python` 中，代码块以冒号开始，并通过缩进表示。所有处于同一缩进级别的语句都视为该代码块的一部分。因此，在 `else` 块结束时，不再需要特殊的关键字。在这里，你必须特别注意代码的格式化；缩进有着重要的意义，因此不能随意缩进。在 `VBA` 示例中，`Then` 和 `Else` 之间、`Else` 和 `End If` 之间都有代码块。注意，这里与前面提到的 `End` 不同，`End If` 并不标志着 `If` 块的结束，即条件 `balance < 0` 满足时执行的代码部分。它标志着整个 `If-Else` 结构的结束。`if-block` 仅在 `Else` 处结束。只有在没有 `Else` 分支时，`End If` 才标志着 `If` 块的结束。14.1 [3 min] 以下伪代码在 `a. x = 10` `b. x = 11` `c. x = 25` `d. x = -1` 时会发生什么？

被输入时会发生什么？

`x = enter("请输入一个数字：")` `If` `x > 10` `Then` `Begin` `If` `x > 20` `Then` `show("Result A")` `show("Result B")` `End` `Else` `Begin` `If` `x > 0` `Then` `show("Result B")` `End` 14.2 [3 min]

修改程序部分，从► 练习 [14.1](#FPar8) 开始，只有当 `x` 大于 10 且小于等于 20 时，才显示 `Result B`。

## 14.4 更深入地了解条件

在上一节中，你已经看到 `If-Else` 结构如何根据特定条件是否满足，决定程序的不同分支。接下来，我们将更深入地探讨在 `If-Else` 结构中检查的条件。

所有条件的一个重要共同特征是它们的结果要么是`true`，要么是`false`，条件是否满足。任何可以评估为真或假的逻辑表达式都适合用作条件。这样的逻辑表达式通常是值比较，就像我们在上一节的网上银行示例中看到的那样。例如，我们检查了账户余额是否小于`0`。这种值比较可以通过使用数学中常见的比较运算符来轻松表达，比如`>`（大于）、`<`（小于）和`=`（等于）。这里，`>=`通常表示“大于或等于”，`<=`表示“小于或等于”，因为在早期计算机时代，字符集并没有包括特殊字符`≤`和`≥`，即便现在理论上可以使用，但直接从键盘输入它们仍然不方便。因此，为了方便快速编写程序，大家约定使用这种复合符号。至于“不等于”符号`≠`，则特别具有挑战性，因为它没有直接对应的复合字符。事实上，不同的编程语言对这一点有不同的解决方法。最常见的两种是`<>`（大于小于）和`!=`（叹号和等号）。

在上一节中，条件总是由比较变量和一个值组成。实际上，任何可以为真或假的表达式都可以作为条件。假设我们在网上银行的示例中有一个函数，用来检查当前客户的账户余额是否为正。该函数的返回值可以存储在一个变量中：

`accountcredit = is_balance_positive()`

所以我们将函数`is_balance_positive()`的返回值赋给变量`accountcredit`。因此，`accountcredit`变量的值现在是`TRUE`或`FALSE`。我们可以在条件中检查该变量的内容：

`If accountcredit = TRUE Then Begin show("您的账户有余额！") End`

大多数编程语言允许你直接在条件中插入函数，而不是检查变量`accountcredit`：

`If is_balance_positive() = TRUE Then Begin show("您的账户有余额！") End`

如果你不想继续使用函数的返回值，这个过程始终很有用。然而，如果你希望在其他地方再次访问该值，将其存储在变量中以便进一步使用是很有意义的。这可以避免重复调用函数，从而节省计算能力和时间：如果函数背后的程序代码非常复杂，那么如果你直接使用存储在变量中的值，而不是通过函数调用重新计算，程序的运行速度会更快。

大多数编程语言允许的另一个简化是直接省略与逻辑值`TRUE`的显式比较。因此，假设在条件中使用一个值（无论是变量的值、函数的返回值，还是以任何方式计算得到的表达式结果），而没有显式地与另一个值进行比较时，应该默认与逻辑值`TRUE`进行比较。在我们的示例中，我们可以写成：

`If` `is_balance_positive()` `Then` `Begin` `show("您的账户有余额！")` `End`

如果你给函数起了一个有意义的名字，就像我们在这里做的那样，条件就非常容易阅读和理解。

如你所见，即使是普通的值比较，最终也是与值`TRUE`的比较，从而根据常规的检查方案进行条件判断。

比如说，代替

`If` `balance > 1000000` `Then`

你也可以这样写：

`If` (`balance > 1000000`) = `TRUE` `Then`

然后左边的表达式会首先被评估。如果账户余额现在大于一百万，那么该表达式将返回`TRUE`，条件将成立。因此，条件最终总是与值`TRUE`进行比较。

## `14.5 逻辑运算符的复杂条件（AND，OR，NOT）`

在前面部分的示例中，总是一个简单的基本条件决定了程序部分是否执行。当然，if-then块中的条件也可以是由多个子条件组成的条件。

假设，在我们的在线银行示例中，我们只想在账户没有被锁定`并且`账户余额（可能为负值）加上透支额度至少和待转账金额相等时，才允许转账。例如，如果账户余额为`$–150`，透支额度为`$500`，且我们的在线银行用户希望转账`$50`，那么在线银行应该允许此交易，因为账户余额和透支额度的总和，即在线银行客户可用的金额，应该为`$350`，即高于实际转账金额。如果，另一方面，客户希望转账`$400`，我们的在线银行应用应该拒绝这个交易请求，因为待转账金额将比账户余额和透支额度的可用总和多出`$50`。

为了简化，我们假设我们有一个`is_account_locked()`函数，如果账户被锁定则返回`TRUE`，否则返回`FALSE`。那么在if-then块中检查客户是否允许转账`amount`金额的条件如下所示：

`If` `is_account_locked()` = `FALSE` `AND` `balance + overdraftrest >= amount` `Then` `Begin` `…` `End`

这里你可以看到，我们用逻辑**AND**将两个（部分）条件连接起来。因此，if-then语句的总条件只有在*两个*部分条件都满足时才会成立。

除了`AND`，还有其他逻辑运算符可以用来组合更复杂的条件。例如，逻辑`OR`，它将两个（部分）条件以一种方式链接，使得总条件只有在一个、另一个或两个部分条件都满足时才会成立。因此，逻辑`OR`的意义不同于日常语言中的“或”，在日常语言中通常是指*排他性的*`OR`：*要么*一个*要么*另一个，但不能同时满足。

正如你可以很容易看到的，逻辑运算符的工作方式就像你在数学中熟悉的那样。因此，编程语言中也有一个排他性的`OR`（通常叫做`XOR`），它对应日常语言中的“或”。

另一个重要的逻辑运算符是逻辑`NOT`，它会反转语句的逻辑真值内容。“账户被锁定”这一语句的真值内容的反面显然是“账户没有被锁定”。然而，在编程中，我们通常无法像在自然语言中那样优雅地把`NOT`放在“句子”的“单词”之间。因此，在程序代码中，它通常会变成“`NOT` 账户被锁定”。因此，除了上面的条件，我们还可以写成：

**如果 NOT** `is_account_locked` **并且** `balance + overdraftrest >= amount` **那么** **开始**… **结束**

如你在前一部分中回忆到的，`is_account_locked()`是`is_account_locked() = TRUE`的简写，因此，如果你想检查值为**TRUE**，你可以简单地省略对该值的显式比较，因为默认情况下，如果你没有指定其他比较值，系统会检查这个值。

这样设计的条件首先确定了函数`is_account_locked()`的值。借助`NOT`运算符，这个真值就会被反转。所以，如果账户没有被锁定，`is_account_locked()`返回**FALSE**，逻辑`NOT`会将这个值反转为**TRUE**。因此，条件可以简化为**如果 TRUE 并且 `balance + overdraft >= amount`**。总条件的真值然后取决于第二个子条件是否成立。

当然，像上面这样的逻辑表达式也可以嵌套括号，复杂度可以任意增加。括号确保括号中的内容首先被求值，然后这个计算结果再与其他表达式逻辑连接。

这是一个简单的例子：

**如果 NOT** `is_account_locked()` **并且** (`balance + overdraftrest >= amount` 或 `is_customerhistory_positive()`) **那么** **开始**… **结束**

第二个子条件判断待转账金额是否符合常规要求，或客户是否有良好的历史记录（例如，账户上有定期存款、没有重大透支等），这一点通过函数`is_customerhistory_positive()`来判断。因此，如果客户迄今为止表现良好，即使转账金额超出了透支限额，交易也会被允许。括号确保首先判断是基于足够小的转账金额还是基于客户的历史行为来决定是否允许交易。为此，两个子条件通过逻辑`OR`连接。结果是一个逻辑值，然后在第二步中，和检查客户账户是否被锁定的逻辑值通过逻辑`AND`连接。

如你所料，逻辑运算符在不同的编程语言中有不同的名称。通常，它们保持使用英语关键字**AND**、**OR**、**XOR**、**NOT**，这些关键词的含义一目了然。然而，一些语言，如`C`、`C++`、`Java`或`R`，使用特殊字符代替书面形式：逻辑`AND`用和号（`&`）表示，逻辑`OR`用管道符号（`|`）表示，逻辑`NOT`用感叹号（`!`）表示。顺便说一句，现在你可以轻松理解为什么在这些语言中不等式用`!=`表示，它的意思就是“NOT equal”。

在`C`、`C++`、`Java`或`R`中，上面的if-then语句块会是这样的：

**如果** `(!is_account_locked() & (balance + overdraft >= amount | is_customerhistory_positive())) {...}`

在Visual Basic for Applications (VBA)宏语言中，它允许你自动化Microsoft Office套件的应用程序，你可以用描述性的标识符来编写这个if-then语句块：

**如果不是** `is_account_locked()` **且** (`balance + overdraftrest >= amount` **或** `is_customerhistory_positive()`) **则**…**结束如果**[10 分钟]

考虑以下程序片段：

`x = input("请输入一个数字：")`**如果** `x > 100` **则** `show("x 大于 100!")`**如果** `x > 50` **则** `show("x 大于 50!")`**如果** `x > 10` **则** `show("x 大于 10!")`**如果** `x < 0` **则** `show("x 小于 0!")`**如果** `x >= 0` **且** `x <= 10` **则** `show("x 在 0 到 10 之间!")`

1.  (a)

    用户输入`x`的值时，检查了多少个条件？

1.  (b)

    修改算法，使得在最好的情况下只检查一个条件，而在最坏的情况下才检查所有条件。

[3 分钟]

以下程序片段的错误在哪里？

`x = input("请输入一个数字：")`

**如果** `x > 100` **则** `show("x 大于 100!")`

**否则**

**开始**

**如果** `x >= 110` **则** `show("x 大于 110!")`

**否则** `show("x 小于或等于 100!")`

**结束**

## 14.6 使用`Switch-Case`结构高效检查类似条件（`Switch/Select…Case`）

有时你想一次检查多个相似的条件。想象一下，我们希望根据每月存入账户的金额来对我们的在线银行客户进行分类，从而能够为特别“优秀”的客户提供特殊服务。我们假设可以使用一个函数 `received_3months()` 来查询过去三个月的平均存入金额。在我们的伪代码语言中，客户分类可以这样写：

`If received_3months() < 1000 Then Begin category="D" End Else Begin If received_3months() < 2000 Then Begin category="C" End Else Begin If received_3months() < 4000 Then Begin category="B" End Else Begin category="A" End End End`

在这里，不同的平均月现金流入阈值通过嵌套的 `If-Else` 结构进行检查。然而，这种方式相对较难阅读。许多编程语言提供了一种结构，允许你更加优雅地检查多个类似的条件。在我们的示例中，这种表达方式可以写成如下：

`Switch received_3months() Begin Case < 1000: category="D" Case < 2000: category="C" Case < 4000: category="B" Else: category="A" End`

这种写法要清晰得多，因此更加易读，也更容易编程。关键字 `Switch` 后面首先是需要检查的变量。在我们的例子中，它就是我们函数 `received_3months()` 的返回值。`Case` 用来引入需要检查的条件，例如 `< 1000`。冒号后面是当条件成立时要执行的操作，在我们的例子中是设置客户类别。特殊关键字 `Else` 用于捕捉所有未通过特定条件显式检查的其他情况。如果没有任何条件适用，则触发这个语句。相反，如果某个条件适用，则执行与该条件相关的语句（在我们的例子中只有一个，但也可以有多个）。执行完该语句后，整个结构退出，也就是说，不再检查其他条件。而是程序在 `End` 后继续执行。

`Switch-Case` 结构的顺序示意图见图 ◘ [14.2](#Fig2)。![](../images/474412_1_En_14_Chapter/474412_1_En_14_Fig2_HTML.jpg)

`Switch-Case` 结构的流程图。输入给表达式，表达式块通过值、表达式的 else 块，并最终结束。

图 14.2

`Switch-Case` 结构的流程图

许多编程语言允许使用这种优雅的方式检查多个相似条件。通常，这种结构称为 `Switch-Case` 或 `Select-Case` 结构，源自这两个中央关键字 `switch` 或 `select` 以及 `case`，它们在大多数具有此类结构的编程语言中都很常见。令人困惑的是，有些语言使用关键字 `case` 来代替 `switch` 或 `select`，但我们在这里不再讨论这个问题。

例如，在支持`Switch-Case 结构`的语言`C`中，上述对客户类别的检查可以写成如下：

`switch`(`received_3months()`){`case` < 1000:`category`="D";`break`;`case` < 2000:`category`="C";`break`;`case` < 4000:`category`="B";`break`;`default`:`category`="A";`break`;}

## 14.7 事件

除了经典的`if`条件语句（包括它们的特殊版本`Switch-Case 结构`）之外，还有另一种重要的方法可以在程序运行时分支到程序的不同部分，那就是通过所谓的`事件`。

经典的条件语句在程序到达相应的位置时执行，该位置是分支条件所在的位置。因此，程序完全按`顺序`执行。然而，有时候，您并不知道程序流中具体什么时候需要进行分支。在这种情况下，事件可以派上用场。

想象一下，在我们的在线银行示例中，银行网站上有三个按钮：“新转账”、“将交易导出为文本文件”和“注销”，用户可以随时点击这些按钮。每个按钮背后都有不同的程序指令，但我们无法预先知道用户何时——以及是否——会触发相应的功能。

处理这个问题的基本方法有两种：

+   要么程序以几乎无限的循环运行，并且始终主动观察用户的行为，也就是检查用户是否点击了按钮。我们将在本书的稍后部分讨论循环，但基本的想法是，程序进入一个实际上无限重复的循环，并总是回到其起点重新运行。现在，只要用户点击了其中一个按钮，程序就执行该按钮背后的程序代码，然后返回到无限循环中，继续监控用户的行为。

+   第二种可能性是程序并不会在无限循环中等待用户，而是完成它应做的事情。然而，当它从外部得知用户已经点击了某个按钮时，它会立即跳转到一个函数，然后执行该按钮背后的指令。

这两种方法的区别在于，在第一种情况下，等待用户并监控他们的活动几乎会阻塞程序。它始终处于`主动监控状态`，不断检查某个按钮是否被点击。在第二种情况下，程序从`外部`得知某个`事件`已发生。一旦发生这种情况，与该事件关联的函数将被执行。这类函数也被称为`事件处理程序`，因为它们描述了如何处理事件。

这种方法节省了计算能力，因为第一种方法所需的主动观察就像主动倾听。它意味着信号必须不断处理，而通过事件控制，其他东西，如操作系统或解释器，会简单地通知您事件已发生。这使得程序可以在此期间做其他事情，并在事件发生时仍能作出反应。

它的工作方式类似于烤箱，您必须将其预热到某个温度才能烤制比萨饼。例如，只有当预热温度达到时，才能将比萨放入烤箱。您可以每隔几分钟去烤箱查看预热温度是否已经达到。或者，您可以有一个独立发出声响的烤箱，当它准备好时会发出信号。在第一种情况下，我们处于无限循环中，一遍又一遍地检查烤箱是否已经达到预热温度。在第二种情况下，其他人（在这种情况下是烤箱本身）通知我们“预热温度已达到”事件已经发生。只要这还没有发生，我们可以做其他事情，因为我们知道烤箱会在适当的时候报告。

许多编程语言支持事件的使用。由于这改变了程序的结构，我们在此上下文中称之为`事件导向编程范式`。支持事件处理的语言，如JavaScript，通常用于开发图形用户界面，在这些界面中，程序流并不是完全顺序的，您也无法预先确切知道哪个程序部分必须执行，因为用户的行为是不可预测的。一般来说，图形用户界面，如我们在►`Sect. [12.​2.​1](474412_1_En_12_Chapter.xhtml#Sec3)`中了解到的，是事件导向方法的典型应用。

事件控制程序的示意图如◘`Fig. [14.3](#Fig3)`所示。![](../images/474412_1_En_14_Chapter/474412_1_En_14_Fig3_HTML.jpg)

事件控制程序的流程图。事件1由事件循环的事件1到3组成。事件1与事件处理程序1连接，并返回事件循环。

`Fig. 14.3`

事件控制程序的流程图

顺便说一下，触发事件的不仅仅是用户。操作系统或连接的设备也可以触发事件，程序可以对此作出反应。例如，操作系统可以宣布它现在要关闭；这时，有事件处理程序的程序就有机会做出反应，在程序关闭之前保存当前的状态。同样，设备也可以触发事件，比如打印机或硬盘驱动器。

到目前为止，我们处理了事件处理程序的基本功能，但这些函数现在是什么样的呢？这里是上面示例的摘录（如往常一样，采用我们伪代码语言）：

`Function` `event_transfer(e)` `Begin` `create_transfer()` `End` `Function` `event_logout(e)` `Begin` `logout()` `End`

在这里，我们定义了两个事件处理程序，一个用于用户点击“新转账”按钮的事件，另一个用于用户想要注销的事件。如你所见，事件处理程序只是普通的函数。在某些语言中，事件处理程序会作为函数参数传递一个特殊对象（如上所示，`e` 类型为 `event`），该对象更详细地描述了事件。例如，对于一个每当用户移动鼠标时触发的事件，可以将当前鼠标指针的“坐标”作为对象的属性传递。事件处理程序函数随后可以从对象中获取这些坐标，并做出相应的反应。

这些函数和我们在►第[13](474412_1_En_13_Chapter.xhtml)章中学习到的函数的唯一区别在于，它们不是由我们程序员调用的，而是“外部调用”的。当事件发生时，解释器或操作系统会通知我们，并通过调用我们的事件处理程序，将事件对象 `e` 作为附加信息传递给它。因此，最终，事件处理程序只是我们开发的函数，但并不是我们自己调用的；我们只是为那些通知我们事件已经发生的人提供这些函数。

上述示例在 JavaScript 中的表现如下：

`function` `event_transfer() {create_transfer();}` `function` `event_logout() {logout();}`

为了让解释器知道在每个事件发生时调用哪个事件处理程序，网站 HTML 源代码中的按钮定义需要如下所示：

`<button onclick="event_transfer()">新转账</button><button onclick="event_logout()">注销</button>`

这样就创建了两个按钮，并将它们的（标准）`onclick` 事件与我们的事件处理程序连接起来，每当有人点击按钮时，就会触发这些事件。

在 Delphi 中，我们的事件处理程序将是这样的：

`procedure` `BankingForm.LogoutButtonClick(Sender: TObject);` `begin` `create_transfer();` `end`; `procedure` `BankingForm.NewTransferButtonClick(Sender: TObject);` `begin` `logout();` `end`;

在这里，我们将定义一个名为`BankingForm`的窗口（一个“表单”），在上面放置名为`NewTransferButton`和`LogoutButton`的按钮。事件处理程序不仅带有相应按钮的名称，还带有“Click”，即它们所处理的事件名称。这样，Delphi就能理解这是哪个事件，并且知道它所指的界面元素是什么。事件处理程序还通过`Sender`传递被点击的按钮，`Sender`在使用相同事件处理程序处理多个界面元素时变得非常有用，这时你需要在事件处理函数内区分触发事件的不同元素。

`14.5` [3分钟]

遵循事件驱动编程范式的程序与完全线性程序有何不同？

`14.6` [3分钟]

为什么事件控制特别适合图形用户界面？

## `14.8` 学习新编程语言的路线图

如果你正在学习一门新的编程语言……

你将会发现：

+   如何在该语言中构建`If-Else`语句（许多语言中用于此的关键字是`if`，`then`，`else`），

+   如何编写用于构建条件的比较运算符，

+   如何编写逻辑运算符，用于将多个基本条件组合成一个整体条件，

+   语言是否具有`Switch-Case`结构，如果有，如何构建（许多语言中用于此的关键字是`switch`，`select`，`case`），

+   代码块如何在该语言中被定界（即如何打开和关闭），以及如果代码块只包含一条语句，是否可以省略这些定界符，

+   语言是否支持事件，如果支持，如何定义事件处理程序（包括是否需要传递任何参数），以及如何将事件处理程序与事件链接，以便在事件发生时调用它们。

视图`14.4`中可以看到考虑的顺序控制结构概述。◘ 图示 [`14.4`](#Fig4)。![](../images/474412_1_En_14_Chapter/474412_1_En_14_Fig4_HTML.jpg)

一张表格展示了条件和事件。第1行包含基本条件和复杂条件，第2行包含3列的if-else语句、switch case语句和事件处理函数。

图示 `14.4`

顺序控制的条件和事件

## `14.9` 练习解答

练习 `14.1`

1.  `(a)`

    输出：`Result C`

1.  `(b)`

    输出：`Result B`

1.  `(c)`

    输出：`Result A`，`Result B`

1.  `(d)`

    无输出（没有任何条件覆盖`x`为负数的情况）

练习 `14.2` x = input("请输入一个数字：") `If` x > 10 `Then` `If` x > 20 `Then` show("Result A") `Else` show("Result B") `Else` `If` x > 0 `Then` show("Result B") `End`

在代码块 `If x > 10` 内部，我们首先检查 `x > 20`。如果这个条件不成立，我们知道 `x` 必定大于 `10`（否则程序根本不会进入这个代码块），但小于或等于 `20`。因此，只需在 `Result B` 的输出前放置关键字 `Else` 即可。

`练习 14.3`

1.  `(a)`

    五次。每个条件都会被检查，无论前一个条件的结果如何。

1.  `(b)`

    通过巧妙地嵌套 `If-Else` 结构，可以减少条件检查的次数。如果 `x` 小于 `0`，那么只检查一个条件。剩下的条件就不会被检查，因为它们在 `x < 0` 的 `else` 分支中。只有当 `x` 大于或等于 `0`，同时小于或等于 `10` 时，程序才会通过所有条件。

这里的诀窍是以一种方式安排条件，使得每个条件至少在理论上是可达成的。例如，如果我们将 `x > 10` 作为最外层的条件，那么像 `x > 50` 这样的条件将根本不再被检查，因为 `x > 10` 已经被评估为真，并且所有位于 `x > 10` 的 `else` 分支中的内容将不再被通过。

当然，使用 `Switch-Case` 构造（► 第[14.6节](#Sec6)）会是一个更加优雅且易读的解决方案。

`x = input("请输入一个数字: ") 如果 x < 0 则 显示("x 小于 0!") 否则 如果 x > 100 则 显示("x 大于 100!") 否则 如果 x > 50 则 显示("x 大于 50!") 否则 如果 x > 10 则 显示("x 大于 10!") 否则 如果 x >= 0 且 x <= 10 则 显示("x 在 0 到 10 之间!") 结束 结束 结束 结束 结束` `练习 14.4`

这个嵌套的 `If-Else` 结构的问题在于，它检查 `x` 是否大于或等于 `110` 的内部条件永远无法得到正面结果。如果 `x` 确实大于 `110`，外部条件 `x > 100` 已经为真，它的关联代码块（此处只包含一条语句）就会执行。另一方面，`else` 块只有在 `x` 小于或等于 `100` 时才会执行，但此时内部 `If-Then` 结构的条件（`x >= 110`）永远不可能为真。可以说，`x` 大于 `110` 的输出语句是孤立的。

`练习 14.5`

与线性程序不同，遵循事件导向编程范式的程序可以通过跳转到为此类事件精心开发的代码位置来响应事件（例如，用户点击按钮）。如果此刻没有事件需要处理，程序会仔细观察其环境，等待再次激活。当线性程序是从头到尾逐步执行的一长串指令时，事件导向程序由一组事件处理程序组成，即在相应事件发生时激活的函数。事件处理程序本身是指令序列，但程序不是执行线性控制流，而是根据当前处理的事件在事件处理程序之间来回跳转。

`练习 14.6`

图形用户界面通常给予用户很大的自由来决定调用哪些功能。用户往往不是被紧密引导的，而是从一系列选项中选择，这些选项通常反映在菜单、工具栏、按钮、标签和其他控件中。这就是事件驱动控制派上用场的地方，简单地调用与用户触发/激活的控件相关联的事件处理程序。
