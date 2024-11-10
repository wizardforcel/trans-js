## 偶数的平均值

以下方法接受一个数字数组并返回所有偶数的平均值。我们如何用大 O 来表达它的效率呢？

| ​  | `function` averageOfEvenNumbers(array) { |
| --- | --- |
| ​  | `let` sum = 0; |
| ​  | `let` countOfEvenNumbers = 0; |
| ​  |  |
| ​  | `for` (`const` number `of` array) { |
| ​  | `if` (number % 2 === 0) { |
| ​  | sum += number; |
| ​  | countOfEvenNumbers += 1; |
| ​  | } |
| ​  | }; |
| ​  |  |
| ​  | `if` (countOfEvenNumbers === 0) { `return` `null`; } |
| ​  |  |
| ​  | `return` Math.floor(sum / countOfEvenNumbers); |
| ​  | } |

下面是如何拆解代码以确定其效率的方法。

请记住，大 O 符号的核心是回答一个关键问题：如果有 `N` 个数据元素，算法将执行多少步骤？因此，我们首先要做的是确定 `N` 个数据元素是什么。

在这种情况下，算法正在处理传递给该方法的数字数组。这些就是 `N` 个数据元素，其中 `N` 是数组的大小。

接下来，我们需要确定算法处理这些 `N` 值所需的步骤数。

我们可以看到算法的核心是遍历数组中每个数字的循环，所以我们首先要分析这个循环。由于循环遍历每个 `N` 元素，我们知道算法至少需要 `N` 步骤。

不过，查看循环内部，我们可以看到每一轮循环中会发生不同数量的步骤。对于每一个数字，我们检查这个数字是否是偶数。然后，如果数字是偶数，我们再执行两个步骤：修改 `sum` 变量和修改 `countOfEvenNumbers` 变量。因此，对于偶数，我们比对奇数多执行两个步骤。

正如你所学，大 O 主要关注最坏情况。在我们的例子中，最坏情况是所有数字都是偶数，在这种情况下，我们在每一轮循环中执行三步。因此，我们可以说，对于 `N` 个数据元素，我们的算法需要 `3N` 步骤。也就是说，对于每一个 `N` 数字，我们的算法执行三步。

现在，我们的方法在循环外还执行了一些其他步骤。在循环之前，我们初始化两个变量并将其设置为 `0`。从技术上讲，这两步。循环之后，我们执行另一个步骤：`sum / countOfEvenNumbers` 的除法。从技术上讲，我们的算法在 `3N` 步骤之外多了三步，所以总步骤数是 `3N + 3`。

然而，你也学到了大 O 符号忽略常数，所以我们不叫我们的算法 `O(3N + 3)`，而是简单地称它为 `O(N)`。