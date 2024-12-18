## `Binary Search Trees`的实际应用

我们已经看到`binary search trees`在搜索、插入和删除方面的效率为`O(log N)`，使其成为存储和操作有序数据时的高效选择。这一点尤其适用，如果我们会频繁修改数据，因为虽然`ordered arrays`在搜索数据时与`binary search trees`同样快速，但在插入和删除数据时，`binary search trees`则显著更快。

例如，假设我们正在创建一个维护书籍标题列表的应用。我们希望我们的应用具备以下功能：

+   我们的程序应该能够按字母顺序打印书籍标题列表。

+   我们的程序应该允许列表进行持续的更改。

+   我们的程序应该允许用户在列表中搜索标题。

如果我们没有预见到我们的书单会频繁更改，`ordered array`将是一个合适的数据结构来存储我们的数据。然而，我们正在构建一个应该能够实时处理许多变化的应用。如果我们的列表有数百万个标题，`binary search tree`可能是一个更好的选择。

这样的树可能看起来像这样：

![images/binary_trees/bst_26.png](images/binary_trees/bst_26.png)

在这里，标题是根据它们的字母顺序进行排列的。字母顺序中较早出现的标题被视为“较低”的值，而较晚出现的标题则是“较高”的值。
