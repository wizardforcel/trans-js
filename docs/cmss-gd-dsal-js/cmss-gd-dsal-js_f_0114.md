## 小小的修正对大O的影响

感谢，有一种简单的方法可以消除所有这些额外的递归调用。我们将在代码中仅调用一次`max`，并将结果保存到一个变量中：

| ​  | `function` max(array) { |
| --- | --- |
| ​  | `if` (array.length === 0) { `return` `null`; } |
| ​  |  |
| ​  | `if` (array.length === 1) { `return` array[0]; } |
| ​  |  |
| ​  | `// 计算数组其余部分的最大值` |
| ​  | `// 并将其存储在一个变量中:` |
| ​  | `const` maxOfRemainder = max(array.slice(1)); |
| ​  |  |
| ​  | `// 将第一个数字与这个变量进行比较:` |
| ​  | `if` (array[0] > maxOfRemainder) { |
| ​  | `return` array[0]; |
| ​  | } `else` { |
| ​  | `return` maxOfRemainder; |
| ​  | } |
| ​  | } |

通过实现这个简单的修改，我们最终只调用了`max`四次。通过添加`console.log('RECURSION')`行并运行代码，自己试试看吧。

这里的窍门是我们每个必要的函数调用只进行一次，并将结果保存在一个变量中，这样就不必再次调用该函数。

我们初始函数与稍微修改过的函数之间的效率差异显著。
