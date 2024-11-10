## 阅读递归代码

习惯于递归需要时间和练习，最终你会学会两套技能：阅读递归代码和编写递归代码。阅读递归代码相对简单，因此我们先来练习这个。

我们将通过看另一个例子来做这个：计算阶乘。

阶乘最好通过一些例子来说明。

这是3的阶乘：

3 * 2 * 1 = 6

这是5的阶乘：

5 * 4 * 3 * 2 * 1 = 120

以此类推。

这是一个递归实现，它返回一个数的阶乘：

| ​  | `function` `factorial`(number) { |
| --- | --- |
| ​  | `if` (number <= 1) { |
| ​  | `return` 1; |
| ​  | } `else` { |
| ​  | `return` number * `factorial`(number - 1); |
| ​  | } |
| ​  | } |

这段代码初看起来可能有些混乱。为了走查代码以查看它的功能，以下是我推荐的过程：

1.  确定基本情况。

1.  遍历基本情况的函数。

1.  确定倒数第二个情况。这是刚好在基本情况之前的情况，如我稍后将演示的那样。

1.  遍历倒数第二个情况的函数。

1.  通过识别你刚分析的情况之前的情况，并遍历该情况的函数，重复这个过程。

让我们将这个过程应用到前面的代码。如果我们分析代码，会很快注意到有两条路径。一条路径是当number小于或等于1时，另一条路径是当number大于1时：

| ​  | `if` (number <= 1) { `// Path 1` |
| --- | --- |
| ​  | ... |
| ​  | } `else` { `// Path 2: number is greater than 1` |
| ​  | ... |
| ​  | } |

我们可以看到递归发生在`else`路径中，因为`factorial`调用了自身：

| ​  | `else` { |
| --- | --- |
| ​  | `return` number * `factorial`(number - 1); |
| ​  | } |

所以基本情况必须是第一条路径，因为这是没有发生递归的路径：

| ​  | `if` (number <= 1) { |
| --- | --- |
| ​  | `return` 1; |
| ​  | } |

然后我们可以得出结论，基本情况是当number小于或等于1时。

接下来，让我们逐步分析`factorial`方法，假设它处理的是一个基本情况，例如`factorial`(1)。再次提醒，相关的代码如下：

| ​  | `if` (number <= 1) { |
| --- | --- |
| ​  | `return` 1; |
| ​  | } |

好吧，这很简单——这是基本情况，所以实际上没有发生递归。如果我们调用`factorial`(1)，该方法简单地返回1。好的，拿张纸巾把这个事实写下来：

![images/recursively_recurse_with_recursion/napkin_1.png](images/recursively_recurse_with_recursion/napkin_1.png)

接下来，让我们上升到下一个情况，即`factorial`(2)。我们方法中相关的代码行是：

| ​  | `else` { |
| --- | --- |
| ​  | `return` number * `factorial`(number - 1); |
| ​  | } |

所以调用`factorial(2)`将返回`2 * factorial(1)`。要计算`2 * factorial(1)`，我们需要知道`factorial(1)`返回什么。如果你查看你的便签，你会看到它返回`1`。所以`2 * factorial(1)`将返回`2 * 1`，正好是`2`。

把这个事实添加到你的便签上：

![images/recursively_recurse_with_recursion/napkin_2.png](images/recursively_recurse_with_recursion/napkin_2.png)

现在，如果我们调用`factorial(3)`会发生什么？再次，这里是相关的代码行：

| ​  | `**否则**`​ { |
| --- | --- |
| ​  | `**返回**`​ `number * factorial(number - 1);` |
| ​  | } |

所以这可以转化为`return 3 * factorial(2)`。`factorial(2)`返回什么？你不必再重新思考，因为它在你的便签上！它返回`2`。所以，`factorial(3)`将返回`6`（因为`3 * 2 = 6`）。继续将这个精彩的事实添加到你的便签上：

![images/recursively_recurse_with_recursion/napkin_3.png](images/recursively_recurse_with_recursion/napkin_3.png)

花点时间自己想一想`factorial(4)`将返回什么。

正如你所看到的，从基本情况开始分析并逐步构建是一种很好的推理递归代码的方法。
