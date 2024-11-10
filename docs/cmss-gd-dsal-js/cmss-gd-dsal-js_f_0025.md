## 有序数组

有序数组几乎与我们在上一章看到的经典数组相同。唯一的区别是有序数组要求值始终保持——没错——有序；也就是说，每次添加一个值时，它都被放置在适当的单元格中，以保持数组中的值排序。

例如，我们取数组`[3, 17, 80, 202]`：

![images/binary_search/binary_search_1.png](images/binary_search/binary_search_1.png)

假设我们想将值`75`插入数组。如果这个数组是经典数组，我们可以将`75`插入到末尾，如下所示：

![images/binary_search/binary_search_2.png](images/binary_search/binary_search_2.png)

正如我们在上一章看到的，计算机可以在一步之内完成这个。

另一方面，如果这是一个有序数组，我们就不得不将`75`插入到正确的位置，以使值保持升序：

![images/binary_search/binary_search_3.png](images/binary_search/binary_search_3.png)

现在，这说起来容易做起来难。计算机不能简单地将`75`一次性放入正确的插槽，因为它首先需要找到插入`75`的正确位置，然后移动其他值以腾出空间。让我们逐步解析这个过程。

让我们从原始有序数组重新开始：

![images/binary_search/binary_search_1.png](images/binary_search/binary_search_1.png)

第1步：我们检查索引`0`的值，以确定我们要插入的值`75`应该放在左边还是右边：

![images/binary_search/binary_search_4.png](images/binary_search/binary_search_4.png)

因为`75`大于`3`，我们知道`75`将被插入到`3`的右侧。然而，我们尚不知道它应该插入哪个单元格，因此我们需要检查下一个单元格。

我们将这种步骤称为比较，其中我们将要插入的值与已存在于有序数组中的数字进行比较。

第2步：我们检查下一个单元格的值：

![images/binary_search/binary_search_5.png](images/binary_search/binary_search_5.png)

由于`75`大于`17`，我们需要继续前进。

第3步：我们检查下一个单元格的值：

![images/binary_search/binary_search_6.png](images/binary_search/binary_search_6.png)

我们遇到了值`80`，它大于我们希望插入的`75`。由于我们已经到达第一个大于`75`的值，我们可以得出结论，`75`必须放在`80`的左侧，以保持这个有序数组的顺序。为此，我们需要移动数据以为`75`腾出空间。

第4步：将最后一个值向右移动：

![images/binary_search/binary_search_7.png](images/binary_search/binary_search_7.png)

第5步：将倒数第二个值向右移动：

![images/binary_search/binary_search_8.png](images/binary_search/binary_search_8.png)

第6步：我们终于可以将`75`插入到正确的位置：

![`images/binary_search/binary_search_9.png`](images/binary_search/binary_search_9.png)

结果是，在插入有序数组时，我们始终需要在实际插入之前进行一次搜索，以确定插入的正确位置。这是经典数组与有序数组之间性能的一个区别。

我们可以在这个例子中看到，最初有四个元素，而插入过程花费了六个步骤。在`N`的情况下，我们可以说，对于有序数组中的`N`个元素，插入总共花费了`N + 2`个步骤。

有趣的是，插入所需的步骤数量在有序数组中无论新值最终位于何处都保持相似。如果我们的值最终位于有序数组的开头，我们会有更少的比较和更多的移动。如果我们的值最终位于末尾，我们会有更多的比较但更少的移动。当新值恰好位于末尾时，所需的步骤最少，因为不需要移动。在这种情况下，我们需要`N`步来将新值与所有`N`个现有值进行比较，再加上一步插入本身，总共为`N + 1`步。

虽然在有序数组中插入的效率不如在经典数组中高，但有序数组在搜索时却有一种秘密超能力。
