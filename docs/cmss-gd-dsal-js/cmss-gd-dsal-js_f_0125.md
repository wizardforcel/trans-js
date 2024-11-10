## `Quicksort`的最坏情况

对于我们遇到的许多其他算法，最佳情况是数组已经排序。而对于`Quicksort`来说，最佳情况是主元（pivot）总是落在分区的中间。有趣的是，这种情况通常发生在数组中的值混合得相当好。

`Quicksort`的最坏情况是主元总是位于子数组的一侧，而不是在中间。这种情况可能发生在数组完全按升序或降序排列时。这个过程的可视化在这里展示：

![images/divide_and_conquer_code_in_turbo_mode/visualization.png](images/divide_and_conquer_code_in_turbo_mode/visualization.png)

在这个图表中，你可以看到主元总是位于每个子数组的左端。

虽然在这种情况下每个分区仍然只涉及一次交换，但由于比较次数的增加，我们会失去效率。在第一个例子中，当主元总是接近中间时，每个分区后的子数组相对较小（最大的子数组大小为`4`）。而在这个例子中，前五个分区发生在大小为`4`或更大的子数组上。每个分区的比较次数与子数组中的元素数量相同。

所以在这个最坏情况下，我们有`8 + 7 + 6 + 5 + 4 + 3 + 2 + 1`个元素的分区，这导致总共`36`次比较。

用公式化的语言来说，我们可以说，对于`N`个元素，有`N + (N - 1) + (N - 2) + (N - 3) … + 1`步。我们在讨论[*获取所有产品*](f_0072.xhtml#sect.get-all-the-products)时看到，这计算为`N² / 2`步，对于大O的目的来说是`O(N²)`。

所以在最坏情况下，`Quicksort`的效率为`O(N²)`。

### `Quicksort`与`Insertion Sort`

现在我们已经掌握了`Quicksort`，让我们将其与一种较简单的排序算法进行比较，比如`Insertion Sort`：

|  | 最佳情况 | 平均情况 | 最坏情况 |
| --- | --- | --- | --- |
| 插入排序 | O(N) | O(N²) | O(N²) |
| 快速排序 | O(N log N) | O(N log N) | O(N²) |

我们可以看到它们的最坏情况是相同的，并且在最佳情况下`Insertion Sort`比`Quicksort`更快。然而，`Quicksort`之所以优于`Insertion Sort`，是因为在平均情况下的表现——这也是大多数情况下的表现。对于平均情况，`Insertion Sort`的复杂度高达`O(N²)`，而`Quicksort`则更快，复杂度为`O(N log N)`。

由于`Quicksort`在平均情况下的优越性，许多编程语言在其内置排序函数的底层使用`Quicksort`。所以你不太可能自己实现`Quicksort`。然而，一种非常相似的算法在实际案例中可以派上用场——它被称为`Quickselect`。
