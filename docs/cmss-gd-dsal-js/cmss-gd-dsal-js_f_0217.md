## 第12章

这些是[*练习*](f_0120.xhtml#dynamic.programming.exercises)部分中的习题解答。

1.  这里的问题是函数每次运行时递归调用自身两次。让我们修改它，使得每次只调用一次：

    | ​  | `function` addUntil100(array) { |
    | --- | --- |
    | ​  | `if` (array.length === 0) { `return` 0; } |
    | ​  |  |
    | ​  | `const` sumOfRemainingNumbers = addUntil100(array.slice(1)); |
    | ​  |  |
    | ​  | `if` (array[0] + sumOfRemainingNumbers > 100) { |
    | ​  | `return` sumOfRemainingNumbers; |
    | ​  | } `else` { |
    | ​  | `return` array[0] + sumOfRemainingNumbers; |
    | ​  | } |
    | ​  | } |

1.  这是备忘录版本：

    | ​  | `function` golomb(n, memo = {}) { |
    | --- | --- |
    | ​  | `if` (n === 1) { `return` 1; } |
    | ​  |  |
    | ​  | `if` (!memo[n]) { |
    | ​  | `memo`[n] = 1 + golomb(n - golomb(golomb(n - 1, memo), memo), memo); |
    | ​  | } |
    | ​  |  |
    | ​  | `return` memo[n]; |
    | ​  | } |

1.  为了实现备忘录功能，我们需要创建一个键，考虑行数和列数。为此，我们可以将键基于行和列组合。

| ​  | `function` uniquePaths(rows, columns, memo = {}) { |
| --- | --- |
| ​  | `if` (rows === 1 | | columns === 1) { |
| ​  | `return` 1; |
| ​  | } |
| ​  |  |
| ​  | `if` (!memo[[rows, columns]]) { |
| ​  | `memo`[[rows, columns]] = (uniquePaths(rows - 1, columns, memo) |
| ​  | + uniquePaths(rows, columns - 1, memo)); |
| ​  | } |
| ​  |  |
| ​  | `return` memo[[rows, columns]]; |
| ​  | } |
