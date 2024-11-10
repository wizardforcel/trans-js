## 第1章

这些是本节中练习的解决方案，链接为 [​`练习`](f_0023.xhtml#why.data.structures.matter.exercises)。

1.  让我们逐一分析每种情况：

    1.  从数组读取操作始终只需一步。

    1.  在大小为100的数组中搜索一个不存在的元素将需要100步，因为计算机需要检查数组中的每个元素，以确定该元素无法找到。

    1.  插入操作将需要101步：将每个元素向右移动100步，然后一步将新元素插入数组的开头。

    1.  在数组末尾插入操作始终只需一步。

    1.  删除操作将需要100步：首先计算机删除第一个元素，然后将剩余的99个元素逐个向左移动。

    1.  在数组末尾删除操作始终只需一步。

1.  让我们逐一分析每种情况：

    1.  与数组一样，从基于数组的集合读取只需一步。

    1.  与数组一样，搜索基于数组的集合将需要100步，因为我们在确认元素不存在之前要检查每个元素。

    1.  为了插入集合，我们首先需要进行一次完整搜索，以确保该值不在集合中。此搜索将需要100步。然后，我们需要将所有100个元素向右移动，以为新值腾出空间。最后，我们将新值放在集合的开头。这总共需要201步。

    1.  此次插入需要101步。同样，我们需要在插入之前进行一次完整搜索，这需要100步。最后一步是在集合的末尾插入新值。

    1.  删除操作将需要100步，和经典数组一样。

    1.  删除操作将只需一步，和经典数组一样。

1.  如果数组包含`N`个元素，在数组中搜索字符串`"apple"`的所有实例将需要`N`步。当只搜索一个实例时，我们可以在找到它后立即结束搜索。但如果我们需要找到所有实例，就必须检查整个数组的每个元素。