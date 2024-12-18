## 最后一个节点的问题……再次

虽然堆的删除算法看起来很简单，但它再次引发了最后一个节点的问题。

我解释了删除的第一步需要将最后一个节点移动并将其变成根节点。但我们到底该如何找到最后一个节点呢？

在解决最后一个节点的问题之前，让我们先探讨一下插入和删除为什么如此依赖最后一个节点。为什么我们不能在堆的其他地方插入新值？而且，为什么在删除时，我们不能用根节点以外的其他节点替换根节点？

现在，仔细想一想，你会意识到如果我们使用其他节点，堆将变得不完整。但这引出了下一个问题：为什么完整性对堆如此重要？

完整性之所以重要，是因为我们希望确保我们的堆保持良好平衡。

为了清楚地看到这一点，让我们再看看插入。假设我们有以下堆：

![images/heaps/small_heap.png](images/heaps/small_heap.png)

如果我们想在这个堆中插入一个`5`，保持堆良好平衡的唯一方法是将`5`作为最后一个节点——在这种情况下，将其设为`10`的子节点：

![images/heaps/make_5_last_node.png](images/heaps/make_5_last_node.png)

任何替代这个算法的方案都会导致失衡。比如，在一个替代宇宙中，算法是将新节点插入最左下角的节点，我们可以通过遍历左子节点直到底部轻易找到这个位置。这将使`5`成为`15`的子节点：

![images/heaps/make_5_child_of_15.png](images/heaps/make_5_child_of_15.png)

我们的堆现在有些失衡，容易看出如果我们不断在最左下角插入新节点，失衡会变得更加严重。

同样，在从堆中删除时，我们总是将最后一个节点变为根节点，因为否则堆可能会变得失衡。再次以我们的示例堆为例：

![images/heaps/small_heap.png](images/heaps/small_heap.png)

如果在我们的替代宇宙中，我们总是将最右下角的节点移动到根位置，`10`将成为根节点，我们将最终得到一个失衡的堆，左侧后代众多而右侧后代为零。

现在，平衡之所以如此重要，是因为这使我们能够实现`O(log N)`的操作。在以下这种严重失衡的树中，遍历可能需要`O(N)`步：

![images/heaps/imbalanced_heap.png](images/heaps/imbalanced_heap.png)

但这又回到了最后一个节点的问题。什么算法能让我们持续找到任何堆的最后一个节点？（同样，无需遍历所有`N`个节点。）

而这正是情节的突然转折。
