## 删除操作

在二叉搜索树中，删除操作是最不直接的操作，需要一些小心的处理。

假设我们想从这棵二叉搜索树中删除`4`：

![images/binary_trees/bst_4.png](images/binary_trees/bst_4.png)

首先，我们执行搜索以找到`4`。我们不再可视化这个搜索，因为你已经掌握了。

一旦找到`4`，我们可以一步删除它：

![images/binary_trees/bst_16.png](images/binary_trees/bst_16.png)

好吧，这很简单。但是让我们看看当我们尝试删除`10`时会发生什么：

![images/binary_trees/bst_17.png](images/binary_trees/bst_17.png)

我们最终得到了一个不再与树连接的`11`。我们不能这样，因为我们会永远失去`11`。

不过，为了解决这个问题，我们可以把`11`放入`10`曾经的位置：

![images/binary_trees/bst_18.png](images/binary_trees/bst_18.png)

到目前为止，我们的删除算法遵循以下规则：

+   如果被删除的节点没有子节点，简单地将其删除。

+   如果被删除的节点有一个子节点，删除该节点并将子节点放入被删除节点的位置。

### 删除一个有两个子节点的节点

删除一个有两个子节点的节点是最复杂的情况。假设我们想在这棵树中删除`56`：

![images/binary_trees/bst_19.png](images/binary_trees/bst_19.png)

我们将如何处理它之前的子节点`52`和`61`？我们不能把它们都移动到`56`的位置。这就是删除算法的下一个规则发挥作用的地方：

+   当删除一个有两个子节点的节点时，用后继节点替换被删除的节点。后继节点是值大于被删除节点的所有值中最小的子节点。

那是一个棘手的句子。换句话说：如果我们将被删除的节点及其所有后代按升序排列，后继节点就是我们刚刚删除的节点之后的下一个数字。

在这种情况下，很容易找出哪个节点是后继，因为被删除的节点只有两个后代。如果我们将数字`52-56-61`按升序排列，`56`之后的下一个数字是`61`。

一旦找到后继节点，我们就把它放入被删除节点的位置。因此，我们用`61`替换`56`：

![images/binary_trees/bst_20.png](images/binary_trees/bst_20.png)

### 查找后继节点

计算机是如何找到后继节点的？当我们删除树中较高的节点时，这可能会很棘手。

这是查找后继节点的算法：

+   访问被删除值的右子节点，然后继续访问每个后续子节点的左子节点，直到没有更多的左子节点为止。最底部的值就是后继节点。

让我们在一个更复杂的例子中再次看到这个过程。让我们删除根节点：

![images/binary_trees/delete_root_node.png](images/binary_trees/delete_root_node.png)

我们现在需要将后继节点插入`50`的位置，并将其转变为根节点。那么让我们找到后继节点。

为此，我们首先访问被删除节点的右子节点，然后继续向左下降，直到到达一个没有左子节点的节点：

![images/binary_trees/bst_21.png](images/binary_trees/bst_21.png)

事实证明，`52`是后继节点。

现在我们已经找到了后继节点，我们将其插入我们删除的节点中：

![images/binary_trees/bst_22.png](images/binary_trees/bst_22.png)

我们完成了！

### 具有右子节点的后继节点

不过，我们还没有考虑到一种情况，那就是后继节点有自己的右子节点。让我们重建前面的树，但给`52`添加一个右子节点：

![images/binary_trees/bst_23.png](images/binary_trees/bst_23.png)

在这种情况下，我们不能简单地将后继节点`52`插入根节点，因为那样会让它的子节点`55`悬空。这给我们的删除算法带来了一个新的规则：

+   如果后继节点有一个右子节点，在将后继节点插入被删除节点的位置后，取后继节点的前右子节点并放置在后继节点曾经的位置。

这又是一个棘手的句子，所以让我们一步步来。

首先，我们将后继节点（`52`）插入根节点。这使得`55`没有父节点而悬空：

![images/binary_trees/bst_24.png](images/binary_trees/bst_24.png)

