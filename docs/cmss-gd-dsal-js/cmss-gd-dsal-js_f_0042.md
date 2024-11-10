## `冒泡排序` 实际运行

让我们完整地演示一次 `冒泡排序`。

假设我们想对数组 `[4, 2, 7, 1, 3]` 进行排序。它目前的顺序不对，我们希望生成一个包含相同值的升序数组。

让我们开始第一次遍历。这是我们的初始数组：

![images/speeding_up_your_code_with_big_o/bubble_sort_5.png](images/speeding_up_your_code_with_big_o/bubble_sort_5.png)

第 1 步：首先，我们比较 4 和 2：

![images/speeding_up_your_code_with_big_o/bubble_sort_6.png](images/speeding_up_your_code_with_big_o/bubble_sort_6.png)

第 2 步：它们的顺序不对，所以我们交换它们：

![images/speeding_up_your_code_with_big_o/bubble_sort_7.png](images/speeding_up_your_code_with_big_o/bubble_sort_7.png)![images/speeding_up_your_code_with_big_o/bubble_sort_8.png](images/speeding_up_your_code_with_big_o/bubble_sort_8.png)

第 3 步：接下来，我们比较 4 和 7：

![images/speeding_up_your_code_with_big_o/bubble_sort_9.png](images/speeding_up_your_code_with_big_o/bubble_sort_9.png)

它们的顺序是正确的，所以我们不需要交换。

第 4 步：我们现在比较 7 和 1：

![images/speeding_up_your_code_with_big_o/bubble_sort_10.png](images/speeding_up_your_code_with_big_o/bubble_sort_10.png)

第 5 步：它们的顺序不对，所以我们交换它们：

![images/speeding_up_your_code_with_big_o/bubble_sort_11.png](images/speeding_up_your_code_with_big_o/bubble_sort_11.png)![images/speeding_up_your_code_with_big_o/bubble_sort_12.png](images/speeding_up_your_code_with_big_o/bubble_sort_12.png)

第 6 步：我们比较 7 和 3：

![images/speeding_up_your_code_with_big_o/bubble_sort_13.png](images/speeding_up_your_code_with_big_o/bubble_sort_13.png)

第 7 步：它们的顺序不对，所以我们交换它们：

![images/speeding_up_your_code_with_big_o/bubble_sort_14.png](images/speeding_up_your_code_with_big_o/bubble_sort_14.png)![images/speeding_up_your_code_with_big_o/bubble_sort_15.png](images/speeding_up_your_code_with_big_o/bubble_sort_15.png)

我们现在可以确定 7 在数组中处于正确的位置，因为我们一直将它向右移动，直到它达到合适的位置。前面的图示中有小线条围绕着 7，以表明 7 确实在正确的位置上。

这实际上就是为什么这个算法被称为`冒泡排序`的原因：在每次遍历中，最大的未排序值会“冒泡”到它正确的位置。

因为在这一轮中我们至少进行了一次交换，所以需要再进行一轮遍历。

我们开始第二轮遍历：

第 8 步：我们比较 2 和 4：

![images/speeding_up_your_code_with_big_o/bubble_sort_17.png](images/speeding_up_your_code_with_big_o/bubble_sort_17.png)

它们的顺序是正确的，所以我们可以继续。

第 9 步：我们比较 4 和 1：

![images/speeding_up_your_code_with_big_o/bubble_sort_18.png](images/speeding_up_your_code_with_big_o/bubble_sort_18.png)

第 10 步：它们的顺序不对，所以我们交换它们：

![images/speeding_up_your_code_with_big_o/bubble_sort_19.png](images/speeding_up_your_code_with_big_o/bubble_sort_19.png)![images/speeding_up_your_code_with_big_o/bubble_sort_20.png](images/speeding_up_your_code_with_big_o/bubble_sort_20.png)

步骤11：我们比较4和3：

![images/speeding_up_your_code_with_big_o/step_11.png](images/speeding_up_your_code_with_big_o/step_11.png)

步骤12：它们是错序的，所以我们交换它们：

![images/speeding_up_your_code_with_big_o/bubble_sort_21.png](images/speeding_up_your_code_with_big_o/bubble_sort_21.png)![images/speeding_up_your_code_with_big_o/bubble_sort_22.png](images/speeding_up_your_code_with_big_o/bubble_sort_22.png)

我们不需要比较4和7，因为我们知道7已经在前一次遍历中处于正确的位置。现在我们也知道4已经上升到了正确的位置。这结束了我们的第二次遍历。

因为我们在这次遍历中至少进行了一个交换，我们需要再进行一次遍历。

我们开始第三次遍历：

步骤13：我们比较2和1：

![images/speeding_up_your_code_with_big_o/bubble_sort_23.png](images/speeding_up_your_code_with_big_o/bubble_sort_23.png)

步骤14：它们是错序的，所以我们交换它们：

