## 栈

栈以与数组相同的方式存储数据——它仅仅是一个元素列表。唯一的限制是栈有以下三个约束：

+   数据只能在栈的末尾插入。

+   数据只能从栈的末尾删除。

+   只有栈的最后一个元素可以被读取。

你可以把栈想象成一堆实际的盘子；你无法查看除了顶部盘子以外的任何盘子。同样，你不能将任何盘子添加到栈的顶部以外的地方，也不能移除除顶部盘子以外的任何盘子。（至少，你不应该这样做。）实际上，大多数计算机科学文献将栈的末尾称为顶部，而将栈的开头称为底部。

我们的图示将通过将栈视为垂直数组来反映这一术语，如下所示：

![images/stacks_and_queues/going_vertical.png](images/stacks_and_queues/going_vertical.png)

如你所见，数组中的第一个项成为栈的底部，而最后一个项成为栈的顶部。

尽管栈的限制似乎——好吧——有些限制，但我们很快会看到这对我们是有好处的。

要观察栈的实际操作，让我们从一个空栈开始。

向栈中插入新值也称为将其推入栈中。可以把它想象成在盘子堆的顶部添加一道菜。

让我们将`5`推入栈中：

![images/stacks_and_queues/push_5.png](images/stacks_and_queues/push_5.png)

再次说明，这里没有什么复杂的。我们实际上只是将一个数据元素插入数组的末尾。

现在让我们将`3`推入栈中：

![images/stacks_and_queues/push_3.png](images/stacks_and_queues/push_3.png)

接下来，让我们将`0`推入栈中：

![images/stacks_and_queues/push_0.png](images/stacks_and_queues/push_0.png)

请注意，我们总是将数据添加到栈的顶部（也就是末尾）。如果我们想在栈的底部或中间插入`0`，我们是不能的，因为这就是栈的特性：数据只能添加到顶部。

从栈的顶部删除元素称为从栈中弹出。由于栈的限制，我们只能从顶部弹出数据。

让我们从示例栈中弹出一些元素。

首先，我们弹出`0`：

![images/stacks_and_queues/pop_0.png](images/stacks_and_queues/pop_0.png)

我们的栈现在仅包含两个元素：`5`和`3`。

接下来，我们弹出`3`：

![images/stacks_and_queues/pop_3.png](images/stacks_and_queues/pop_3.png)

我们的栈现在只包含`5`：

![images/stacks_and_queues/only_5.png](images/stacks_and_queues/only_5.png)

一个用于描述栈操作的方便缩写是`LIFO`，表示后进先出。这意味着最后推入栈的项总是第一个被弹出的。这有点像那些懒惰的学生——他们总是最后到达教室，但却是第一个离开的。
