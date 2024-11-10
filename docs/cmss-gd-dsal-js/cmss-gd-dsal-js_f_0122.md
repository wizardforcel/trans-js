## 划分

对数组进行划分就是从数组中选取一个随机值——这个值称为基准值——确保所有小于基准值的数字位于基准值的左侧，而所有大于基准值的数字位于基准值的右侧。我们通过一个简单的算法完成划分，接下来的示例将描述这个算法。

假设我们有以下数组：

![images/divide_and_conquer_code_in_turbo_mode/quicksort_1.png](images/divide_and_conquer_code_in_turbo_mode/quicksort_1.png)

为了一致性，我们将始终选择最右边的值作为我们的基准值（尽管从技术上讲，我们可以选择其他值）。在这种情况下，数字`3`是我们的基准值。我们通过圈出它来表示：

![images/divide_and_conquer_code_in_turbo_mode/quicksort_2.png](images/divide_and_conquer_code_in_turbo_mode/quicksort_2.png)

然后我们分配指针——一个指向数组的最左边的值，另一个指向数组的最右边的值，排除基准值本身：

![images/divide_and_conquer_code_in_turbo_mode/quicksort_3.png](images/divide_and_conquer_code_in_turbo_mode/quicksort_3.png)

我们现在准备开始实际的划分，遵循以下步骤。别担心——这些步骤很快会变得更加清晰，当我们逐步讲解我们的示例时。

1.  左指针不断向右移动一个单元，直到它找到一个大于或等于基准值的值并停止。

1.  然后右指针不断向左移动一个单元，直到它找到一个小于或等于基准值的值并停止。如果右指针到达数组的开头，它也会停止。

1.  一旦右指针停止，我们就到达了一个十字路口。如果左指针已到达（或超出）右指针，我们就进入第4步。否则，我们交换左指针和右指针指向的值，然后回去重复步骤1、2和3。

1.  最后，我们将基准值与左指针当前指向的值交换。

当我们完成一个划分后，我们现在可以确保基准值左侧的所有值都小于基准值，右侧的所有值都大于基准值。这意味着基准值本身现在处于数组中的正确位置，尽管其他值尚未完全排序。

让我们将其应用到我们的示例中：

第1步：将左指针（现在指向`0`）与我们的基准值（值为`3`）进行比较：

![images/divide_and_conquer_code_in_turbo_mode/quicksort_3.png](images/divide_and_conquer_code_in_turbo_mode/quicksort_3.png)

由于`0`小于基准值，左指针在下一步继续移动。

第2步：左指针继续移动：

![images/divide_and_conquer_code_in_turbo_mode/quicksort_4.png](images/divide_and_conquer_code_in_turbo_mode/quicksort_4.png)

我们将左指针（`5`）与基准进行比较。`5`是否低于基准？不，所以左指针停止，并在下一步中激活右指针。

第3步：将右指针（`6`）与我们的基准进行比较。这个值是否大于基准？是的，因此我们的指针将在下一步中继续移动。

第4步：右指针继续移动：

![images/divide_and_conquer_code_in_turbo_mode/quicksort_5.png](images/divide_and_conquer_code_in_turbo_mode/quicksort_5.png)

我们将右指针（`1`）与基准进行比较。这个值是否大于基准？不，所以我们的右指针停止。

第5步：由于两个指针都已停止，我们交换这两个指针的值：

![images/divide_and_conquer_code_in_turbo_mode/quicksort_6.png](images/divide_and_conquer_code_in_turbo_mode/quicksort_6.png)![images/divide_and_conquer_code_in_turbo_mode/quicksort_7.png](images/divide_and_conquer_code_in_turbo_mode/quicksort_7.png)

然后在下一步中再次激活我们的左指针。

第6步：左指针继续移动：

![images/divide_and_conquer_code_in_turbo_mode/quicksort_8.png](images/divide_and_conquer_code_in_turbo_mode/quicksort_8.png)

我们将左指针（`2`）与基准进行比较。这个值是否小于基准？是的，因此左指针继续移动。

第7步：左指针移动到下一个单元格。请注意，此时，左指针和右指针指向相同的值：

![images/divide_and_conquer_code_in_turbo_mode/quicksort_9.png](images/divide_and_conquer_code_in_turbo_mode/quicksort_9.png)

我们将左指针与基准进行比较。由于我们的左指针指向的值大于我们的基准，它停止了。此时，由于左指针已到达右指针，我们不再移动指针。

第8步：在我们的分区的最后一步中，我们将左指针指向的值与基准进行交换：

![images/divide_and_conquer_code_in_turbo_mode/quicksort_10.png](images/divide_and_conquer_code_in_turbo_mode/quicksort_10.png)![images/divide_and_conquer_code_in_turbo_mode/quicksort_11.png](images/divide_and_conquer_code_in_turbo_mode/quicksort_11.png)

