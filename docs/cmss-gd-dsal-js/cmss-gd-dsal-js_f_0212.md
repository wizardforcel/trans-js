## 第7章

这些是位于`[练习](f_0075.xhtml#big.o.in.everyday.code.exercises)`部分的习题解决方案。

1.  在这里，`N`是数组的大小。我们的循环运行`N / 2`次，因为每轮循环处理两个值。然而，这被表示为`O(N)`，因为我们忽略了常数。

1.  在这种情况下定义`N`稍微有些棘手，因为我们处理的是两个不同的数组。算法仅处理每个值一次，因此我们可以决定将`N`称为两个数组之间的值的总数，时间复杂度将为`O(N)`。如果我们想更字面地理解，将一个数组称为`N`，另一个称为`M`，我们可以将效率表达为`O(N + M)`。然而，由于我们只是将`N`和`M`相加，因此更简单的做法是直接用`N`来指代两个数组中的数据元素总数，并称之为`O(N)`。

1.  在最坏的情况下，这个算法的运行次数（大约）等于`needle`中的字符数乘以`haystack`中的字符数。想象一下，我们正在搜索`needle` `ab`在`haystack` `aaaaaaaaaaab`中。每当我们的外循环到达一个新的`a`时，我们就会运行一个内循环来查找`ab`。

    因为`needle`和`haystack`可能有不同的字符数量，所以这是`O(N * M)`。

1.  `N`是数组的大小，时间复杂度为`O(N³)`，因为它通过三重嵌套循环处理。实际上，中间循环运行`N / 2`次，最内层循环运行`N / 4`次，因此这是`N * (N / 2) * (N / 4)`，结果是`N³ / 8`步。但我们忽略了常数，最终得到`O(N³)`。

1.  `N`是简历数组的大小。由于在每轮循环中我们消除一半的简历，因此我们有一个`O(log N)`的算法。
