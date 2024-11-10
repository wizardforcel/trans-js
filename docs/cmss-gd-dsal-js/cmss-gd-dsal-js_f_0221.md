## 第16章

这些是[`练习`](f_0165.xhtml#heaps.exercises)部分中找到的习题解答。

1.  插入一个`11`后，堆的结构会如下所示：

    ![`images/heaps/solution_1.png`](images/heaps/solution_1.png)

1.  删除根节点后，堆的结构会如下所示：

    ![`images/heaps/solution_2.png`](images/heaps/solution_2.png)

1.  这些数字将完全按降序排列。（这是针对最大堆的。如果是最小堆，则按升序排列。）

    你意识到这意味着什么吗？这意味着你刚刚发现了另一种排序算法！

    Heapsort是一种排序算法，它将所有值插入堆中，然后逐个弹出。正如你从这个练习中看到的，值总是最终以排序的顺序排列。

    像`Quicksort`一样，`Heapsort`是`O(N log N)`，因为我们需要将`N`个值插入堆中，而每次插入需要`log N`步。

    虽然有一些更复杂的`Heapsort`版本试图最大化其效率，但这就是基本思路。