虽然我们的数组尚未完全排序，但我们已经成功完成了一次分区；也就是说，由于我们的基准是数字`3`，所有小于`3`的数字都在它的左侧，而所有大于`3`的数字都在它的右侧。这也意味着，根据定义，`3`现在在数组中的正确位置。

### 代码实现：分区

以下是一个在JavaScript中实现的`SortableArray`类，其中包括一个分区方法，按照我们描述的方式对数组进行分区：

| ​  | `class` SortableArray { |
| --- | --- |
| ​  | `constructor`(`array`) { |
| ​  | `this`.array = `array`; |
| ​  | } |
| ​  |  |
| ​  | `partition(leftPointer, rightPointer) {` |
| ​  | `const` pivotIndex = `rightPointer`; |
| ​  | `const` pivot = `this`.array[pivotIndex]; |
| ​  |  |
| ​  | `rightPointer -= 1;` |
| ​  |  |
| ​  | `while` (`true`) { |
| ​  | `while` (`this`.array[`leftPointer`] < `pivot`) { |
| ​  | `leftPointer += 1;` |
| ​  | } |
| ​  |  |
| ​  | `while ([this].array[rightPointer] > pivot) {` |
| ​  | `rightPointer -= 1；` |
| ​  | `}` |
| ​  |  |
| ​  | `if (leftPointer >= rightPointer) {` |
| ​  | `break`； |
| ​  | `} else {` |
| ​  | `[this].array[leftPointer], [this].array[rightPointer]` = |
| ​  | `[this].array[rightPointer], [this].array[leftPointer]`； |
| ​  | `leftPointer += 1；` |
| ​  | `}` |
| ​  | `}` |
| ​  |  |
| ​  | `[this].array[leftPointer], [this].array[pivotIndex]` = |
| ​  | `[this].array[pivotIndex], [this].array[leftPointer]`； |
| ​  |  |
| ​  | `return leftPointer；` |
| ​  | `}` |
| ​  | `}` |

让我们稍微分解一下这段代码。

`partition`方法接受`left`和`right`指针的起始点作为参数：

| ​  | `partition(leftPointer, rightPointer) {` |
| --- | --- |

当此方法第一次在数组上调用时，这些指针将分别指向数组的左端和右端。然而，我们会看到快速排序还会在数组的子部分调用此方法。因此，我们不能总是假设`left`和`right`指针总是数组的两个极端，所以它们需要成为方法参数。等我解释完整的快速排序算法时，这一点会更清晰。

接下来，我们选择我们的基准值，它始终是我们处理范围内最右边的元素：

| ​  | `const pivotIndex = rightPointer；` |
| --- | --- |
| ​  | `const pivot = [this].array[pivotIndex]；` |

一旦我们的基准值被确定，我们将`rightPointer`移动到基准值左侧的元素：

| ​  | `rightPointer -= 1；` |
| --- | --- |

然后我们开始一个循环（`while (true)`），看起来会无限运行。然而，在循环的后面有一个`break`语句，它将在`leftPointer`和`rightPointer`交叉时终止循环。在这个循环中，我们使用另一个循环继续将`leftPointer`向右移动，直到它达到一个大于或等于基准值的元素：

| ​  | `while ([this].array[leftPointer] < pivot) {` |
| --- | --- |
| ​  | `leftPointer += 1；` |
| ​  | `}` |

类似地，我们将`rightPointer`向左移动，直到它碰到一个小于或等于基准值的元素：

| ​  | `while ([this].array[rightPointer] > pivot) {` |
| --- | --- |
| ​  | `rightPointer -= 1；` |
| ​  | `}` |

一旦`leftPointer`和`rightPointer`停止移动，我们检查两个指针是否相遇：

| ​  | `if (leftPointer >= rightPointer) {` |
| --- | --- |
| ​  | `break`； |
| ​  | `}` |

如果指针相遇了，我们就退出循环，准备交换基准值，稍后会详细介绍。然而，如果两个指针停止了但还没有相遇，我们就交换两个指针处的值：

| ​  | `[this].array[leftPointer], [this].array[rightPointer]` = |
| --- | --- |
| ​  | `[this].array[rightPointer], [this].array[leftPointer]`； |

然后我们移动`leftPointer`以准备下一轮的左指针和右指针移动：

| ​  | `leftPointer += 1；` |
| --- | --- |

最后，一旦两个指针相遇，我们将`pivot`与`leftPointer`处的值交换：

| ​  | [`this`.array[`leftPointer`], `this`.array[`pivotIndex`]] = |
| --- | --- |
| ​  | [`this`.array[`pivotIndex`], `this`.array[`leftPointer`]]; |

该方法通过返回`leftPointer`结束，因为这将被`Quicksort`算法所需（我将很快解释）。
