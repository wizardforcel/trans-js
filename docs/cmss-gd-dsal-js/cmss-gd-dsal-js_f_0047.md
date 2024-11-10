## 练习

以下练习提供了一个机会，让你练习加快代码的速度。这些练习的解决方案在章节 [​*第 4 章*](f_0209.xhtml#speeding.up.your.code.with.big.o.solutions) 中可以找到。

1.  替换下表中的问号，以描述在不同类型的大 O 中，对于给定数量的数据元素会发生多少步骤：

    | N 元素 | O(N) | O(log N) | O(N²) |
    | --- | --- | --- | --- |
    | 100 | 100 | ? | ? |
    | 2,000 | ? | ? | ? |

1.  如果我们有一个 O(N²) 算法处理一个数组，并且发现它需要 256 步，那么数组的大小是多少？

1.  使用大 O 符号描述以下函数的时间复杂度。它在给定数组中找到任何两个数字的最大乘积：

    | ​  | `function` greatestProduct(array) { |
    | --- | --- |
    | ​  | `if` (array.length < 2) { `return` `null`; } |
    | ​  |  |
    | ​  | `let` greatestProductSoFar = array[0] * array[1]; |
    | ​  |  |
    | ​  | `for` (`const` [indexI, valueI] `of` array.entries()) { |
    | ​  | `for` (`const` [indexJ, valueJ] `of` array.entries()) { |
    | ​  | `if` (indexI !== indexJ && valueI * valueJ > greatestProductSoFar) { |
    | ​  | greatestProductSoFar = valueI * valueJ; |
    | ​  | } |
    | ​  | } |
    | ​  | } |
    | ​  |  |
    | ​  | `return` greatestProductSoFar; |
    | ​  | } |

1.  该函数在数组中找到最大的单个数字，但它的效率为 O(N²)。重写该函数，使其变得快速，效率为 O(N)：

    | ​  | `function` greatestNumber(array) { |
    | --- | --- |
    | ​  | `let` isITheGreatest; |
    | ​  | `if` (array.length === 0) { `return` `null`; } |
    | ​  |  |
    | ​  | `for` (`const` i `of` array) { |
    | ​  | `// 假设目前 i 是最大的：` |
    | ​  | isITheGreatest = `true`; |
    | ​  |  |
    | ​  | `for` (`const` j `of` array) { |
    | ​  | `// 如果我们找到另一个比 i 更大的值，` |
    | ​  | `// 那么 i 不是最大的：` |
    | ​  | `if` (j > i) { isITheGreatest = `false`; } |
    | ​  | } |
    | ​  | `// 如果到我们检查所有其他数字时，i 仍然是` |
    | ​  | `// 如果 i 是最大的数字：` |
    | ​  | `if` (isITheGreatest) { |
    | ​  | `return` i; |
    | ​  | } |
    | ​  | } |
    | ​  | } |

版权所有 © 2024, The Pragmatic Bookshelf.
