## 前缀树搜索的效率

前缀树搜索的一个好处是它极其高效。

让我们分析一下所需的步骤数量。

在我们的算法中，我们一次关注搜索字符串的每个字符。这样做时，我们使用每个节点的哈希表在一步内找到适当的子节点。如你所知，哈希表查找只需`O(1)`时间。因此，我们的算法所需的步骤数量与搜索字符串中的字符数相同。

这比在有序数组上使用二分搜索要快得多。二分搜索是`O(log N)`，其中`N`是字典中的单词数量。而前缀树搜索则只需与搜索词中的字符数相同的步骤。对于像“cat”这样的单词，仅需三步。

用大O表示前缀树搜索稍显棘手。我们不能完全称其为`O(1)`，因为步骤数量不是常量，完全取决于搜索字符串的长度。而`O(N)`可能会误导，因为`N`通常指的是数据结构中的数据量。这将是前缀树中的节点数量，这远大于搜索字符串中的字符数量。

大多数参考文献决定称其为`O(K)`，其中`K`是我们搜索字符串中的字符数。除了`N`的任何字母在这里都可以，但`K`就是。

尽管`O(K)`并不是常量，因为搜索字符串的大小可能会变化，但在一个重要意义上，`O(K)`类似于常量时间。大多数非恒定算法与手头的数据量有关；也就是说，随着`N`数据的增加，算法会变慢。然而，使用`O(K)`算法时，我们的前缀树可以大幅增长，但这不会影响搜索的速度。对于三个字符的字符串，`O(K)`算法始终需要三步，无论前缀树有多大。影响我们算法速度的唯一因素是输入的大小，而不是所有可用数据的大小。这使得我们的`O(K)`算法极其高效。

尽管搜索是对前缀树执行的最常见操作，但没有填充数据的前缀树，测试它是很困难的，因此我们接下来处理插入。