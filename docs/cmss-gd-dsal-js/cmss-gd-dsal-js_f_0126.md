## `Quickselect`

假设你有一个随机顺序的数组，而你并不需要对其进行排序，但你想知道数组中的第十小值或第五大值。如果我们有很多测试成绩，并想知道第25百分位数，或者想找到中位数，这将会很有用。

解决这个问题的一种方法是对整个数组进行排序，然后跳到适当的索引。

然而，即使我们使用像`Quicksort`这样的快速排序算法，该算法在平均情况下也至少需要`O(N log N)`的时间。虽然这并不算坏，但我们可以使用一个称为`Quickselect`的出色小算法做得更好。与`Quicksort`一样，`Quickselect`依赖于分区，并可以看作是`Quicksort`和`binary search`的混合。

正如你在本章之前看到的，经过分区后，枢轴值会出现在数组中的适当位置。`Quickselect`利用这一点的方式如下：

假设我们有一个包含八个值的数组，而我们想要找到数组中的第二小值。

首先，我们对整个数组进行分区：

![images/divide_and_conquer_code_in_turbo_mode/partition_entire_array.png](images/divide_and_conquer_code_in_turbo_mode/partition_entire_array.png)

在分区后，枢轴希望出现在数组的中间位置：

![images/divide_and_conquer_code_in_turbo_mode/pivot_in_middle.png](images/divide_and_conquer_code_in_turbo_mode/pivot_in_middle.png)

这个枢轴现在在其正确的位置上，由于它在第五个单元格中，我们现在知道哪个值是数组中的第五小值。

现在，我们要找的是第二小的值，而不是第五小的值。但我们知道，第二小的值在枢轴的左侧。我们现在可以忽略枢轴右侧的所有内容，专注于左侧的子数组。就这一点而言，`Quickselect`与`binary search`类似：我们不断将数组对半分，并专注于我们知道会找到所需值的那一半。

接下来，我们对枢轴左侧的子数组进行分区：

![images/divide_and_conquer_code_in_turbo_mode/subarray_left_of_pivot.png](images/divide_and_conquer_code_in_turbo_mode/subarray_left_of_pivot.png)

假设这个子数组的新枢轴恰好是第三个单元格：

![images/divide_and_conquer_code_in_turbo_mode/pivot_third_cell.png](images/divide_and_conquer_code_in_turbo_mode/pivot_third_cell.png)

我们现在知道第三个单元格中的值在其正确的位置上，这意味着它是数组中的第三小值。根据定义，第二小的值将位于它的左侧。我们现在可以对第三个单元格左侧的子数组进行分区：

![images/divide_and_conquer_code_in_turbo_mode/partition_left_of_third_cell.png](images/divide_and_conquer_code_in_turbo_mode/partition_left_of_third_cell.png)

在下一个分区后，最低和第二低的值将出现在数组中的正确位置：

![images/divide_and_conquer_code_in_turbo_mode/second_lowest_value.png](images/divide_and_conquer_code_in_turbo_mode/second_lowest_value.png)

我们可以从第二个单元格中获取值，并有信心地知道它是整个数组中的第二小值。Quickselect的一个美妙之处在于，我们可以在不对整个数组进行排序的情况下找到正确的值。

与Quicksort相比，每次我们将数组对半时，需要重新分区每个元素（以其子数组形式），这使得时间复杂度为O(N log N)。而在Quickselect中，每次我们将数组对半时，只需分区我们关心的那一半——我们知道值所在的那一半。

### Quickselect的效率

在分析Quickselect的效率时，我们会发现其在平均情况下的时间复杂度为O(N)。这是为什么呢？

在我们之前提到的包含八个元素的数组示例中，我们执行了三次分区：一次在包含八个元素的数组上，一次在包含四个元素的子数组上，以及一次在包含两个元素的子数组上。

请回忆一下，每次分区在它运行的子数组上大约需要N步。那么，对于这三次分区，总步数为8 + 4 + 2 = 14步。所以，八个元素的数组大约需要14步。

对于包含64个元素的数组，我们大约需要64 + 32 + 16 + 8 + 4 + 2 = 126步。对于128个元素，我们大约需要254步。对于256个元素，我们将最终需要510步。

我们可以看到，对于数组中的N个元素，我们大约需要2N步。

（另一种表达方式是，对于N个元素，我们需要N + (N/2) + (N/4) + (N/8) + … 2步。这总是大约是2N步。）

由于大O表示法忽略常数，我们去掉2并说Quickselect的效率为O(N)。

### `代码实现：Quickselect`

以下是一个可以直接放入之前描述的`SortableArray`类中的quickselect方法的实现。你会注意到它与quicksort方法非常相似：

| ​  | quickselect(kthLowestValue, leftIndex, rightIndex) { |
| --- | --- |
| ​  | `如果` (rightIndex - leftIndex <= 0) { |
| ​  | `返回` `this`.array[leftIndex]; |
| ​  | } |
| ​  |  |
| ​  | `const` pivotIndex = `this`.partition(leftIndex, rightIndex); |
| ​  |  |
| ​  | `如果` (kthLowestValue < pivotIndex) { |
| ​  | `返回` `this`.quickselect(kthLowestValue, leftIndex, pivotIndex - 1); |
| ​  | } `否则` `如果` (kthLowestValue > pivotIndex) { |
| ​  | `返回` `this`.quickselect(kthLowestValue, pivotIndex + 1, rightIndex); |
| ​  | } `否则`​ { |
| ​  | `返回` `this`.array[pivotIndex]; |
| ​  | } |
| ​  | } |

变量`kthLowestValue`允许我们选择要搜索的值。我们可以搜索第二小的值、第五小的值，或者我们想要的任何其他值。

如果你想找到一个未排序数组的第二小值，你可以运行以下代码：

| ​  | `const` array = [0, 50, 20, 10, 60, 30]; |
| --- | --- |
| ​  | `const` sortableArray = `new` SortableArray(array); |
| ​  | `console.log(sortableArray.quickselect(1, 0, array.length - 1));` |

`quickselect`方法的第一个参数接受您要查找的位置，从索引`0`开始。我们输入`1`以表示第二小的值。第二个和第三个值分别是数组的左索引和右索引。
