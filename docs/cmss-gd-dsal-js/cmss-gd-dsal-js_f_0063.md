## 练习

以下练习为您提供了优化最佳和最坏情况场景的实践机会。这些练习的解决方案在章节 [*第六章*](f_0211.xhtml#optimizing.for.optimistic.scenarios.solutions) 中找到。

1.  使用`Big O`符号来描述一个算法的效率，该算法需要`3N² + 2N + 1`步。

1.  使用`Big O`符号来描述一个算法的效率，该算法需要`N + log N`步。

1.  以下函数检查一个数字数组是否包含一对和为10的两个数字。

    | ​  | ​`function`​ `twoSum`(`array`) { |
    | --- | --- |
    | ​  | ​`for`​ (​`const`​ [indexI, i] ​`of`​ `array.entries()`) { |
    | ​  | ​`for`​ (​`const`​ [indexJ, j] ​`of`​ `array.entries()`) { |
    | ​  | ​`if`​ ((indexI !== indexJ) && (i + j === 10)) { |
    | ​  | ​`return`​ ​`true`; |
    | ​  | } |
    | ​  | } |
    | ​  | } |
    | ​  |  |
    | ​  | ​`return`​ ​`false`; |
    | ​  | } |

    最佳、平均和最坏情况场景是什么？然后，用`Big O`符号表达最坏情况场景。

1.  以下函数返回字符串中是否存在大写字母“X”。

    | ​  | ​`function`​ `containsX`(`string`) { |
    | --- | --- |
    | ​  | ​`let`​ `foundX` = ​`false`; |
    | ​  |  |
    | ​  | ​`for`​ (​`const`​ ​`char`​ ​`of`​ `string`) { |
    | ​  | ​`if`​ (`char` === `'X'`) { `foundX` = ​`true`; } |
    | ​  | } |
    | ​  | ​`return`​ `foundX`; |
    | ​  | } |

    这个函数的时间复杂度用`Big O`符号表示是什么？

    然后，修改代码以提高算法在最佳和平均情况场景下的效率。

版权所有 © 2024, The Pragmatic Bookshelf.
