## 二叉搜索树遍历

现在，我们已经看到了如何在二叉搜索树中搜索、插入和删除数据。不过，我提到过，我们还希望能够以字母顺序打印整个书名列表。我们该如何做到呢？

首先，我们需要能够访问树中的每一个节点。访问节点是访问它们的另一种说法。在数据结构中访问每个节点的过程称为遍历数据结构。

其次，我们需要确保按字母升序遍历树，以便能够以该顺序打印列表。你可以以多种方式遍历树，但对于这个应用程序，我们将执行所谓的中序遍历，以便能按字母顺序打印每个标题。

递归是执行遍历的一个很好的工具。我们将创建一个递归函数叫做`traverse`，可以在特定节点上调用。该函数接下来执行以下步骤：

1.  递归地调用自身（`traverse`）在节点的左子节点上。该函数将不断被调用，直到我们遇到一个没有左子节点的节点。

1.  访问该节点。（对于我们的书名应用程序，我们在此步骤中打印节点的值。）

1.  递归地调用自身（`traverse`）在节点的右子节点上。该函数将不断被调用，直到我们遇到一个没有右子节点的节点。

对于这个递归算法，基例是当我们在不存在的子节点上调用`traverse`，此时我们将返回而不再进行任何操作。

这是一个适用于我们书名列表的JavaScript `traverseAndPrint`函数。注意它是多么简洁：

| ​  | ​`function`​ `traverseAndPrint(node)` { |
| --- | --- |
| ​  | ​`if`​ (!node) { ​`return`​; } |
| ​  |  |
| ​  | `traverseAndPrint(node.leftChild);` |
| ​  | `console.log(node.value);` |
| ​  | `traverseAndPrint(node.rightChild);` |
| ​  | } |

让我们逐步了解中序遍历。

我们首先在“Moby Dick”上调用`traverseAndPrint`。这将反过来调用`traverseAndPrint`在“Moby Dick”的左子节点上，左子节点是“Great Expectations”：

| ​  | `traverseAndPrint(node.leftChild);` |
| --- | --- |

不过在继续之前，我们需要将“我们正在处理‘Moby Dick’函数”的事实以及“我们正在遍历它的左子节点”的事实添加到调用栈中：

![images/binary_trees/call_stack_1.png](images/binary_trees/call_stack_1.png)

然后，我们继续执行`traverseAndPrint("Great Expectations")`，这将调用`traverse_and_print`在“Great Expectations”的左子节点上，左子节点是“Alice in Wonderland”。

在继续之前，让我们将`traverseAndPrint("Great Expectations")`添加到调用栈中：

![images/binary_trees/call_stack_2.png](images/binary_trees/call_stack_2.png)

`traverseAndPrint("Alice in Wonderland")`在“Alice in Wonderland”的左子节点上调用`traverseAndPrint`。然而，那里没有左子节点（基准情况），所以什么也不会发生。`traverseAndPrint`的下一行是：

| ​  | `console.log(node.value);` |
| --- | --- |

这一行打印“Alice in Wonderland”。

接下来，函数尝试对“Alice in Wonderland”的右子节点进行`traverseAndPrint`：

| ​  | `traverseAndPrint(node.rightChild);` |
| --- | --- |

然而，没有右子节点（基本情况），因此函数返回而不再执行其他操作。

由于我们已经完成了`traverseAndPrint("Alice in Wonderland")`函数，我们检查调用栈，以查看我们在这个递归状态中的进展：

![`images/binary_trees/call_stack_3.png`](images/binary_trees/call_stack_3.png)

啊，对了。我们正处于`traverseAndPrint("Great Expectations")`的中间，刚完成了对它的左子节点的`traverseAndPrint`调用。让我们将其从调用栈中弹出：

![`images/binary_trees/call_stack_4.png`](images/binary_trees/call_stack_4.png)

让我们继续。这个函数接下来打印“Great Expectations”，然后调用`traverseAndPrint`对右子节点进行操作，即“Lord of the Flies”。不过在继续之前，让我们在调用栈中保持这个函数的位置：

![`images/binary_trees/call_stack_5.png`](images/binary_trees/call_stack_5.png)

我们现在执行`traverseAndPrint("Lord of the Flies")`。首先，我们对它的左子节点调用`traverseAndPrint`，但它没有左子节点。接着，我们打印“Lord of the Flies”。最后，我们对它的右子节点调用`traverseAndPrint`，但也没有，所以这个函数现在完成了。

我们查看调用栈，发现我们正在对“Great Expectations”的右子节点执行`traverseAndPrint`。我们可以将其从栈中弹出并继续，如[图示](#fig.ch15.call_stack_6)所示。

![`images/binary_trees/call_stack_6.png`](images/binary_trees/call_stack_6.png)

现在，恰好我们已经完成了在`traverseAndPrint("Great Expectations")`中的所有操作，所以我们可以返回到调用栈查看接下来要做什么：

![`images/binary_trees/call_stack_7.png`](images/binary_trees/call_stack_7.png)

我们可以看到，我们正处于对“Moby Dick”的左子节点进行`traverseAndPrint`的中间。我们可以将其从调用栈中弹出（这使得栈现在为空），并继续进行`traverseAndPrint("Moby Dick")`中的下一步，即打印“Moby Dick”。

然后，我们对“Moby Dick”的右子节点调用`traverseAndPrint`。我们将其添加到调用栈中：

![`images/binary_trees/call_stack_8.png`](images/binary_trees/call_stack_8.png)

为了简洁起见（尽管可能已经太晚了），我将让你从这里继续走完剩下的`traverseAndPrint`函数。

到我们函数执行完毕时，我们将以如下顺序打印节点：

![`images/binary_trees/bst_27.png`](images/binary_trees/bst_27.png)

这就是我们以字母顺序打印书名的目标。请注意，树遍历是O(N)的，因为按定义，遍历会访问树的所有N个节点。
