## `Insertion Sort`

我们之前遇到过两种不同的排序算法：`Bubble Sort`和`Selection Sort`。它们的效率都是`O(N²)`，但`Selection Sort`实际上是两倍于`Bubble Sort`的速度。现在你将学习第三种排序算法，称为`Insertion Sort`，它将揭示分析场景超越最坏情况的力量。

`Insertion Sort`由以下步骤组成：

1.  在第一次遍历中，我们暂时移除索引1（第二个单元格）处的值，并将其存储在一个临时变量中。这将在该索引处留下一个间隙，因为它没有值：

    ![`images/optimizing_for_optimistic_scenarios/insertion_sort_1.png`](images/optimizing_for_optimistic_scenarios/insertion_sort_1.png)![`images/optimizing_for_optimistic_scenarios/insertion_sort_2.png`](images/optimizing_for_optimistic_scenarios/insertion_sort_2.png)

    在后续的遍历中，我们移除后续索引处的值。

1.  接着我们开始一个移动阶段，在这个阶段我们将间隙左侧的每个值与临时变量中的值进行比较：

    ![`images/optimizing_for_optimistic_scenarios/insertion_sort_3.png`](images/optimizing_for_optimistic_scenarios/insertion_sort_3.png)

    如果间隙左侧的值大于临时变量，我们将该值向右移动：

    ![`images/optimizing_for_optimistic_scenarios/insertion_sort_4.png`](images/optimizing_for_optimistic_scenarios/insertion_sort_4.png)

    当我们将值向右移动时，间隙会向左移动。一旦我们遇到一个小于临时移除值的值，或者到达数组的左端，这个移动阶段就结束了。

1.  然后我们将临时移除的值插入到当前的间隙中：

    ![`images/optimizing_for_optimistic_scenarios/insertion_sort_5.png`](images/optimizing_for_optimistic_scenarios/insertion_sort_5.png)

1.  第1到第3步代表一次完整的遍历。我们重复这些遍历，直到遍历开始于数组的最后一个索引。到那时，数组将被完全排序。
