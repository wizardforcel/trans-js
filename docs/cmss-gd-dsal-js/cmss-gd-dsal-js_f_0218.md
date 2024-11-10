## -   第 13 章

-   这些是 [`Exercises`](f_0129.xhtml#divide.and.conquer.in.turbo.mode.exercises) 部分中练习的解决方案。

1.  -   如果我们对数字进行排序，我们知道最大的三个数字将在数组的末尾，我们可以直接将它们相乘。排序的时间复杂度为 O(N log N)：

    | ​  | ​`function`​ `greatestProductOf3(array) {` |
    | --- | --- |
    | ​  | `array.sort((a, b) => a - b);` |
    | ​  |  |
    | ​  | ​`return`​ `array[array.length - 1] *` |
    | ​  | `array[array.length - 2] *` |
    | ​  | `array[array.length - 3];` |
    | ​  | } |

    -   （这段代码假设数组中至少有三个值。你可以添加代码来处理不满足这一条件的数组。）

1.  -   如果我们对数组进行预排序，那么我们可以期待每个数字都在其对应的索引上。也就是说，0 应该在索引 0，1 应该在索引 1，依此类推。然后我们可以遍历数组，寻找一个不等于索引的数字。一旦找到，我们就知道跳过了缺失的数字：

    | ​  | ​`function`​ `findMissingNumber(array) {` |
    | --- | --- |
    | ​  | `array.sort((a, b) => a - b);` |
    | ​  |  |
    | ​  | ​`for`​ (​`const`​ `[index, num]` ​`of`​ `array.entries()) {` |
    | ​  | ​`if`​ (`num !== index`) { |
    | ​  | ​`return`​ `index;` |
    | ​  | } |
    | ​  | } |
    | ​  |  |
    | ​  | ​`return`​ ​`null`​; |
    | ​  | } |

    -   排序需要 N log N 步骤，而后面的循环需要 N 步骤。然而，我们将表达式 (N log N) + N 简化为 O(N log N)，因为添加的 N 相较于 N log N 是较低的阶。

1.  -   这个实现使用了嵌套循环，时间复杂度为 O(N²)：

    | ​  | ​`function`​ `max(array) {` |
    | --- | --- |
    | ​  | ​`if`​ (`array.length === 0`) { ​`return`​ ​`null`​; } |
    | ​  |  |
    | ​  | ​`for`​ (​`const`​ `i` ​`of`​ `array`) { |
    | ​  | ​`let`​ `iIsGreatestNumber` = ​`true`​; |
    | ​  |  |
    | ​  | ​`for`​ (​`const`​ `j` ​`of`​ `array`) { |
    | ​  | ​`if`​ (`j > i`) { |
    | ​  | `iIsGreatestNumber` = ​`false`​; |
    | ​  | } |
    | ​  | } |
    | ​  |  |
    | ​  | ​`if`​ (`iIsGreatestNumber`) { |
    | ​  | ​`return`​ `i;` |
    | ​  | } |
    | ​  | } |
    | ​  | } |

    -   下一个实现简单地对数组进行排序并返回最后一个数字。排序的时间复杂度是 O(N log N)：

    | ​  | ​`function`​ `max(array) {` |
    | --- | --- |
    | ​  | ​`if`​ (`array.length === 0`) { ​`return`​ ​`null`​; } |
    | ​  |  |
    | ​  | `array.sort((a, b) => a - b);` |
    | ​  |  |
    | ​  | ​`return`​ `array[array.length - 1];` |
    | ​  | } |

    -   我们的下一个也是最后一个实现是 O(N)，因为我们只需对数组进行一次遍历：

    | ​  | ​`function`​ `max(array) {` |
    | --- | --- |
    | ​  | ​`if`​ (`array.length === 0`) { ​`return`​ ​`null`​; } |
    | ​  |  |
    | ​  | ​`let`​ `greatestNumberSoFar` = `array[0]`; |
    | ​  |  |
    | ​  | ​`for`​ (​`const`​ `number` ​`of`​ `array`) { |
    | ​  | ​`if`​ (`number > greatestNumberSoFar`) { |
    | ​  | `greatestNumberSoFar` = `number`; |
    | ​  | } |
    | ​  | } |
    | ​  |  |
    | ​  | ​`return`​ `greatestNumberSoFar;` |
    | ​  | } |
