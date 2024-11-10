## `选择排序`的实际操作

让我们通过示例数组`[4, 2, 7, 1, 3]`来逐步演示`选择排序`：

我们开始第一次遍历：

我们通过检查索引`0`的值来进行设置。根据定义，它是我们迄今为止遇到的数组中的最低值（因为它是我们遇到的唯一值），所以我们在一个变量中跟踪它的索引：

![`images/optimizing_code_with_and_without_big_o/selection_sort_1.png`](images/optimizing_code_with_and_without_big_o/selection_sort_1.png)

步骤`1`：我们将`2`与目前为止的最低值（恰好是`4`）进行比较：

![`images/optimizing_code_with_and_without_big_o/selection_sort_2.png`](images/optimizing_code_with_and_without_big_o/selection_sort_2.png)

`2`的值甚至小于`4`，因此它成为目前为止的最低值：

![`images/optimizing_code_with_and_without_big_o/selection_sort_3.png`](images/optimizing_code_with_and_without_big_o/selection_sort_3.png)

步骤`2`：我们将下一个值`7`与目前为止的最低值进行比较。`7`大于`2`，因此`2`仍然是我们的最低值：

![`images/optimizing_code_with_and_without_big_o/selection_sort_4.png`](images/optimizing_code_with_and_without_big_o/selection_sort_4.png)

步骤`3`：我们将`1`与目前为止的最低值进行比较：

![`images/optimizing_code_with_and_without_big_o/selection_sort_5.png`](images/optimizing_code_with_and_without_big_o/selection_sort_5.png)

因为`1`甚至小于`2`，所以`1`成为我们新的最低值：

![`images/optimizing_code_with_and_without_big_o/selection_sort_6.png`](images/optimizing_code_with_and_without_big_o/selection_sort_6.png)

步骤`4`：我们将`3`与目前为止的最低值`1`进行比较。我们已经到达数组的末尾，确认`1`是整个数组中的最低值：

![`images/optimizing_code_with_and_without_big_o/selection_sort_7.png`](images/optimizing_code_with_and_without_big_o/selection_sort_7.png)

步骤`5`：因为`1`是最低值，我们将其与索引`0`的值进行交换——这是我们开始此次遍历时的索引：

![`images/optimizing_code_with_and_without_big_o/selection_sort_8.png`](images/optimizing_code_with_and_without_big_o/selection_sort_8.png)

由于我们已将最低值移动到数组的开头，这意味着最低值现在在正确的位置：

![`images/optimizing_code_with_and_without_big_o/selection_sort_9.png`](images/optimizing_code_with_and_without_big_o/selection_sort_9.png)

我们现在准备开始第二次遍历。

设置：第一个单元——索引`0`——已经排序，因此此次遍历从下一个单元开始，即索引`1`。索引`1`的值是数字`2`，而且它是我们在此次遍历中遇到的最低值：

![`images/optimizing_code_with_and_without_big_o/selection_sort_10.png`](images/optimizing_code_with_and_without_big_o/selection_sort_10.png)

第`6`步：我们将`7`与目前为止的最低值进行比较。`2`小于`7`，因此`2`仍然是我们的最低值：

![images/optimizing_code_with_and_without_big_o/selection_sort_11.png](images/optimizing_code_with_and_without_big_o/selection_sort_11.png)

第7步：我们将`4`与目前为止的最低值进行比较。`2`小于`4`，因此`2`仍然是我们最低的值：

![images/optimizing_code_with_and_without_big_o/selection_sort_12.png](images/optimizing_code_with_and_without_big_o/selection_sort_12.png)

第8步：我们将`3`与目前为止的最低值进行比较。`2`小于`3`，因此`2`仍然是我们目前的最低值：

![images/optimizing_code_with_and_without_big_o/selection_sort_13.png](images/optimizing_code_with_and_without_big_o/selection_sort_13.png)

我们已到达数组的末尾。由于这一轮中最低的值已经在正确的位置，我们无需进行交换。这结束了我们的第二次遍历，结果如下：

![images/optimizing_code_with_and_without_big_o/selection_sort_14.png](images/optimizing_code_with_and_without_big_o/selection_sort_14.png)

现在我们开始第三次遍历。

设置：我们从索引`2`开始，该位置包含值`7`。`7`是我们在这次遍历中遇到的最低值：

![images/optimizing_code_with_and_without_big_o/selection_sort_15.png](images/optimizing_code_with_and_without_big_o/selection_sort_15.png)

第9步：我们将`4`与`7`进行比较：

![images/optimizing_code_with_and_without_big_o/selection_sort_16.png](images/optimizing_code_with_and_without_big_o/selection_sort_16.png)

我们注意到`4`是我们新的最低值：

![images/optimizing_code_with_and_without_big_o/selection_sort_17.png](images/optimizing_code_with_and_without_big_o/selection_sort_17.png)

第10步：我们遇到了`3`，它比`4`还要小：

