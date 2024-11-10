## 删除

从 `array` 中删除是指消除特定索引处的值的过程。

让我们回到最初的示例数组，并删除索引 `2` 处的值。在我们的示例中，这个值是 `"cucumbers"`。

第 `1` 步：我们从 `array` 中删除 `"cucumbers"`：

![`images/understanding_arrays/array_16.png`](images/understanding_arrays/array_16.png)

尽管实际上删除 `"cucumbers"` 只需一步，但我们现在遇到了一个问题：我们的数组中正好有一个空单元。数组在中间有空缺时并不高效，因此为了解决这个问题，我们需要将 `"dates"` 和 `"elderberries"` 向左移动。这意味着我们的删除过程需要额外的步骤。

第 `2` 步：我们将 `"dates"` 向左移动：

![`images/understanding_arrays/array_17.png`](images/understanding_arrays/array_17.png)

第 `3` 步：我们将 `"elderberries"` 向左移动：

![`images/understanding_arrays/array_18.png`](images/understanding_arrays/array_18.png)

结果是，这个删除操作总共花费了三步。第一步是实际的删除，接下来的两步是数据移动以填补空缺。

与插入相似，删除元素的最坏情况是删除 `array` 中的第一个元素。这是因为索引 `0` 会变为空，我们需要将所有剩余元素向左移动以填补空缺。

对于一个包含 `5` 个元素的 `array`，我们需要 `1` 步删除第一个元素，并且需要 `4` 步将剩下的 `4` 个元素移动。对于一个包含 `500` 个元素的 `array`，我们需要 `1` 步删除第一个元素，以及 `499` 步移动剩余数据。因此我们可以说，对于一个包含 `N` 个元素的 `array`，删除操作所需的最大步骤数是 `N` 步。

恭喜你！我们已经分析了第一个数据结构的时间复杂度。现在你已经学会了如何分析数据结构的效率，你可以发现不同的数据结构具有不同的效率。这一点至关重要，因为为你的代码选择正确的数据结构可能会对软件的性能产生严重影响。

下一个数据结构——`set`——乍一看似乎与 `array` 非常相似。然而，你会发现对 `arrays` 和 `sets` 执行的操作具有不同的效率。
