## 重叠子问题

斐波那契数列是一个数学数列，延续至无穷大：

0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55…

这个数列以0和1开始，每个后续的数字是前两个数字的总和。例如，数字55是因为它是前两个数字21和34的总和。

以下JavaScript函数返回斐波那契数列中的第N个数字。例如，如果我们将数字10传递给函数，它将返回55，因为55是该系列中的第十个数字。（0被视为该系列中的第0个数字。）

| ​  | `function` fib(n) { |
| --- | --- |
| ​  | `if` (n === 0 | | n === 1) { |
| ​  | `return` n; |
| ​  | } |
| ​  |  |
| ​  | `return` fib(n - 2) + fib(n - 1); |
| ​  | } |

这个函数中的关键行如下：

| ​  | `return` fib(n - 2) + fib(n - 1); |
| --- | --- |

这一行将斐波那契数列中的前两个数字相加。这是一个美丽的递归函数。

然而，你现在脑海中应该响起警报，因为我们的函数自我调用了两次。

以计算第六个斐波那契数为例。函数 `fib(6)` 调用了 `fib(4)` 和 `fib(5)`，如下面的图所示：

![images/dynamic_programming/simple_fib_6.png](images/dynamic_programming/simple_fib_6.png)

正如我们所见，一个函数自我调用两次，容易导致 `O(2^N)` 的情况。实际上，`fib(6)` 所做的所有递归调用在 [图示](#fig.ch12.complete_fib_6) 中都有显示。

![images/dynamic_programming/complete_fib_6.png](images/dynamic_programming/complete_fib_6.png)

你得承认，`O(2^N)` 看起来确实有点吓人。

虽然一个简单的改变成功优化了本章的第一个例子，但优化我们的斐波那契数列并不那么简单。

这并不是因为我们只能在一个变量中保存一段数据。我们需要同时计算 `fib(n - 2)` 和 `fib(n - 1)`（因为每个斐波那契数字是这两个数字的总和），仅存储一个结果并不能给我们另一个的结果。

这是计算机科学家所称的重叠子问题的一个案例。让我们深入探讨一下这个术语。

当一个问题通过解决同一问题的小版本来解决时，小问题被称为子问题。这个概念并不新颖——在我们讨论递归时经常会遇到。在斐波那契数列的案例中，我们通过先计算序列中的较小数字来计算每个数字。这些较小数字的计算就是子问题。

使这些子问题重叠的原因在于，`fib(n - 2)`和`fib(n - 1)`最终会调用许多相同的函数。具体来说，`fib(n - 1)`会进行一些`fib(n - 2)`已经做过的相同计算。例如，在之前的图中可以看到，`fib(5)`调用了`fib(3)`，尽管`fib(4)`已经调用过它。还有许多其他调用也是重复的。

好吧，看起来我们已经走到了死胡同。我们的斐波那契示例需要进行许多重叠的函数调用，而我们的算法以`O(2^N)`的速度缓慢推进。我们真的无能为力。

或者说并非如此？