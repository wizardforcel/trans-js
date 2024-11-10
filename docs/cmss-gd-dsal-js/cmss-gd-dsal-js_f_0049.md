## `选择排序`

在上一章中，我们探讨了一种称为`冒泡排序`的排序算法，其效率为`O(N²)`。现在我们将深入研究另一种排序算法，称为`选择排序`，看看它与`冒泡排序`的比较。

`选择排序`的步骤如下：

1.  我们从左到右检查数组的每个单元格，以确定哪个值是最小的。当我们在单元格之间移动时，我们会跟踪到目前为止遇到的最低值。（我们会通过将其索引存储在一个变量中来做到这一点。）如果我们遇到一个包含比我们变量中值更低的单元格，我们就会替换它，以便变量现在指向新的索引。请参见以下图示：

    ![images/optimizing_code_with_and_without_big_o/set_of_four.png](images/optimizing_code_with_and_without_big_o/set_of_four.png)![images/optimizing_code_with_and_without_big_o/swap.png](images/optimizing_code_with_and_without_big_o/swap.png)![images/optimizing_code_with_and_without_big_o/post_swap.png](images/optimizing_code_with_and_without_big_o/post_swap.png)

1.  一旦我们确定了哪个索引包含最低值，我们就将其值与我们开始遍历时的值进行交换。在第一次遍历中，这将是索引`0`，在第二次遍历中是索引`1`，依此类推。这里的图示展示了第一次遍历中的交换过程。

1.  每次遍历由步骤1和步骤2组成。我们重复遍历，直到达到一个将从数组末尾开始的遍历。此时，数组将完全排序。
