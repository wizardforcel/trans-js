## 练习

以下练习为你提供了用大 O 符号进行练习的机会。这些练习的答案在 [`第 3 章`](f_0208.xhtml#big.o.notation.solutions) 中可以找到。

1.  使用大 O 符号描述以下函数的时间复杂度，该函数用于确定给定年份是否为闰年：

    | ​  | `function` isLeapYear(year) { |
    | --- | --- |
    | ​  | `if` (year % 100 === 0) { |
    | ​  | `if` (year % 400 === 0) { |
    | ​  | `return` `true`; |
    | ​  | } `else` { |
    | ​  | `return` `false`; |
    | ​  | } |
    | ​  | } |
    | ​  | `return` year % 4 === 0; |
    | ​  | } |

1.  使用大 O 符号描述以下函数的时间复杂度，该函数计算给定数组中所有数字的总和：

    | ​  | `function` arraySum(array) { |
    | --- | --- |
    | ​  | `let` sum = 0; |
    | ​  |  |
    | ​  | `for` (`const` number `of` array) { |
    | ​  | sum += number; |
    | ​  | }; |
    | ​  |  |
    | ​  | `return` sum; |
    | ​  | } |

1.  以下函数基于古老的类比，用于描述复利的威力：

    想象一下你有一个棋盘，在一个方格上放置一粒米。在第二个方格上，你放置两粒米，因为那是前一个方格米粒数量的两倍。在第三个方格上，你放置四粒米。在第四个方格上，你放置八粒米，在第五个方格上放置十六粒米，依此类推。

    以下函数计算需要放置多少粒米的方格。例如，对于十六粒米，函数将返回 5，因为你将在第五个方格上放置这十六粒米。

    使用大 O 符号描述以下函数的时间复杂度，该函数如下：

    | ​  | `function` chessboardSpace(numberOfGrains) { |
    | --- | --- |
    | ​  | `let` chessboardSpaces = 1; |
    | ​  | `let` placedGrains = 1; |
    | ​  |  |
    | ​  | `while` (placedGrains < numberOfGrains) { |
    | ​  | placedGrains *= 2; |
    | ​  | chessboardSpaces += 1; |
    | ​  | } |
    | ​  |  |
    | ​  | `return` chessboardSpaces; |
    | ​  | } |

1.  以下函数接受一个字符串数组，并返回一个只包含以字符 ’a’ 开头的字符串的新数组。请用大 O 符号描述该函数的时间复杂度：

    | ​  | `function` selectAStrings(array) { |
    | --- | --- |
    | ​  | `const` newArray = []; |
    | ​  |  |
    | ​  | `for` (`const` string `of` array) { |
    | ​  | `if` (string[0] === `'a'`) { newArray.push(string); } |
    | ​  | }; |
    | ​  |  |
    | ​  | `return` newArray; |
    | ​  | } |

1.  以下函数计算有序数组的中位数。请用大 O 符号描述其时间复杂度：

    | ​  | `function` median(array) { |
    | --- | --- |
    | ​  | `if` (array.length === 0) { `return` `null`; } |
    | ​  |  |
    | ​  | `const` middle = Math.floor(array.length / 2); |
    | ​  |  |
    | ​  | `// 如果数组中的数字数量为偶数:` |
    | ​  | `if` (array.length % 2 === 0) { |
    | ​  | `return` (array[`middle - 1`] + array[`middle`]) / 2; |
    | ​  | } `else` { `// 如果数组中的数字数量为奇数:` |
    | ​  | `return` array[`middle`]; |
    | ​  | } |
    | ​  | } |

版权 © 2024, The Pragmatic Bookshelf.