![images/speeding_up_your_code_with_big_o/bubble_sort_24.png](images/speeding_up_your_code_with_big_o/bubble_sort_24.png)![images/speeding_up_your_code_with_big_o/bubble_sort_24b.png](images/speeding_up_your_code_with_big_o/bubble_sort_24b.png)

步骤15：我们比较2和3：

![images/speeding_up_your_code_with_big_o/bubble_sort_25.png](images/speeding_up_your_code_with_big_o/bubble_sort_25.png)

它们是有序的，所以我们不需要交换。

我们现在知道3已经上升到它的正确位置：

![images/speeding_up_your_code_with_big_o/bubble_sort_26.png](images/speeding_up_your_code_with_big_o/bubble_sort_26.png)

由于我们在这次遍历中至少进行了一个交换，我们需要再进行一次遍历。

于是第四次遍历开始：

步骤16：我们比较1和2：

![images/speeding_up_your_code_with_big_o/bubble_sort_27.png](images/speeding_up_your_code_with_big_o/bubble_sort_27.png)

因为它们是有序的，我们不需要交换。我们可以结束这次遍历，因为所有剩余的值已经正确排序。

现在我们已经进行了不需要任何交换的遍历，我们知道我们的数组已经完全排序：

![images/speeding_up_your_code_with_big_o/bubble_sort_28.png](images/speeding_up_your_code_with_big_o/bubble_sort_28.png)

### 代码实现：冒泡排序

这是一个用JavaScript实现的冒泡排序：

| ​  | `function` bubbleSort(array) { |
| --- | --- |
| ​  | `let` unsortedUntilIndex = array.length - 1; |
| ​  | `let` sorted = `false`; |
| ​  |  |
| ​  | `while` (!sorted) { |
| ​  | sorted = `true`; |
| ​  |  |
| ​  | `for` (`let` i = 0; i < unsortedUntilIndex; i++) { |
| ​  | `if` (array[i] > array[i + 1]) { |
| ​  | [array[i], array[i + 1]] = [array[i + 1], array[i]]; |
| ​  | `sorted` = `false`; |
| ​  | } |
| ​  | } |
| ​  | `unsortedUntilIndex` -= 1; |
| ​  | } |
| ​  |  |
| ​  | `return` array; |
| ​  | } |

要使用这个函数，我们可以将一个未排序的数组传递给它，如下所示：

| ​  | `console.log(bubbleSort([65, 55, 45, 35, 25, 15, 10]));` |
| --- | --- |

这个函数将返回排序后的数组。

让我们逐行分析这个函数，看看它是如何工作的。我将先提供解释，然后给出代码行。

我们首先创建一个名为 `unsortedUntilIndex` 的变量。它跟踪尚未排序的数组的最右索引。当我们首次启动算法时，数组是完全未排序的，因此我们将该变量初始化为数组的最后一个索引：

| ​  | `let` `unsortedUntilIndex` = array.length - 1; |
| --- | --- |

我们还创建了一个名为 `sorted` 的变量，用于跟踪数组是否完全排序。当然，当我们的代码首次运行时，数组并没有排序，所以我们将其设置为 `false`：

| ​  | `let` `sorted` = `false`; |
| --- | --- |

我们开始一个 `while` 循环，只要数组未排序，它就会继续运行。每次循环代表一次对数组的遍历：

| ​  | `while` (!`sorted`) { |
| --- | --- |

接下来，我们初步将 `sorted` 设置为 `true`：

| ​  | `sorted` = `true`; |
| --- | --- |

这里的方法是，在每次遍历中，我们假设数组是已排序的，直到遇到交换，这时我们会将变量改回 `false`。如果我们在一次完整的遍历中没有进行任何交换，`sorted` 将保持为 `true`，我们就知道数组已经完全排序。

在 `while` 循环中，我们开始一个 `for` 循环，指向数组中的每对值。我们使用变量 `i` 作为第一个指针，它从数组的开始处开始，直到尚未排序的索引：

| ​  | `for` (`let` i = 0; i < `unsortedUntilIndex`; i += 1) { |
| --- | --- |

在这个循环中，我们比较每对相邻值，如果它们的顺序不对，就交换这些值。如果我们进行了交换，还会将 `sorted` 改为 `false`：

| ​  | `if` (array[i] > array[i + 1]) { |
| --- | --- |
| ​  | [array[i], array[i + 1]] = [array[i + 1], array[i]]; |
| ​  | `sorted` = `false`; |
| ​  | } |

在每次遍历结束时，我们知道我们冒泡到右边的值现在已在正确的位置。因此，我们将 `unsortedUntilIndex` 减少 1，因为它之前指向的索引现在已排序：

| ​  | `unsortedUntilIndex` -= 1; |
| --- | --- |

`while` 循环在 `sorted` 为 `true` 时结束，这意味着数组已完全排序。一旦满足这个条件，我们返回排序后的数组：

| ​  | `return` array; |
| --- | --- |
