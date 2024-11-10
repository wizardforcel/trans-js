## 第10章

这些是章节[**练习**](f_0103.xhtml#recursively.recurse.with.recursion.exercises)中练习的解答。

1.  基准情况是`if (low > high)`——也就是说，我们希望在`low`超过`high`时停止递归。否则，我们将打印出比`high`更大的数字，一直到无穷大。

1.  我们会有无限递归！`factorial(10)`调用`factorial(8)`，它又调用`factorial(6)`，依此类推，最终调用`factorial(0)`。由于我们的基准情况是`if (number === 1)`，因此我们永远不会得到`number`为1，所以递归继续。`factorial(0)`调用`factorial(-2)`，依此类推。

1.  假设`low`是1，`high`是10。当我们调用`sum(1, 10)`时，它会返回`10 + sum(1, 9)`。也就是说，我们返回10加上`1`到`9`的和。`sum(1, 9)`最终调用`sum(1, 8)`，依此类推。

    我们希望最后的调用是`sum(1, 1)`，在这种情况下我们只想返回数字1。这成为我们的基准情况：

    | ​  | `function` sum(low, high) { |
    | --- | --- |
    | ​  | `// 基准情况:` |
    | ​  | `if` (high === low) { |
    | ​  | `return` low; |
    | ​  | } |
    | ​  |  |
    | ​  | `return` high + `sum`(low, high - 1); |
    | ​  | } |

1.  这种方法类似于文本中的文件目录示例：

    | ​  | `function` printAllItems(array) { |
    | --- | --- |
    | ​  | `for` (`const` value `of` array) { |
    | ​  | `// 如果当前值是一个数组:` |
    | ​  | `if` (Array.isArray(value)) { |
    | ​  | `printAllItems(value);` |
    | ​  | } `else` { |
    | ​  | `console.log(value);` |
    | ​  | } |
    | ​  | } |
    | ​  | } |

    我们迭代外部数组中的每个项目。如果值本身是另一个数组，我们就对该子数组递归调用函数。否则，就是基准情况，我们只是将值打印到屏幕上。