接下来，我们将`55`放在后继节点曾经的位置，也就是`61`的左子节点：

![images/binary_trees/bst_25.png](images/binary_trees/bst_25.png)

### 后继节点是右子节点

有时会发生后继节点本身就是右子节点的情况。有时，这个后继节点可能还有自己的右子节点。例如，在以下树中，如果我们删除`3`，`4`就成为后继节点，因为`4`没有左子节点：

![images/binary_trees/bst_15.png](images/binary_trees/bst_15.png)

在这里，当我们将后继节点插入被删除的`3`的位置时，我们不会让`5`悬空并在其他地方重新连接。相反，我们只是将`5`保留为`4`的右子节点。

现在我们真的完成了。

### 完整的删除算法

将所有步骤结合在一起，这就是从二叉搜索树中删除的算法：

+   如果被删除的节点没有子节点，简单地删除它。

+   如果被删除的节点有一个子节点，删除该节点并将子节点插入被删除节点的位置。

+   当删除一个具有两个子节点的节点时，用后继节点替换被删除的节点。后继节点是值大于被删除节点的所有值中最小的子节点。

+   要找到继承节点：访问删除节点的右子节点，然后继续访问每个后续子节点的左子节点，直到没有更多左子节点。底部节点就是继承节点。如果删除节点的右子节点没有左子节点，删除节点的右子节点本身就成为继承节点。

+   如果继承节点有右子节点（而且继承节点本身是其父节点的左子节点），在将继承节点插入删除节点的位置后，将继承节点的前右子节点变为前继承节点父节点的左子节点。

### 代码实现：二叉搜索树删除

这是一个从二叉搜索树中删除的 JavaScript 实现。这里的主要方法是 `delete`，它依赖于一个名为 `replaceWithSuccessorNode` 的辅助方法：

| `function deleteNode(valueToDelete, node) {` |
| --- |
| `let currentNode = node;` |
| `let parentOfCurrentNode;` |
| `let childOfDeletedNode;` |
| `let nodeToDelete;` |
| `` |
| `while (currentNode) {` |
| `if (currentNode.value === valueToDelete) {` |
| `nodeToDelete = currentNode;` |
| `break;` |
| `}` |
| `` |
| `parentOfCurrentNode = currentNode;` |
| `if (valueToDelete < currentNode.value) {` |
| `currentNode = currentNode.leftChild;` |
| `} else if (valueToDelete > currentNode.value) {` |
| `currentNode = currentNode.rightChild;` |
| `}` |
| `}` |
| `` |
| `if (!nodeToDelete) { return null; }` |
| `` |
| `if (nodeToDelete.leftChild && nodeToDelete.rightChild) {` |
| `replaceWithSuccessorNode(nodeToDelete);` |
| `} else { // deleted node has 0 or 1 children` |
| `childOfDeletedNode = (nodeToDelete.leftChild | | nodeToDelete.rightChild);` |
| `` |
| `if (!parentOfCurrentNode) {` |
| `nodeToDelete.value = childOfDeletedNode.value;` |
| `nodeToDelete.leftChild = childOfDeletedNode.leftChild;` |
| `nodeToDelete.rightChild = childOfDeletedNode.rightChild;` |
| `} else if (nodeToDelete === parentOfCurrentNode.leftChild) {` |
| `parentOfCurrentNode.leftChild = childOfDeletedNode;` |
| `} else if (nodeToDelete === parentOfCurrentNode.rightChild) {` |
| `parentOfCurrentNode.rightChild = childOfDeletedNode;` |
| `}` |
| `}` |
| `` |
| `return nodeToDelete;` |
| `}` |
| `` |
| `function replaceWithSuccessorNode(node) {` |
| `let successorNode = node.rightChild;` |
| `let parentOfSuccessorNode;` |
| `` |
| `if (!successorNode.leftChild) {` |
| `node.value = successorNode.value;` |
| `node.rightChild = successorNode.rightChild;` |
| `return;` |
| `}` |
| `` |
| `while (successorNode.leftChild) {` |
| `parentOfSuccessorNode = successorNode;` |
| `successorNode = successorNode.leftChild;` |
| `}` |
| `` |
| `if (successorNode.rightChild) {` |
| `parentOfSuccessorNode.leftChild = successorNode.rightChild;` |
| `} else {` |
| `parentOfSuccessorNode.leftChild = null;` |
| `}` |
| `` |
| `node.value = successorNode.value;` |
| `return successorNode;` |
| ​  | } |

