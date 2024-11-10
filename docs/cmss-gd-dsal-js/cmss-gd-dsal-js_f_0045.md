## 线性解决方案

接下来是另一个`hasDuplicateValue`函数的实现，它不依赖于嵌套循环。它有点聪明，所以让我们先看看它是如何工作的，然后再看看它是否比我们第一次的实现更高效。

|   | `function hasDuplicateValue(array) {` |
| --- | --- |
|   | `const existingNumbers = [];` |
|   |   |
|   | `for (let i = 0; i < array.length; i += 1) {` |
|   | `if (existingNumbers[array[i]] === 1) {` |
|   | `return true;` |
|   | `}` `else` `{` |
|   | `existingNumbers[array[i]] = 1;` |
|   | `}` |
|   | `}` |
|   |   |
|   | `return false;` |
|   | `}` |

这个函数的作用是创建一个名为`existingNumbers`的数组，它最开始是空的。

然后我们使用一个循环检查输入数组中的每个数字。当它遇到每个数字时，它会在等于我们正在遇到的数字的索引位置向`existingNumbers`中放置一个任意值（我们选择使用`1`）。

例如，假设我们的输入数组是`[3, 5, 8]`。当我们遇到`3`时，我们在`existingNumbers`的索引`3`位置放置一个`1`。因此，`existingNumbers`数组现在大致相当于：

|   | `[0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0]` |
| --- | --- |

在`existingNumbers`的索引`3`处现在有一个`1`，以指示并记住我们已经在给定数组中遇到过一个`3`。

当我们的循环遇到给定数组中的`5`时，它在`existingNumbers`的索引`5`位置添加一个`1`：

|   | `[0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0]` |
| --- | --- |

最后，当我们达到`8`时，`existingNumbers`现在看起来是这样的：

|   | `[0, 0, 0, 1, 0, 1, 0, 0, 1, 0, 0]` |
| --- | --- |

本质上，我们使用`existingNumbers`的索引来记住到目前为止我们从数组中见过哪些数字。

现在，这里有个真正的技巧。在代码将`1`存储到适当的索引之前，它首先检查该索引的值是否已经为`1`。如果是，这意味着我们已经遇到过那个数字，说明找到了重复项。如果是这种情况，我们只需返回`true`并中止函数。如果我们到达循环末尾而没有返回`true`，则意味着没有重复项，我们返回`false`。

为了确定这个新算法在大O符号方面的效率，我们需要再次确定算法在最坏情况下所需的步骤数。

在这里，重要的步骤类型是查看每个数字并检查其在`existingNumbers`中的索引值是否为`1`：

|   | `if (existingNumbers[array[i]] === 1) {` |
| --- | --- |

（除了比较，我们还对`existingNumbers`数组进行插入，但在此分析中我们认为这类步骤是微不足道的。关于这一点，我们将在下一章讨论。）

在最坏情况下，这种情况发生在数组不包含重复项的情况下，这时我们的函数必须完成整个循环。

这个新算法似乎为N个数据元素进行了N次比较。这是因为只有一个循环，它只是为数组中的数字数量进行迭代。我们可以通过在JavaScript控制台中跟踪步骤来测试这个理论：

| ​  | `function`​ hasDuplicateValue(array) { |
| --- | --- |
| ​  | `let`​ steps = 0; |
| ​  | `const`​ existingNumbers = []; |
| ​  |  |
| ​  | `for` (​`let`​ i = 0; i < array.length; i += 1) { |
| ​  | steps += 1; |
| ​  | `if` (existingNumbers[array[i]] === 1) { |
| ​  | `return`​ `true`; |
| ​  | } `else` { |
| ​  | existingNumbers[array[i]] = 1; |
| ​  | } |
| ​  | } |
| ​  |  |
| ​  | `console.log(steps);` |
| ​  | `return`​ `false`; |
| ​  | } |

如果我们现在运行`hasDuplicateValue([1, 4, 5, 2, 9])`，我们会看到JavaScript控制台中的输出是5，这与我们数组的大小相同。我们会发现这一点在所有大小的数组中都是成立的。因此，这个算法是O(N)。

我们知道O(N)比O(N²)快得多，因此通过使用这种第二种方法，我们显著优化了我们的`hasDuplicateValue`函数。这是一个巨大的速度提升。

(这种新实现的一个缺点是，这种方法会比第一种方法消耗更多的内存。暂时不必担心这一点；我们将在第19章[​*处理空间限制*​](f_0189.xhtml#chp.dealing_with_space_constraints)中详细讨论。)
