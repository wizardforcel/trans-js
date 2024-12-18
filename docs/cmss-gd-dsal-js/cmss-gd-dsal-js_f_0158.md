## 查找最后节点

虽然插入算法看似简单，但有一个小问题。第一步要求我们将新值放置为堆的最后节点。但这引出了一个问题：我们如何找到将成为最后节点的位置？

让我们再看看插入`40`之前的堆：

![images/heaps/foundational_heap.png](images/heaps/foundational_heap.png)

我们通过查看图示知道，要将`40`变成最后节点，我们需要将其设置为`8`的右孩子，因为那是底层行中的下一个可用位置。

但是计算机没有眼球，它不会把堆看作一堆行。它看到的只是根节点，它可以通过链接跟随子节点。那么我们如何为计算机创建一个算法来找到新值的位置呢？

以我们的示例堆为例。当我们从`100`的根节点开始时，我们是否告诉计算机在`100`的右侧后代中寻找新最后节点的下一个可用位置？

虽然在我们的示例堆中，下一个可用位置位于`100`的右侧后代中，但看看下面的替代堆：

![images/heaps/last_node_on_left_side.png](images/heaps/last_node_on_left_side.png)

在这个堆中，新最后节点的下一个可用位置将是`88`的右孩子，这个位置位于`100`的左侧后代中。

从本质上讲，正如在堆中搜索是不可能的那样，在不检查每一个节点的情况下，也不可能有效地找到堆的最后节点（或下一个可用位置以容纳新的最后节点）。

那么我们如何找到下一个可用节点呢？我稍后会解释这个问题，但现在让我们将这个问题称为最后节点的问题。我保证我们会回到这个问题。

与此同时，让我们探讨堆的另一个主要操作，即删除。
