## `快速排序`

`快速排序`算法是分区和递归的组合。它的工作方式如下：

1.  分区数组。枢轴现在在它的正确位置。

1.  将枢轴左侧和右侧的子数组视为各自的数组，并递归重复步骤1和2。这意味着我们将对每个子数组进行分区，并最终得到每个子数组枢轴左侧和右侧的更小的子子数组。然后我们对这些子子数组进行分区，以此类推。

1.  当我们有一个包含零个或一个元素的子数组时，这就是我们的基例，我们什么都不做。

让我们回到我们的例子。我们从数组`[0, 5, 2, 1, 6, 3]`开始，并在整个数组上运行一次分区。由于`快速排序`以这样的分区开始，这意味着我们已经部分完成了`快速排序`过程。以下是我们停下的地方：

![images/divide_and_conquer_code_in_turbo_mode/quicksort_11.png](images/divide_and_conquer_code_in_turbo_mode/quicksort_11.png)

正如你所看到的，值`3`是原始枢轴。现在枢轴在正确的位置，我们需要对枢轴左侧和右侧的内容进行排序。请注意，在我们的例子中，枢轴左侧的数字恰好已经排序，但计算机还不知道这一点。

在分区之后的下一步是将枢轴左侧的所有元素视为自己的数组并进行分区。

我们暂时遮住数组的其余部分，因为我们此时不关注它：

![images/divide_and_conquer_code_in_turbo_mode/quicksort_12.png](images/divide_and_conquer_code_in_turbo_mode/quicksort_12.png)

现在，在这个`[0, 1, 2]`子数组中，我们将最右边的元素作为枢轴。所以这将是数字`2`：

![images/divide_and_conquer_code_in_turbo_mode/quicksort_13.png](images/divide_and_conquer_code_in_turbo_mode/quicksort_13.png)

我们将建立我们的左指针和右指针：

![images/divide_and_conquer_code_in_turbo_mode/quicksort_14.png](images/divide_and_conquer_code_in_turbo_mode/quicksort_14.png)

现在我们准备对这个子数组进行分区。让我们从第8步继续，我们在这里停下了。

第9步：我们将左指针（`0`）与枢轴（`2`）进行比较。由于`0`小于枢轴，我们继续移动左指针。

第10步：我们将左指针向右移动一个单元，现在它恰好指向右指针指向的同一值：

![images/divide_and_conquer_code_in_turbo_mode/quicksort_15.png](images/divide_and_conquer_code_in_turbo_mode/quicksort_15.png)

我们将左指针与枢轴进行比较。由于值`1`小于枢轴，我们继续前进。

第11步：我们将左指针向右移动一个单元，这恰好是枢轴：

![images/divide_and_conquer_code_in_turbo_mode/quicksort_16.png](images/divide_and_conquer_code_in_turbo_mode/quicksort_16.png)

此时，左指针指向的值等于枢轴（因为它就是枢轴！），所以左指针停止。

注意左指针是如何巧妙地超过右指针的。不过没关系，这个算法设计得即使出现这种情况也能正常工作。

`第12步`：现在我们激活右指针。然而，由于右指针的值（`1`）小于枢轴，它保持不动。

由于我们的左指针已经超过了右指针，我们在这个分区中不再移动指针。

`第13步`：接下来，我们将枢轴与左指针的值交换。现在，左指针正好指向枢轴本身，所以我们将枢轴与自身交换，这导致没有任何变化。此时，分区完成，枢轴（`2`）现在在它的正确位置：

![`images/divide_and_conquer_code_in_turbo_mode/quicksort_17.png`](images/divide_and_conquer_code_in_turbo_mode/quicksort_17.png)

我们现在有一个子数组`[0, 1]`在枢轴（`2`）的左侧，而在其右侧没有子数组。下一步是递归地对枢轴左侧的子数组进行分区，这个子数组也是`[0, 1]`。由于在枢轴的右侧没有任何子数组，因此我们不需要处理它。

因为在下一步我们将专注于子数组`[0, 1]`，所以我们会暂时遮住数组的其余部分，使其看起来像这样：

![`images/divide_and_conquer_code_in_turbo_mode/quicksort_18.png`](images/divide_and_conquer_code_in_turbo_mode/quicksort_18.png)

为了划分子数组`[0, 1]`，我们将最右侧的元素（`1`）作为枢轴。我们该如何放置左指针和右指针呢？左指针指向`0`，而右指针也指向`0`，因为我们总是将右指针放在枢轴左侧一个单元的位置。这给我们带来了：

![`images/divide_and_conquer_code_in_turbo_mode/quicksort_19.png`](images/divide_and_conquer_code_in_turbo_mode/quicksort_19.png)

我们现在准备开始划分。

`步骤 14`：我们将左指针（`0`）与枢轴（`1`）进行比较：

![`images/divide_and_conquer_code_in_turbo_mode/quicksort_19.png`](images/divide_and_conquer_code_in_turbo_mode/quicksort_19.png)

它小于枢轴，因此我们继续前进。

`步骤 15`：我们将左指针向右移动一个单元。它现在指向枢轴：

![`images/divide_and_conquer_code_in_turbo_mode/quicksort_20.png`](images/divide_and_conquer_code_in_turbo_mode/quicksort_20.png)

由于左指针的值（`1`）不低于枢轴（因为它就是枢轴），左指针停止移动。

`步骤 16`：我们将右指针与枢轴进行比较。由于它指向的值小于枢轴，因此我们不再移动它。由于左指针已经超过了右指针，我们在此划分中完成了指针的移动。

