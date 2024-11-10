## 练习

以下练习为你提供了练习动态编程的机会。这些练习的解答在章节 [`第12章`](f_0217.xhtml#dynamic.programming.solutions) 中可以找到。

1.  以下函数接受一个数字数组，并返回其总和，只要某个特定数字没有使总和超过100。如果添加某个特定数字会使总和高于100，则忽略该数字。然而，这个函数做了不必要的递归调用。修复代码以消除不必要的递归：

    | ​  | `function` addUntil100(array) { |
    | --- | --- |
    | ​  | `if` (array.length === 0) { `return` 0; } |
    | ​  |  |
    | ​  | `if` (array[0] + addUntil100(array.slice(1)) > 100) { |
    | ​  | `return` addUntil100(array.slice(1)); |
    | ​  | } `else` { |
    | ​  | `return` array[0] + addUntil100(array.slice(1)); |
    | ​  | } |
    | ​  | } |

1.  以下函数使用递归来计算一个称为 Golomb 序列的数学序列中的第 N 个数字。然而，它的效率非常低！使用备忘录来优化它。（你不需要理解 Golomb 序列的工作原理就可以完成这个练习。）

    | ​  | `function` golomb(n) { |
    | --- | --- |
    | ​  | `if` (n === 1) { `return` 1; } |
    | ​  |  |
    | ​  | `return` 1 + golomb(n - golomb(golomb(n - 1))); |
    | ​  | } |

1.  这里是上章练习中唯一路径问题的解答。（抱歉，如果你还没有尝试这个练习，这有点剧透。）使用备忘录来提高其效率：

    | ​  | `function` uniquePaths(rows, columns) { |
    | --- | --- |
    | ​  | `if` (rows === 1 ` | | ` columns === 1) { |
    | ​  | `return` 1; |
    | ​  | } |
    | ​  |  |
    | ​  | `return` uniquePaths(rows - 1, columns) + uniquePaths(rows, columns - 1); |
    | ​  | } |

版权所有 © 2024, The Pragmatic Bookshelf.
