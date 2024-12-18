## 一个实际的例子

假设你正在编写一个JavaScript应用程序，在代码的某个地方你发现需要获取两个数组之间的交集。交集是两个数组中所有出现的值的列表。例如，如果你有数组`[3, 1, 4, 2]`和`[4, 5, 3, 6]`，交集将是第三个数组`[3, 4]`，因为这两个值在两个数组中都是公共的。

这里有一个可能的实现：

| ​  | ​`function`​ `intersection(firstArray, secondArray) {` |
| --- | --- |
| ​  | ​`const`​ `result = [];` |
| ​  |  |
| ​  | ​`for`​ (​`const`​ `i` ​`of`​ `firstArray`) { |
| ​  | ​`for`​ (​`const`​ `j` ​`of`​ `secondArray`) { |
| ​  | ​`if`​ (`i === j`) { |
| ​  | `result.push(i);` |
| ​  | } |
| ​  | } |
| ​  | } |
| ​  |  |
| ​  | ​`return`​ `result;` |
| ​  | } |

在这里，我们运行嵌套循环。在外循环中，我们遍历第一个数组中的每个值。当我们指向第一个数组中的每个值时，我们会运行一个内部循环，检查第二个数组中的每个值，以查看它是否可以找到与第一个数组中指向的值匹配的值。

在这个算法中，进行的步骤有两种：比较和插入。我们将两个数组的每个值彼此进行比较，并将匹配的值插入到数组`result`中。让我们先看看有多少次比较。

如果两个数组的大小相等，假设`N`是任一数组的大小，则执行的比较次数为`N²`。这是因为我们将第一个数组的每个元素与第二个数组的每个元素进行比较。因此，如果我们有两个各包含五个元素的数组，我们最终会进行二十五次比较。所以这个交集算法的效率是`O(N²)`。

插入操作最多会花费`N`步（如果两个数组恰好是相同的）。这比`N²`的阶数要低，所以我们仍然将该算法视为`O(N²)`。如果数组的大小不同——假设为`N`和`M`——我们会说这个函数的效率是`O(N * M)`。（更多内容可以在第7章找到，[​*日常代码中的大O*​](f_0064.xhtml#chp.everyday_big_o)）。

是否有任何方法可以改进这个算法？

在此，我们重要的是考虑最坏情况以外的场景。在当前的交集函数实现中，我们在所有场景中进行`N²`次比较，无论数组是否相同或数组是否没有一个共同值。

然而，在两个数组共享公共值的地方，我们实际上不应该需要将第二个数组的每个值与第一个数组的值进行比较。

让我们看看原因：

![images/optimizing_for_optimistic_scenarios/unnecessary_step.png](images/optimizing_for_optimistic_scenarios/unnecessary_step.png)

在这个例子中，一旦我们找到一个共同的值（`8`），其实就没有理由完成第二个循环。此时我们在检查什么呢？我们已经确定第二个数组包含了与第一个数组相同的`8`，可以将其添加到`result`中。我们正在执行一个不必要的步骤。

为了解决这个问题，我们可以在实现中添加一个单词：

| ​  | `function`​ `intersection(firstArray, secondArray) {` |
| --- | --- |
| ​  | `const`​ `result` = []; |
| ​  |  |
| ​  | `for`​ (`const`​ `i` ​`of`​ `firstArray`) { |
| ​  | `for`​ (`const`​ `j` ​`of`​ `secondArray`) { |
| ​  | `if`​ (`i === j`) { |
| ​  | `result.push(i);` |
| ​  | `break`​; |
| ​  | } |
| ​  | } |
| ​  | } |
| ​  |  |
| ​  | `return`​ `result;` |
| ​  | } |

通过添加`break`，我们可以缩短内循环并节省步骤（因此也节省时间）。

在最坏的情况下，如果两个数组不包含任何共同值，我们仍然不得不执行`N²`次比较。但现在，在数组共享值的情况下，我们可以减少步骤数。

这是我们`intersection`函数的一个重要优化，因为我们第一版的实现会在所有情况下进行`N²`次比较。