这段代码相当多，但我们将一步步走过。

与搜索和插入相比，我们在没有递归的情况下编写了删除代码。虽然我们可以递归地编写删除方法，但我发现递归删除代码要比非递归的代码难以理解得多。相反，我们使用循环在树中移动。

让我们开始逐步了解删除方法。

当我们调用这个方法时，我们传入想要删除的值（valueToDelete）以及树的根节点（node）。

一开始，我们创建了几个变量：

| ​  | `let` currentNode = node; |
| --- | --- |
| ​  | `let` parentOfCurrentNode; |
| ​  | `let` childOfDeletedNode; |
| ​  | `let` nodeToDelete; |

`currentNode`最初指向根节点，但在我们向下移动树时会被更新，寻找要删除的值。`parentOfCurrentNode`，顾名思义，将追踪`currentNode`的父节点。`childOfDeletedNode`的情况也是如此。我们需要追踪这些变量的原因稍后会变得清楚。最后，`nodeToDelete`最终将指向我们要删除的节点。

然后我们开始一个循环，在树中搜索`valueToDelete`。这本质上是一个搜索操作，但这次我们使用迭代而不是递归：

| ​  | `while`(currentNode) { |
| --- | --- |
| ​  | `if`(currentNode.value === valueToDelete) { |
| ​  | nodeToDelete = currentNode; |
| ​  | `break`; |
| ​  | } |
| ​  |  |
| ​  | parentOfCurrentNode = currentNode; |
| ​  | `if`(valueToDelete < currentNode.value) { |
| ​  | currentNode = currentNode.leftChild; |
| ​  | } `else` `if`(valueToDelete > currentNode.value) { |
| ​  | currentNode = currentNode.rightChild; |
| ​  | } |
| ​  | } |

这个代码片段在树中向下移动，随着我们搜索`valueToDelete`更新`currentNode`。如果我们没有找到它（当值不在树中时就是这种情况），循环会因`currentNode`为`null`而自动终止。

然而，如果我们找到了`valueToDelete`，我们将`currentNode`声明为`nodeToDelete`并退出循环。注意，我们还跟踪`parentOfCurrentNode`，它现在是我们将要删除的节点的父节点。

接下来，我们有这个代码片段：

| ​  | `if`(!nodeToDelete) { `return` `null`; } |
| --- | --- |

如果我们想要删除的值根本不在树中，则返回`null`。

该方法的其余部分执行实际的删除操作。我们首先处理最复杂的情况，即我们要删除的节点有两个子节点：

| ​  | `if`(nodeToDelete.leftChild && nodeToDelete.rightChild) { |
| --- | --- |
| ​  | replaceWithSuccessorNode(nodeToDelete); |
| ​  | } |

在这里，我们将重任外包给`replaceWithSuccessorNode`辅助方法，稍后我们会分析它。与此同时，让我们继续。

接下来，我们处理被删除节点有0个或1个子节点的情况：

