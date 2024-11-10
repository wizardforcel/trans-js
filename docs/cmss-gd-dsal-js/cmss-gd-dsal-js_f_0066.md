## 单词构建器

下一个示例是一个算法，收集从单字符数组构建的每个两字符字符串组合。例如，给定数组 `["a", "b", "c", "d"]`，我们将返回一个包含以下字符串组合的新数组：

| ​  | [ |
| --- | --- |
| ​  | ​`'ab'`，​`'ac'`，​`'ad'`，​`'ba'`，​`'bc'`，​`'bd'`， |
| ​  | ​`'ca'`，​`'cb'`，​`'cd'`，​`'da'`，​`'db'`，​`'dc'` |
| ​  | ] |

以下是该算法的实现。让我们看看能否找出它的 Big O 效率：

| ​  | ​`function` wordBuilder(array) { |
| --- | --- |
| ​  | ​`const` collection = []; |
| ​  |  |
| ​  | ​`for` (​`const` [indexI, valueI] ​`of` array.entries()) { |
| ​  | ​`for` (​`const` [indexJ, valueJ] ​`of` array.entries()) { |
| ​  | ​`if` (indexI !== indexJ) { |
| ​  | collection.push(valueI + valueJ); |
| ​  | } |
| ​  | } |
| ​  | } |
| ​  |  |
| ​  | ​`return` collection; |
| ​  | } |

在这里，我们在一个循环内部运行另一个循环。外层循环遍历数组中的每个字符，并跟踪 valueI 的索引。对于每个 indexI，我们运行一个内部循环，再次遍历同一数组中的每个字符，使用索引 indexJ。在这个内部循环中，我们连接 indexI 和 indexJ 处的字符，除了当 indexI 和 indexJ 指向相同的索引时。

为了确定我们算法的效率，我们再次需要确定 N 数据元素是什么。在我们的例子中，和之前的例子一样，N 是传递给函数的数组中的项数。

下一步是确定我们的算法相对于 N 数据元素所需的步骤数。在我们的例子中，外层循环遍历所有 N 元素，而对于每个元素，内层循环再次遍历所有 N 元素，这相当于 N 步乘以 N 步。这是经典的 O(N²) 情况，通常嵌套循环算法的结果就是这样。

现在，如果我们修改算法以计算每个三字符字符串的组合，会发生什么呢？对于我们示例数组 `["a", "b", "c", "d"]`，我们的函数将返回以下数组：

| ​  | [ |
| --- | --- |
| ​  | ​`'abc'`，​`'abd'`，​`'acb'`， |
| ​  | ​`'acd'`，​`'adb'`，​`'adc'`， |
| ​  | ​`'bac'`，​`'bad'`，​`'bca'`， |
| ​  | ​`'bcd'`，​`'bda'`，​`'bdc'`， |
| ​  | ​`'cab'`，​`'cad'`，​`'cba'`， |
| ​  | ​`'cbd'`，​`'cda'`，​`'cdb'`， |
| ​  | ​`'dab'`，​`'dac'`，​`'dba'`， |
| ​  | ​`'dbc'`，​`'dca'`，​`'dcb'` |
| ​  | ] |

这是一个使用三个嵌套循环的实现。它的时间复杂度是什么？

| ​  | ​`function` wordBuilder(array) { |
| --- | --- |
| ​  | ​`const` collection = []; |
| ​  |  |
| ​  | ​`for` (​`const` [indexI, valueI] ​`of` array.entries()) { |
| ​  | ​`for` (​`const` [indexJ, valueJ] ​`of` array.entries()) { |
| ​  | ​`for` (​`const` [indexK, valueK] ​`of` array.entries()) { |
| ​  | `if` (indexI !== indexJ && indexJ !== indexK && indexI !== indexK) { |
| ​  | `collection.push(valueI + valueJ + valueK);` |
| ​  | } |
| ​  | } |
| ​  | } |
| ​  | } |
| ​  |  |
| ​  | `return` collection; |
| ​  | } |

在这个算法中，对于N个数据元素，我们有N步的`i`循环乘以N步的`j`循环再乘以N步的`k`循环。这是`N * N * N`，即`N³`步，描述为`O(N³)`。

如果我们有四个或五个嵌套循环，那么相应的算法将是`O(N⁴)`和`O(N⁵)`。让我们看看这些在图上是如何出现的，如[所示](#fig.ch7.big_o_graph_with_arrows)。

![images/big_o_in_everyday_code/big_o_graph_with_arrows.png](images/big_o_in_everyday_code/big_o_graph_with_arrows.png)

将任何代码从`O(N³)`的速度优化到`O(N²)`将是一个很大的胜利，因为代码会变得指数级更快。然而，上面的算法仍然停留在`O(N³)`。
