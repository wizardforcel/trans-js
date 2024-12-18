# 第17章

使用Trie不会造成伤害

你有没有想过你的智能手机的自动补全功能是如何工作的？自动补全是您开始输入`"catn"`时，手机建议您要输入的单词是`"catnip"`或`"catnap"`的功能。（是的，我总是给朋友发关于`catnip`的短信。）

为了使其工作，您的手机可以访问整个单词字典。但这些单词存储在什么数据结构中呢？

让我们想象一下，所有英语单词都存储在一个数组中。如果数组是无序的，我们必须搜索字典中的每个单词，以找到所有以`"catn"`开头的单词。这是`O(N)`，考虑到`N`在这种情况下是一个相当大的数字（因为它是字典中所有单词的数量），这是一项非常慢的操作。

`hash table`对我们也没有帮助，因为它对整个单词进行哈希，以确定值应该存储在内存中的位置。由于`hash table`没有`"catn"`键，我们将没有简单的方法在`hash table`中找到`"catnip"`或`"catnap"`。

如果我们将单词存储在一个有序数组中，情况会大大改善。如果数组包含所有按字母顺序排列的单词，我们可以使用二分查找以`O(log N)`时间找到以`"catn"`开头的单词。虽然`O(log N)`并不算糟糕，但我们可以做得更好。实际上，如果我们使用一种特殊的基于树的数据结构，我们可以以接近`O(1)`的速度找到我们想要的单词。

本章中的示例展示了如何使用`tries`进行处理文本的应用，因为`tries`允许重要的功能，如自动补全和自动纠正。然而，`tries`也有其他用途，包括涉及`IP`地址或电话号码的应用。
