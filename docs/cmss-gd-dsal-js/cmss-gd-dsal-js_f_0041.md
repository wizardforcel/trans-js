## `冒泡排序`

不过，在进入我们的实际问题之前，我们需要首先看看`Big O`世界中算法效率的新类别。为了说明这一点，我们将使用计算机科学经典算法之一。

排序算法在计算机科学中一直是广泛研究的主题，多年来开发了数十种此类算法。它们都解决了以下问题：

给定一个未排序值的数组，我们如何对其进行排序，使其按升序排列？

在本章及随后的章节中，我们将遇到许多这些排序算法。您将首先学习到的一些算法被称为简单排序，因为它们易于理解，但不如一些更快速的排序算法高效。

`冒泡排序`遵循以下步骤：

1.  指向数组中的两个连续值。（最初，我们开始时指向数组的前两个值。）将第一个项与第二个项进行比较：

    ![images/speeding_up_your_code_with_big_o/bubble_sort_1.png](images/speeding_up_your_code_with_big_o/bubble_sort_1.png)

1.  如果两个项的顺序错误（换句话说，左侧的值大于右侧的值），则交换它们（如果它们已经是正确顺序，则在此步骤中不做任何操作）：

    ![images/speeding_up_your_code_with_big_o/bubble_sort_2.png](images/speeding_up_your_code_with_big_o/bubble_sort_2.png)![images/speeding_up_your_code_with_big_o/bubble_sort_3.png](images/speeding_up_your_code_with_big_o/bubble_sort_3.png)

1.  将“指针”向右移动一个单元：

    ![images/speeding_up_your_code_with_big_o/bubble_sort_4.png](images/speeding_up_your_code_with_big_o/bubble_sort_4.png)

1.  重复`步骤 1 到 3`，直到到达数组的末尾，或遇到已经排序的值。（在随后的逐步演示中，这会更加清晰。）此时，我们已经完成了对数组的第一次遍历——我们通过指向每个值来“遍历”数组，直到到达末尾。

1.  然后，我们将两个指针移动回数组的前两个值，并再次执行数组的遍历，运行`步骤 1 到 4`。我们继续执行这些遍历，直到有一次遍历中没有进行任何交换。当这种情况发生时，意味着我们的数组已经完全排序，工作完成。
