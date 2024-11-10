## 练习

以下练习为您提供在空间限制下练习的机会。这些练习的解决方案在[`第19章`](f_0224.xhtml#dealing.with.space.constraints.solutions)中可以找到。

1.  以下是我们在[`单词生成器`](f_0066.xhtml#sect.word-builder)中遇到的单词生成算法。用大O符号描述其空间复杂度：

    | ​  | ​`function`​ `wordBuilder(array)` { |
    | --- | --- |
    | ​  | ​`const`​ `collection` = []; |
    | ​  |  |
    | ​  | ​`for`​ (​`const`​ `[indexI, valueI]` ​`of`​ `array.entries()`) { |
    | ​  | ​`for`​ (​`const`​ `[indexJ, valueJ]` ​`of`​ `array.entries()`) { |
    | ​  | ​`if`​ (`indexI !== indexJ`) { |
    | ​  | `collection.push(valueI + valueJ);` |
    | ​  | } |
    | ​  | } |
    | ​  | } |
    | ​  |  |
    | ​  | ​`return`​ `collection`; |
    | ​  | } |

1.  以下是一个反转数组的函数。用大O符号描述其空间复杂度：

    | ​  | ​`function`​ `reverse(array)` { |
    | --- | --- |
    | ​  | ​`const`​ `newArray` = []; |
    | ​  |  |
    | ​  | ​`for`​ (​`const`​ `value` ​`of`​ `array`) { |
    | ​  | `newArray.unshift(value);` |
    | ​  | } |
    | ​  |  |
    | ​  | ​`return`​ `newArray`; |
    | ​  | } |

1.  创建一个新的函数来反转数组，仅占用O(1)的额外空间。

1.  以下是三个不同的实现，它们接受一个数字数组并返回一个包含这些数字乘以2的数组。例如，如果输入是`[5, 4, 3, 2, 1]`，输出将是`[10, 8, 6, 4, 2]`。

    | ​  | ​`function`​ `doubleArray1(array)` { |
    | --- | --- |
    | ​  | ​`const`​ `newArray` = []; |
    | ​  |  |
    | ​  | ​`for`​ (​`const`​ `value` ​`of`​ `array`) { |
    | ​  | `newArray.push(value * 2);` |
    | ​  | } |
    | ​  |  |
    | ​  | ​`return`​ `newArray`; |
    | ​  | } |
    | ​  |  |
    | ​  | ​`function`​ `doubleArray2(array)` { |
    | ​  | ​`for`​ (​`let`​ `i = 0; i < array.length; i += 1`) { |
    | ​  | `array[i] *= 2;` |
    | ​  | } |
    | ​  |  |
    | ​  | ​`return`​ `array`; |
    | ​  | } |
    | ​  |  |
    | ​  | ​`function`​ `doubleArray3(array, index = 0)` { |
    | ​  | ​`if`​ (`index >= array.length`) { ​`return`; } |
    | ​  |  |
    | ​  | `array[index] *= 2;` |
    | ​  | `doubleArray3(array, index + 1);` |
    | ​  |  |
    | ​  | ​`return`​ `array`; |
    | ​  | } |

    填写下表，以描述这三个版本在时间和空间效率方面的表现：

    | 版本 | 时间复杂度 | 空间复杂度 |
    | --- | --- | --- |
    | 版本 #1 | ? | ? |
    | 版本 #2 | ? | ? |
    | 版本 #3 | ? | ? |

版权所有 © 2024, The Pragmatic Bookshelf.
