## 第四章

这些是 [练习](f_0047.xhtml#speeding.up.your.code.with.big.o.exercises) 部分中的习题解答。

1.  这里是完成的表格：

    | N 元素 | O(N) | O(log N) | O(N²) |
    | --- | --- | --- | --- |
    | 100 | 100 | 约 7 | 10,000 |
    | 2,000 | 2,000 | 约 11 | 4,000,000 |

1.  该数组将有十六个元素，因为 16² 是 256。（换句话说，256 的平方根是 16。）

1.  该算法的时间复杂度为 O(N²)。在这种情况下，N 是数组的大小。我们有一个外部循环，它遍历数组 N 次，对于每次循环，内部循环也遍历同一个数组 N 次。这导致了 N² 步骤。

1.  以下版本的时间复杂度为 O(N)，因为我们只遍历数组一次：

    | ​  | `function` greatestNumber(array) { |
    | --- | --- |
    | ​  | `if` (array.length === 0) { `return` `null`; } |
    | ​  |  |
    | ​  | `let` greatestNumberSoFar = array[0]; |
    | ​  |  |
    | ​  | `for` (`const` i `of` array) { |
    | ​  | `if` (i > greatestNumberSoFar) { |
    | ​  | greatestNumberSoFar = i; |
    | ​  | } |
    | ​  | } |
    | ​  |  |
    | ​  | `return` greatestNumberSoFar; |
    | ​  | } |
