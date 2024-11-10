## 插入排序的实际操作

让我们对数组 `[4, 2, 7, 1, 3]` 应用插入排序。

我们通过检查索引 `1` 处的值开始第一次遍历。这个值恰好是 `2`：

`![images/optimizing_for_optimistic_scenarios/insertion_sort_6.png](images/optimizing_for_optimistic_scenarios/insertion_sort_6.png)`

第 1 步：我们暂时移除 `2` 并将其保存在一个名为 `tempValue` 的变量中。我们通过将其移动到数组的其他值上方来表示这个值：

`![images/optimizing_for_optimistic_scenarios/insertion_sort_7.png](images/optimizing_for_optimistic_scenarios/insertion_sort_7.png)`

第 2 步：我们将 `4` 与 `tempValue` 进行比较，`tempValue` 为 `2`：

`![images/optimizing_for_optimistic_scenarios/insertion_sort_8.png](images/optimizing_for_optimistic_scenarios/insertion_sort_8.png)`

第 3 步：因为 `4` 大于 `2`，我们将 `4` 向右移动：

`![images/optimizing_for_optimistic_scenarios/insertion_sort_9.png](images/optimizing_for_optimistic_scenarios/insertion_sort_9.png)`

没有剩下的值可以移动，因为空位现在在数组的左端。

第 4 步：我们将 `tempValue` 插入空位，完成第一次遍历：

`![images/optimizing_for_optimistic_scenarios/step_4.png](images/optimizing_for_optimistic_scenarios/step_4.png)`

接下来，我们开始第二次遍历：

第 5 步：在我们的第二次遍历中，我们暂时移除索引 `2` 处的值。我们将其存储在 `tempValue` 中。在这种情况下，`tempValue` 为 `7`：

`![images/optimizing_for_optimistic_scenarios/insertion_sort_12.png](images/optimizing_for_optimistic_scenarios/insertion_sort_12.png)`

第 6 步：我们将 `4` 与 `tempValue` 进行比较：

`![images/optimizing_for_optimistic_scenarios/insertion_sort_13.png](images/optimizing_for_optimistic_scenarios/insertion_sort_13.png)`

`4` 较小，因此我们不会移动它。因为我们到达了一个小于 `tempValue` 的值，这个移动阶段结束了。

第 7 步：我们将 `tempValue` 插入空位，结束第二次遍历：

`![images/optimizing_for_optimistic_scenarios/insertion_sort_14.png](images/optimizing_for_optimistic_scenarios/insertion_sort_14.png)`

现在我们开始第三次遍历：

第 8 步：我们暂时移除 `1` 并将其存储在 `tempValue` 中：

`![images/optimizing_for_optimistic_scenarios/insertion_sort_16.png](images/optimizing_for_optimistic_scenarios/insertion_sort_16.png)`

第 9 步：我们将 `7` 与 `tempValue` 进行比较：

`![images/optimizing_for_optimistic_scenarios/insertion_sort_17.png](images/optimizing_for_optimistic_scenarios/insertion_sort_17.png)`

第 10 步：`7` 大于 `1`，所以我们将 `7` 向右移动：

`![images/optimizing_for_optimistic_scenarios/insertion_sort_18.png](images/optimizing_for_optimistic_scenarios/insertion_sort_18.png)`

第 11 步：我们将 `4` 与 `tempValue` 进行比较：

`![images/optimizing_for_optimistic_scenarios/insertion_sort_19.png](images/optimizing_for_optimistic_scenarios/insertion_sort_19.png)`

第12步：`4`大于`1`，所以我们也将其移动：

![images/optimizing_for_optimistic_scenarios/insertion_sort_20.png](images/optimizing_for_optimistic_scenarios/insertion_sort_20.png)

第13步：我们将2与`tempValue`进行比较：

![images/optimizing_for_optimistic_scenarios/insertion_sort_21.png](images/optimizing_for_optimistic_scenarios/insertion_sort_21.png)

第14步：2更大，因此我们将其移动：

![images/optimizing_for_optimistic_scenarios/insertion_sort_22.png](images/optimizing_for_optimistic_scenarios/insertion_sort_22.png)

第15步：空隙已到达数组的左端，因此我们将`tempValue`插入到空隙中，结束此次遍历：

![images/optimizing_for_optimistic_scenarios/step_15.png](images/optimizing_for_optimistic_scenarios/step_15.png)

现在，我们开始第四次遍历：