![images/optimizing_code_with_and_without_big_o/selection_sort_18.png](images/optimizing_code_with_and_without_big_o/selection_sort_18.png)

`3`成为我们新的最低值：

![images/optimizing_code_with_and_without_big_o/selection_sort_19.png](images/optimizing_code_with_and_without_big_o/selection_sort_19.png)

第11步：我们已到达数组的末尾，因此我们将`3`与开始遍历时的值`7`进行交换：

![images/optimizing_code_with_and_without_big_o/selection_sort_20.png](images/optimizing_code_with_and_without_big_o/selection_sort_20.png)

我们现在知道`3`在数组中处于正确的位置：

![images/optimizing_code_with_and_without_big_o/selection_sort_21.png](images/optimizing_code_with_and_without_big_o/selection_sort_21.png)

虽然你我都可以看到此时整个数组已正确排序，但计算机还不知道这一点，因此必须开始第四次遍历。

设置：我们从索引`3`开始遍历。`4`是目前为止的最低值：

![images/optimizing_code_with_and_without_big_o/selection_sort_22.png](images/optimizing_code_with_and_without_big_o/selection_sort_22.png)

第12步：我们将`7`与`4`进行比较：

![`images/optimizing_code_with_and_without_big_o/selection_sort_23.png`](images/optimizing_code_with_and_without_big_o/selection_sort_23.png)

4仍然是我们在这一轮遍历中遇到的最低值，因此我们不需要交换它，因为它已经在正确的位置。

因为除了最后一个单元格外，所有单元格都是正确排序的，这必然意味着最后一个单元格也是按正确顺序排列的，因此我们的整个数组是正确排序的：

![`images/optimizing_code_with_and_without_big_o/selection_sort_24.png`](images/optimizing_code_with_and_without_big_o/selection_sort_24.png)

### 代码实现：选择排序

这是一个JavaScript中选择排序的实现：

| ​  | `function` selectionSort(`array`) { |
| --- | --- |
| ​  | `for` (`let` `i` = 0; `i` < `array.length` - 1; `i` += 1) { |
| ​  | `let` `lowestNumberIndex` = `i`; |
| ​  |  |
| ​  | `for` (`let` `j` = `i` + 1; `j` < `array.length`; `j` += 1) { |
| ​  | `if` (`array[j]` < `array[lowestNumberIndex]`) { |
| ​  | `lowestNumberIndex` = `j`; |
| ​  | } |
| ​  | } |
| ​  |  |
| ​  | `if` (`lowestNumberIndex` !== `i`) { |
| ​  | [`array[i]`, `array[lowestNumberIndex]`] = |
| ​  | [`array[lowestNumberIndex]`, `array[i]`]; |
| ​  | } |
| ​  | } |
| ​  |  |
| ​  | `return` `array`; |
| ​  | } |

让我们逐行分析一下。

我们开始一个循环，表示每次遍历。它使用变量`i`指向数组的每个索引，并一直到倒数第二个值：

| ​  | `for` (`let` `i` = 0; `i` < `array.length` - 1; `i` += 1) { |
| --- | --- |

它不需要对最后一个值本身进行运行，因为到那时数组将完全排序。

接下来，开始跟踪我们遇到的最低值的索引：

| ​  | `let` `lowestNumberIndex` = `i`; |
| --- | --- |

这个`lowestNumberIndex`在第一次遍历开始时为0，在第二次遍历开始时为1，依此类推。

我们特别跟踪索引的原因是因为我们需要在其余代码中同时访问最低值及其索引，并且可以使用该索引引用两者。（我们可以通过调用`array[lowestNumberIndex]`来检查最低值）。

在每一次遍历中，我们检查数组中剩余的值，以查看是否可能存在比当前最低值更低的值：

| ​  | `for` (`let` `j` = `i` + 1; `j` < `array.length`; `j` += 1) { |
| --- | --- |

的确，如果我们找到一个更低的值，我们就把这个新值的索引存储在`lowestNumberIndex`中：

| ​  | `if` (`array[j]` < `array[lowestNumberIndex]`) { |
| --- | --- |
| ​  | `lowestNumberIndex` = `j`; |
| ​  | } |

到了内循环结束时，我们将找到这一轮遍历中最低数字的索引。

如果在这一轮遍历中，最低值已经在其正确的位置（当最低值是我们在遍历中遇到的第一个值时会发生这种情况），我们就不需要做任何事情。但如果最低值不在其正确的位置，我们需要进行交换。具体来说，我们将最低值与索引为`i`的值交换，`i`是我们开始遍历时的索引：

| ​  | `if` (lowestNumberIndex !== i) { |
| --- | --- |
| ​  | `[array[i], array[lowestNumberIndex]] = [array[lowestNumberIndex], array[i]];` |
| ​  | `}` |

最后，我们返回已排序的数组：

| ​  | `return` array; |
| --- | --- |