| ​  | `else` { |
| --- | --- |
| ​  | `childOfDeletedNode = (nodeToDelete.leftChild | | nodeToDelete.rightChild);` |
| ​  |  |
| ​  | `if (!parentOfCurrentNode) {` |
| ​  | `nodeToDelete.value = childOfDeletedNode.value;` |
| ​  | `nodeToDelete.leftChild = childOfDeletedNode.leftChild;` |
| ​  | `nodeToDelete.rightChild = childOfDeletedNode.rightChild;` |
| ​  | `} else if (nodeToDelete === parentOfCurrentNode.leftChild) {` |
| ​  | `parentOfCurrentNode.leftChild = childOfDeletedNode;` |
| ​  | `} else if (nodeToDelete === parentOfCurrentNode.rightChild) {` |
| ​  | `parentOfCurrentNode.rightChild = childOfDeletedNode;` |
| ​  | `}` |
| ​  | `}` |

在这里，我们首先设置一个新变量`childOfDeletedNode`，表示被删除节点的子节点。如果被删除的节点没有子节点，则此变量将被设置为`null`。这个变量至关重要，因为在删除我们的`nodeToDelete`时，我们需要将其子节点放置在被删除节点原本的位置。

而这正是上面代码在两个`else if`子句中所做的。它确定被删除的节点是其父节点的左子节点还是右子节点，并相应地将`childOfDeletedNode`附加到被删除节点的父节点上。

`if`语句中的第一个子句处理删除根节点的情况。为了确保我们将被删除根节点的子节点标记为新根，我们用其子节点覆盖根节点。

这带我们到了方法的最后一行，它简单地返回被删除的节点，以防我们想将其用于其他目的：

| ​  | `return nodeToDelete;` |
| --- | --- |

现在我们回到被删除节点有两个子节点的情况。我们之前的代码调用了辅助方法 `replaceWithSuccessorNode`，现在我们来逐步分析它。

调用此方法时，我们传入要删除的节点，该节点将被称为 `node`。

接下来，我们使用以下代码识别后继节点：

| ​  | `let successorNode = node.rightChild;` |
| --- | --- |
| ​  | `let parentOfSuccessorNode;` |
| ​  |  |
| ​  | `if (!successorNode.leftChild) {` |
| ​  | `node.value = successorNode.value;` |
| ​  | `node.rightChild = successorNode.rightChild;` |
| ​  | `return;` |
| ​  | `}` |
| ​  |  |
| ​  | `while (successorNode.leftChild) {` |
| ​  | `parentOfSuccessorNode = successorNode;` |
| ​  | `successorNode = successorNode.leftChild;` |
| ​  | `}` |

在这里，我们从被删除节点的右子节点开始，然后沿着左子节点向下移动，直到无法再继续。最底部的节点就是我们的后继节点。我们还跟踪后继节点的父节点。

然而，在后继节点恰好是被删除节点的右子节点的情况下（当被删除节点的右子节点没有左子节点时会发生这种情况），我们只需将后继节点放入被删除节点的位置。如果是这种情况，这就是我们所需的全部操作。但如果后继节点是其父节点的左子节点，我们就继续。

接下来，我们从其位置中移除后继节点：

| ​  | `if` (successorNode.rightChild) { |
| --- | --- |
| ​  | `parentOfSuccessorNode.leftChild = successorNode.rightChild;` |
| ​  | } `else` { |
| ​  | `parentOfSuccessorNode.leftChild = null;` |
| ​  | } |

我们的代码处理了两种可能的情况。第二种情况（在 `else` 子句中）是较简单的情况，即后继节点没有子节点。在这种情况下，我们通过将后继节点替换为 `null` 来删除它。

在更复杂的情况下，如果后继节点有右子节点，我们将右子节点放在后继节点原来的位置。

我们已经成功地从树中移除了后继节点，但还有一步关键的操作。请记住，我们最初并不打算删除后继节点。我们整个目标是删除树中更高位置的 `node`。

为了实现这一点，我们将后继节点插入要删除节点的位置：

| ​  | `node.value = successorNode.value;` |
| --- | --- |

请注意，我们并不直接插入实际的后继节点；相反，我们仅用其值覆盖 `node` 的值，有效地删除了 `node`。

就这样！这是一个旅程，但我们做到了。

### 二叉搜索树删除的效率

与搜索和插入一样，从树中删除节点通常也是 `O(log N)`。这是因为删除操作需要搜索以及一些额外步骤来处理任何悬挂的子节点。与此相比，从有序数组中删除一个值的复杂度是 `O(N`)，因为需要向左移动元素以填补被删除值的空缺。