第16步：我们暂时从索引4中移除该值，使其成为我们的`tempValue`。这个值是3：

![images/optimizing_for_optimistic_scenarios/insertion_sort_24.png](images/optimizing_for_optimistic_scenarios/insertion_sort_24.png)

第17步：我们将7与`tempValue`进行比较：

![images/optimizing_for_optimistic_scenarios/insertion_sort_25.png](images/optimizing_for_optimistic_scenarios/insertion_sort_25.png)

第18步：7更大，因此我们将7向右移动：

![images/optimizing_for_optimistic_scenarios/insertion_sort_26.png](images/optimizing_for_optimistic_scenarios/insertion_sort_26.png)

第19步：我们将4与`tempValue`进行比较：

![images/optimizing_for_optimistic_scenarios/insertion_sort_27.png](images/optimizing_for_optimistic_scenarios/insertion_sort_27.png)

第20步：4大于3，因此我们将4移动：

![images/optimizing_for_optimistic_scenarios/insertion_sort_28.png](images/optimizing_for_optimistic_scenarios/insertion_sort_28.png)

第21步：我们将2与`tempValue`进行比较。2小于3，因此我们的移动阶段完成：

![images/optimizing_for_optimistic_scenarios/insertion_sort_29.png](images/optimizing_for_optimistic_scenarios/insertion_sort_29.png)

第22步：我们将`tempValue`插入到空隙中：

![images/optimizing_for_optimistic_scenarios/step_22.png](images/optimizing_for_optimistic_scenarios/step_22.png)

我们的数组现在已完全排序：

![images/optimizing_for_optimistic_scenarios/insertion_sort_31.png](images/optimizing_for_optimistic_scenarios/insertion_sort_31.png)

### 代码实现：插入排序

这是插入排序的JavaScript实现：

| ​  | ​`function`​ `insertionSort`(array) { |
| --- | --- |
| ​  | ​`for`​ (​`let`​ index = 1; index < array.length; index += 1) { |
| ​  | ​`const`​ `tempValue` = array[index]; |
| ​  | ​`let`​ position = index - 1; |
| ​  |  |
| ​  | ​`while`​ (position >= 0) { |
| ​  | ​`if`​ (array[position] > `tempValue`) { |
| ​  | array[position + 1] = array[position]; |
| ​  | position -= 1; |
| ​  | } ​`else`​ { |
| ​  | ​`break`​; |
| ​  | } |
| ​  | } |
| ​  |  |
| ​  | array[position + 1] = `tempValue` ; |
| ​  | } |
| ​  |  |
| ​  | ​`return`​ array; |
| ​  | } |

让我们一步一步地走过这段代码。

首先，我们从索引`1`开始一个循环，遍历整个数组。这个循环的每一轮代表一次遍历：

| ​  | `for` (`let` `index = 1; index < array.length; index += 1`) { |
| --- | --- |

在每次遍历中，我们将要“移除”的值保存在一个名为`tempValue`的变量中：

| ​  | `const` tempValue = `array[index]`; |
| --- | --- |

接下来，我们创建一个名为`position`的变量，它将立即位于`tempValue`索引的左侧。这个位置将代表我们与`tempValue`进行比较的每个值：

| ​  | `let` `position = index - 1;` |
| --- | --- |

在遍历过程中，这个`position`会随着我们将每个值与`tempValue`进行比较而向左移动。

然后我们开始一个内部的while循环，只要`position`大于或等于`0`，它就会运行：

| ​  | `while` (`position >= 0`) { |
| --- | --- |

然后我们进行比较；也就是说，我们检查`position`处的值是否大于`tempValue`：

| ​  | `if` (`array[position] > tempValue`) { |
| --- | --- |

如果是，我们将该左侧值向右移动：

| ​  | `array[position + 1] = array[position];` |
| --- | --- |

然后我们将`position`减少`1`，以在下一轮循环中将下一个左侧值与`tempValue`进行比较：

| ​  | `position -= 1;` |
| --- | --- |

如果在任何时刻我们遇到`position`处的值小于或等于`tempValue`，我们可以准备结束遍历，因为是时候将`tempValue`移入空缺：

| ​  | } `else` { |
| --- | --- |
| ​  | `break`; |
| ​  | } |

每次遍历的最后一步是将`tempValue`移入空缺：

| ​  | `array[position + 1] = tempValue;` |
| --- | --- |

在所有的遍历完成后，我们返回排序后的数组：

| ​  | `return` `array`; |
| --- | --- |
