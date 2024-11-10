## 不必要的递归调用

这是一个递归函数，用于从数组中找到最大数：

| ​  | `function` max(array) { |
| --- | --- |
| ​  | `if` (array.length === 0) { `return` `null`; } |
| ​  |  |
| ​  | `if` (array.length === 1) { `return` array[0]; } |
| ​  |  |
| ​  | `if` (array[0] > `max`(array.slice(1))) { |
| ​  | `return` array[0]; |
| ​  | } `else` { |
| ​  | `return` `max`(array.slice(1)); |
| ​  | } |
| ​  | } |

每个递归调用的本质是将单个数字（`array[0]`）与剩余数组中的最大数字进行比较。（为了计算剩余数组中的最大数，我们调用了当前函数`max`，这就是使函数递归的原因。）

我们通过条件语句实现比较。条件语句的前半部分如下：

| ​  | `if` (array[0] > `max`(array.slice(1))) { |
| --- | --- |
| ​  | `return` array[0]; |
| ​  | } |

这段代码表示，如果单个数字（`array[0]`）大于已经确定为剩余数组的最大数（`max(array.slice(1))`），那么根据定义，`array[0]`必须是最大数，因此我们返回它。

这是条件语句的后半部分：

| ​  | `else` { |
| --- | --- |
| ​  | `return` `max`(array.slice(1)); |
| ​  | } |

这个第二段代码表示，如果`array[0]`不大于剩余数组中的最大数，那么剩余数组中的最大数一定是总体的最大数，我们返回它。

虽然这段代码有效，但它包含了一个隐藏的低效。如果仔细观察，您会注意到我们的代码中有两次出现了`max(array.slice(1))`，分别在条件语句的两半中。

问题在于每次提到`max(array.slice(1))`时，我们都会触发一连串的递归调用。

让我们用数组`[1, 2, 3, 4]`来分解这个例子。

我们知道，我们将开始比较`1`与剩余数组`[2, 3, 4]`的最大数。这将进一步比较`2`与剩余数组`[3, 4]`的最大值，而后又比较`3`与`[4]`。这也会触发对`[4]`本身的一个递归调用，这是基线情况。

然而，为了真正了解我们的代码如何执行，我们将从分析底部调用开始，并逐步向上工作调用链。

让我们开始吧。

### 最大递归遍历

当我们调用`max([4])`时，函数简单地返回数字`4`。这再次是因为我们的基线情况是数组只包含一个元素，如下面这行代码所规定的：

| ​  | `if` (array.length === 1) { |
| --- | --- |
| ​  | `return` array[0]; |
| ​  | } |

这非常简单——这是一个单独的函数调用：

![images/dynamic_programming/single_function_call.png](images/dynamic_programming/single_function_call.png)

向上回溯调用链，让我们看看当我们调用`max([3, 4])`时会发生什么。在条件语句的前半部分（`if (array[0] > max(array.slice(1)))`），我们将3与`max([4])`进行比较。但是调用`max([4])`本身就是一个递归调用。下面的图示描绘了`max([3, 4])`调用`max([4])`的过程：

![images/dynamic_programming/first_recursive_call.png](images/dynamic_programming/first_recursive_call.png)

注意，在箭头旁边，我们放置了标签“1st”以表示这个递归调用是由`max([3, 4])`条件语句的前半部分触发的。

在完成这一步后，我们的代码现在可以将3与`max([4])`的结果进行比较。由于3不大于该结果（4），我们触发条件的第二部分。（这段代码是`return max(array.slice(1));`）在这种情况下，我们返回`max([4])`。

但是当我们的代码返回`max([4])`时，它触发了实际的函数调用`max([4])`。这已经是我们第二次触发`max([4])`的调用：

![images/dynamic_programming/second_recursive_call.png](images/dynamic_programming/second_recursive_call.png)

正如你所见，函数`max([3, 4])`最后调用了`max([4])`两次。当然，如果我们不需要的话，最好避免这样做。如果我们已经计算过`max([4])`的结果，为什么还要再次调用同样的函数来获取相同的结果呢？

当我们向上移动一个调用链级别时，这个问题会变得更加严重。

当我们调用`max([2, 3, 4])`时，会发生以下情况。

在条件的前半部分，我们将2与`max([3, 4])`进行比较，而我们已经确定这看起来是这样的：

![images/dynamic_programming/second_recursive_call.png](images/dynamic_programming/second_recursive_call.png)

所以`max([2, 3, 4])`调用`max([3, 4])`的情况如下：

![images/dynamic_programming/max_2_3_4_first.png](images/dynamic_programming/max_2_3_4_first.png)

但这里有个关键点。这只是`max([2, 3, 4])`条件的前半部分。对于条件的后半部分，我们又调用了`max([3, 4])`：

![images/dynamic_programming/max_2_3_4_second.png](images/dynamic_programming/max_2_3_4_second.png)

哎呀！

让我们勇敢地回到调用链的顶部，调用`max([1, 2, 3, 4])`。经过所有操作后，在我们为条件的两个部分调用`max`之后，我们得到如[图示](#fig.ch12.max_1_2_3_4)所示的结果。

![images/dynamic_programming/max_1_2_3_4.png](images/dynamic_programming/max_1_2_3_4.png)

所以当我们调用`max([1, 2, 3, 4])`时，实际上我们触发了`max`函数十五次。

我们可以通过在函数开头添加语句`console.log('RECURSION')`来直观地看到这一点：

| ​  | **function**​ `max(array)` { |
| --- | --- |
| ​  | `console.log('RECURSION');` |
| ​  |  |
| ​  | `// 省略其余代码以简化` |
| ​  | } |

当我们运行代码时，会看到单词`RECURSION`在终端打印了十五次。

现在，我们确实需要其中一些调用，但并不是所有的调用。例如，我们确实需要计算`max([4])`，但一个这样的函数调用就足够得出计算结果。然而在这里，我们调用了该函数八次。
