## `回文检查器`

回文是一个单词或短语，正着和反着读都是一样的。一些例子包括`racecar`、`kayak`和`deified`。

这是一个确定字符串是否为回文的函数：

| ​  | `function` isPalindrome(string) { |
| --- | --- |
| ​  | `let` leftIndex = 0; |
| ​  | `let` rightIndex = string.length - 1; |
| ​  |  |
| ​  | `// Iterate until leftIndex reaches the middle of the array:` |
| ​  | `while` (leftIndex < Math.floor(string.length / 2)) { |
| ​  | `// If the character on the left doesn't equal the character` |
| ​  | `// on the right, the string is not a palindrome:` |
| ​  | `if` (string[leftIndex] !== string[rightIndex]) { |
| ​  | `return` `false`; |
| ​  | } |
| ​  |  |
| ​  | leftIndex += 1; |
| ​  | rightIndex -= 1; |
| ​  | } |
| ​  |  |
| ​  | `// If we got through the entire loop without finding any` |
| ​  | `// mismatches, the string must be a palindrome:` |
| ​  | `return` `true`; |
| ​  | } |

让我们来确定这个算法的**大 O**。

在这种情况下，N是传递给此函数的字符串的大小。

算法的核心在于while循环。现在，这个循环有点有趣，因为它只在到达字符串的中点之前运行。这意味着循环运行了N / 2步。

然而，**大 O**忽略常数。因此，我们去掉除以2的操作，我们的算法是O(N)。