`步骤 17`：我们现在将左指针与枢轴交换。同样，在这种情况下，左指针实际上指向枢轴本身，因此交换实际上并没有改变任何东西。枢轴现在位于适当的位置，我们完成了这个划分。

这使我们得到了：

![images/divide_and_conquer_code_in_turbo_mode/quicksort_21.png](images/divide_and_conquer_code_in_turbo_mode/quicksort_21.png)

接下来，我们需要对最近的枢轴左侧的子数组进行划分。在这个例子中，该子数组是`[0]`——一个只有一个元素的数组。零个或一个元素的数组是我们的基本情况，因此我们不做任何操作。该元素会自动被认为在其适当的位置上。所以现在我们得到了这个：

![images/divide_and_conquer_code_in_turbo_mode/quicksort_22.png](images/divide_and_conquer_code_in_turbo_mode/quicksort_22.png)

我们开始时将`3`视为我们的枢轴，并递归地划分其左侧的子数组`[0, 1, 2]`。正如承诺的那样，我们现在需要回到递归划分`3`右侧的子数组，即`[6, 5]`。

我们将遮蔽`[0, 1, 2, 3]`，因为我们已经对这些进行了排序，现在我们只关注`[6, 5]`：

![images/divide_and_conquer_code_in_turbo_mode/quicksort_23.png](images/divide_and_conquer_code_in_turbo_mode/quicksort_23.png)

在下一个划分中，我们将最右侧的元素（`5`）视为枢轴。这样我们得到了：

![images/divide_and_conquer_code_in_turbo_mode/quicksort_24.png](images/divide_and_conquer_code_in_turbo_mode/quicksort_24.png)

在设置下一个划分时，我们的左指针和右指针都指向`6`：

![images/divide_and_conquer_code_in_turbo_mode/quicksort_25.png](images/divide_and_conquer_code_in_turbo_mode/quicksort_25.png)

第18步：我们将左指针（`6`）与枢轴（`5`）进行比较。由于`6`大于枢轴，左指针不再移动。

第19步：右指针也指向`6`，因此我们理论上会移动到左侧的下一个单元格。然而，`6`左侧没有更多单元格，因此右指针停止移动。由于左指针已经到达右指针，我们在这个划分上不再移动指针。这意味着我们准备进行最后一步。

第20步：我们将枢轴与左指针的值进行交换：

![images/divide_and_conquer_code_in_turbo_mode/quicksort_26.png](images/divide_and_conquer_code_in_turbo_mode/quicksort_26.png)

我们的枢轴（`5`）现在在正确的位置，留下的是：

![images/divide_and_conquer_code_in_turbo_mode/quicksort_27.png](images/divide_and_conquer_code_in_turbo_mode/quicksort_27.png)

接下来，我们技术上需要递归地划分`[5, 6]`子数组的左侧和右侧。由于左侧没有子数组，这意味着我们只需划分右侧的子数组。由于`5`右侧的子数组是单个元素`[6]`，这就是我们的基例，我们不需要做任何操作——`6`自动被认为在它的正确位置：

![images/divide_and_conquer_code_in_turbo_mode/quicksort_28.png](images/divide_and_conquer_code_in_turbo_mode/quicksort_28.png)

然后我们完成了！

### 代码实现：快速排序

以下是我们可以添加到之前的`SortableArray`类中的一个`quicksort`方法，它能够成功完成快速排序：

| ​  | `quicksort(leftIndex, rightIndex)` { |
| --- | --- |
| ​  | ​`if`​ (`rightIndex - leftIndex <= 0`) { |
| ​  | ​`return`​; |
| ​  | } |
| ​  |  |
| ​  | ​`const`​ `pivotIndex` = ​`this`​.partition(`leftIndex`, `rightIndex`); |
| ​  |  |
| ​  | ​`this`​.quicksort(`leftIndex`, `pivotIndex - 1`); |
| ​  |  |
| ​  | ​`this`​.quicksort(`pivotIndex + 1`, `rightIndex`); |
| ​  | } |

这里的代码令人惊讶地简洁，但让我们看一下每一行。目前，我们将跳过表示基例的第一行代码，直接跳到关键的递归部分。

我们通过划分`leftIndex`和`rightIndex`之间的元素范围开始：

| ​  | ​`const`​ `pivotIndex` = ​`this`​.partition(`leftIndex`, `rightIndex`); |
| --- | --- |

第一次运行`quicksort`时，我们划分整个数组。然而，在后续调用中，这行代码划分`leftIndex`和`rightIndex`之间的任何元素范围，这可能是原始数组的一个子部分。

请注意，我们将`partition`的返回值赋给一个名为`pivotIndex`的变量。如果你还记得，这个值在`partition`方法完成时是指向枢轴的`leftPointer`。

然后我们在枢轴左侧和右侧的子数组上递归调用`quicksort`：

| ​  | ​`this`​.quicksort(`leftIndex`, `pivotIndex - 1`); |
| --- | --- |
| ​  | ​`this`​.quicksort(`pivotIndex + 1`, `rightIndex`); |

当我们达到基例时递归结束，即当前子数组包含不超过一个元素：

| ​  | ​`if`​ (`rightIndex - leftIndex <= 0`) { |
| --- | --- |
| ​  | ​`return`​; |
| ​  | } |

我们可以使用以下代码对我们的`Quicksort`实现进行测试：

| ​  | ​`const`​ `array` = `[0, 5, 2, 1, 6, 3]`; |
| --- | --- |
| ​  | ​`const`​ `sortableArray` = ​`new`​ `SortableArray`(`array`); |
| ​  | `sortableArray.quicksort(0, array.length - 1);` |
| ​  | `console.log(sortableArray.array);` |
