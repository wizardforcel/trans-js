## 处理冲突

哈希表非常棒，但也并非没有复杂性。

继续我们的同义词例子：如果我们想将以下条目添加到同义词库中，会发生什么？

| ​  | `thesaurus[​*"dab"*​] = ​*"pat"*​;` |
| --- | --- |

首先，计算机会对键进行哈希：

`DAB = 4 * 1 * 2 = 8`

然后，它会尝试将`"pat"`添加到我们哈希表的单元格`8`：

![`images/blazing_fast_lookup_with_hashes/hash_4.png`](images/blazing_fast_lookup_with_hashes/hash_4.png)

噢，不。单元格`8`已经被`"evil"`填满了——字面意思！

尝试将数据添加到已填满的单元格中称为冲突。幸运的是，有解决方法。

一种处理冲突的经典方法称为分离链表。当发生冲突时，它不是将单个值放入单元格，而是放入对一个数组的引用。

让我们更仔细地看一下哈希表底层数据存储的一个子部分：

![`images/blazing_fast_lookup_with_hashes/hash_5.png`](images/blazing_fast_lookup_with_hashes/hash_5.png)

在我们的例子中，计算机想将`"pat"`添加到单元格`8`，但它已经包含`"evil"`。所以它用一个数组替换单元格`8`的内容，如下所示：

![`images/blazing_fast_lookup_with_hashes/hash_6.png`](images/blazing_fast_lookup_with_hashes/hash_6.png)

该数组包含子数组，其中第一个值是单词，第二个值是其同义词。

让我们逐步了解在这种情况下哈希表查找是如何工作的。假设我们查找以下单词：

| ​  | `thesaurus[​*"dab"*​]` |
| --- | --- |

计算机执行以下步骤：

1.  它对键进行哈希：`DAB = 4 * 1 * 2 = 8`。

1.  它查找单元格`8`。计算机注意到单元格`8`包含一个数组的数组，而不是单个值。

1.  它通过数组线性搜索，查看每个子数组的索引`0`，直到找到我们的键（`"dab"`）。然后返回正确子数组索引`1`的值。

让我们可视化这些步骤。

我们对`DAB`进行哈希到`8`，所以计算机检查那个单元格：

![`images/blazing_fast_lookup_with_hashes/hash_7.png`](images/blazing_fast_lookup_with_hashes/hash_7.png)

由于单元格`8`包含一个子数组的数组，我们开始在线性搜索中遍历每个子数组，从第一个开始。我们检查第一个子数组的索引`0`：

![`images/blazing_fast_lookup_with_hashes/hash_8.png`](images/blazing_fast_lookup_with_hashes/hash_8.png)

它不包含我们要找的键（`"dab"`），所以我们继续检查下一个子数组的索引`0`：

![`images/blazing_fast_lookup_with_hashes/hash_9.png`](images/blazing_fast_lookup_with_hashes/hash_9.png)

我们找到`"dab"`，这表明该子数组索引`1`的值（`"pat"`）就是我们要找的值。

在计算机碰到一个引用数组的单元格的情况下，它的搜索可能需要额外的步骤，因为它需要在多个值的数组中进行线性搜索。如果我们的所有数据都最终落在哈希表的单个单元格中，我们的哈希表就和数组没有区别。因此，实际上哈希表查找的最坏情况性能是`O(N)`。

因此，设计哈希表时至关重要的一点是确保冲突较少，因此通常在`O(1)`时间内执行查找，而不是`O(N)`时间。

幸运的是，大多数编程语言都实现了哈希表并为我们处理这些细节。然而，通过理解其背后的工作原理，我们可以更好地理解哈希表如何实现`O(1)`的性能。

让我们看看如何设置哈希表以避免频繁的冲突。
