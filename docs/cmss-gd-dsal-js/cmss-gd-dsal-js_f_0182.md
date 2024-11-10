## `深度优先搜索`

图搜索的两种著名方法是深度优先搜索和广度优先搜索。这两种方法都能完成任务，但在特定情况下各自提供独特的优势。我们将首先介绍深度优先搜索，也称为`DFS`，因为它实际上与我们之前讨论的`二叉树遍历`的算法非常相似。实际上，它也是我们在`文件系统遍历`中看到的同一基本算法。

如前所述，图搜索可以用来找到特定顶点或简单地遍历图形。我们将首先使用深度优先搜索来遍历图，因为该算法稍微简单一些。

任何图搜索算法的关键是跟踪我们到目前为止访问过的顶点。如果我们不这样做，可能会陷入无限循环。以下图形就是一个例子：

![images/graphs/cycle_graph.png](images/graphs/cycle_graph.png)

在这里，`Mohammad`与`Felicia`是朋友。`Felicia`也恰好与`Zeina`是朋友。但是`Zeina`与`Mohammad`是朋友。因此，除非我们跟踪已经遍历的顶点，否则我们的代码会陷入循环。

当我们处理树（或文件系统遍历）时，这个问题并不存在，因为树不能有循环。但由于图可以有循环，我们现在需要解决这个问题。

跟踪我们已访问的顶点的一种方法是使用哈希表。当我们访问每个顶点时，将顶点（或其值）作为哈希表中的键，并为其分配一个任意值，如布尔值`true`。如果某个顶点在哈希表中，则意味着我们已经访问过它。

考虑到这一点，深度优先搜索算法的工作方式如下。

1.  从图中的任何随机顶点开始。

1.  将当前顶点添加到哈希表中，以标记它为已访问。

1.  遍历当前顶点的相邻顶点。

1.  对于每个相邻顶点，如果该相邻顶点已经被访问过，则忽略它。

1.  如果相邻顶点尚未被访问，则对该顶点递归执行深度优先搜索。

### `深度优先搜索演示`

让我们看看这如何实现。

在这个演示中，我们将从`Alice`开始。在下面的图示中，带有线条的顶点是当前顶点。一个勾号意味着我们已经正式标记该顶点为已访问（并添加到哈希表中）。

步骤 1：我们从`Alice`开始，并给她一个勾号以表示我们已经正式访问了她的顶点：

![images/graphs/visited_alice.png](images/graphs/visited_alice.png)

接下来，我们将使用循环遍历`Alice`的邻居。这些邻居将是`Bob`、`Candy`、`Derek`和`Elaine`。

访问邻居的顺序无关紧要，所以我们就从`Bob`开始吧。他看起来很好。

第二步：我们现在对`Bob`执行深度优先搜索。请注意，这个调用是递归的，因为我们已经在`Alice`的深度优先搜索中。

与所有递归一样，计算机需要记住它仍在进行哪些函数调用，因此它首先将`Alice`添加到调用栈中：

![`images/graphs/alice_call_stack.png`](images/graphs/alice_call_stack.png)

我们现在可以开始对`Bob`进行深度优先搜索，这使得`Bob`成为当前顶点。我们将他标记为已访问，如图所示[graph](#fig.ch18.visit_bob)。

![`images/graphs/visit_bob.png`](images/graphs/visit_bob.png)

然后我们遍历`Bob`的相邻顶点。这些是`Alice`和`Fred`。

第三步：`Alice`已经被访问过，所以我们可以忽略她。

第四步：唯一的另一个邻居是`Fred`。我们在`Fred`的顶点上调用深度优先搜索函数。计算机首先将`Bob`添加到调用栈，以记住它仍在对`Bob`进行搜索：

![`images/graphs/bob_call_stack.png`](images/graphs/bob_call_stack.png)

我们现在对`Fred`执行深度优先搜索。他现在是当前顶点，所以我们将他标记为已访问：

![`images/graphs/visit_fred.png`](images/graphs/visit_fred.png)

接下来，我们遍历`Fred`的相邻顶点，它们是`Bob`和`Helen`。

第五步：`Bob`已经被访问过，所以我们忽略他。

第六步：唯一剩下的相邻顶点是`Helen`。我们递归地首先对`Helen`执行深度搜索，因此计算机首先将`Fred`添加到调用栈中：

![`images/graphs/fred_call_stack.png`](images/graphs/fred_call_stack.png)

我们现在开始对`Helen`进行深度优先搜索。她是当前顶点，所以我们将她标记为已访问：

![`images/graphs/visit_helen.png`](images/graphs/visit_helen.png)

`Helen`有两个相邻顶点：`Fred`和`Candy`。

第七步：我们已经访问过`Fred`，所以我们可以忽略他。

步骤8：`Candy`尚未被访问，因此我们对`Candy`执行递归的深度优先搜索。然而，首先，`Helen`被添加到调用栈中：

![`images/graphs/helen_call_stack.png`](images/graphs/helen_call_stack.png)

我们对`Candy`执行深度优先搜索。她现在是当前顶点，我们将她标记为已访问：

![`images/graphs/visit_candy.png`](images/graphs/visit_candy.png)

`Candy`有两个相邻顶点：`Alice`和`Helen`。

步骤9：我们已经访问过`Alice`，所以可以忽略她。

步骤10：我们已经访问过`Helen`，所以也可以忽略她。

由于`Candy`没有其他邻居，我们完成了对`Candy`的深度优先搜索。此时，计算机开始撤销调用栈。

首先，它从调用栈中弹出`Helen`。我们已经遍历过她的所有邻居，因此对`Helen`的深度优先搜索已完成。

计算机弹出了`Fred`。我们也遍历过了他所有的邻居，因此也完成了对他的搜索。

计算机弹出了`Bob`，但我们也完成了对他的处理。

计算机随后将`Alice`从调用栈中弹出。在我们搜索`Alice`的过程中，我们正在循环遍历`Alice`的所有邻居。现在，这个循环已经遍历过`Bob`。（这是步骤2。）这留下了`Candy`、`Derek`和`Elaine`。

步骤11：`Candy`已经被访问过，所以没有必要对她进行搜索。

然而，我们还没有访问`Derek`或`Elaine`。

步骤12：让我们通过递归地对`Derek`执行深度优先搜索来进行。计算机再次将`Alice`添加到调用栈中：

![`images/graphs/alice_call_stack.png`](images/graphs/alice_call_stack.png)

`Derek`的深度优先搜索现在开始。`Derek`是当前顶点，因此我们将他标记为已访问：

![`images/graphs/visit_derek.png`](images/graphs/visit_derek.png)

`Derek`有三个相邻顶点：`Alice`、`Elaine`和`Gina`。

步骤13：`Alice`已经被访问过，因此我们不需要对她进行另一次搜索。

步骤14：接下来让我们访问`Elaine`，通过递归地对她的顶点执行深度优先搜索。在我们执行之前，计算机将`Derek`添加到调用栈中：

![`images/graphs/derek_call_stack.png`](images/graphs/derek_call_stack.png)

我们现在对`Elaine`执行深度优先搜索。我们将`Elaine`标记为已访问，如图所示[graph](#fig.ch18.visit_elaine)。

![`images/graphs/visit_elaine.png`](images/graphs/visit_elaine.png)

`Elaine`有两个相邻顶点：`Alice`和`Derek`。

步骤15：`Alice`已经被访问过，因此没有必要再对她进行一次搜索。

步骤16：`Derek`也已经被访问过。

由于我们已经遍历了所有`Elaine`的邻居，因此我们完成了对`Elaine`的搜索。计算机现在从调用栈中弹出`Derek`，并遍历他剩余的相邻顶点。在这种情况下，`Gina`是最后一个要访问的邻居。

步骤17：我们之前从未访问过`Gina`，所以我们对她的顶点递归地执行深度优先搜索。不过，计算机首先再次将`Derek`添加到调用栈中：

![`images/graphs/derek_call_stack.png`](images/graphs/derek_call_stack.png)

我们开始对`Gina`进行深度优先搜索，并将她标记为已访问，如图所示[graph](#fig.ch18.visit_gina)。

![`images/graphs/visit_gina.png`](images/graphs/visit_gina.png)

`Gina`有两个邻居：`Derek`和`Irena`。

步骤18：`Derek`已经被访问过。

步骤19：`Gina`有一个未访问的相邻顶点——即`Irena`。`Gina`被添加到调用栈中，以便我们可以递归地对`Irena`执行深度优先搜索：

![`images/graphs/gina_call_stack.png`](images/graphs/gina_call_stack.png)

我们开始对`Irena`进行搜索，并将她标记为已访问：

![`images/graphs/visit_irena.png`](images/graphs/visit_irena.png)

我们遍历`Irena`的邻居。`Irena`只有一个邻居：`Gina`。

步骤20：`Gina`已经被访问过。

计算机随后逐个弹出调用栈，依次将每个顶点弹出。然而，由于调用栈中的每个顶点已经遍历过它的所有邻居，计算机对每个顶点没有更多操作。

这意味着我们完成了！

### 代码实现：深度优先搜索

-   下面是深度优先遍历的实现：

| ​  | ​`function`​ `dfsTraverse(vertex, visitedVertices={})` { |
| --- | --- |
| ​  | `visitedVertices[vertex.value]` = ​`true`​; |
| ​  |  |
| ​  | `console.log(vertex.value);` |
| ​  |  |
| ​  | ​`for`​ (​`const`​ `adjacentVertex` ​`of`​ `vertex.adjacentVertices`) { |
| ​  | ​`if`​ (!`visitedVertices[adjacentVertex.value]`) { |
| ​  | `dfsTraverse(adjacentVertex, visitedVertices);` |
| ​  | } |
| ​  | } |
| ​  | } |

-   我们的`dfsTraverse`方法接受一个单独的顶点和一个`visitedVertices`哈希表。第一次调用这个`function`时，`visitedVertices`默认为一个空的哈希表。对于上述示例，我们将从`alice`顶点开始执行深度优先遍历，过程如下：

| ​  | `dfsTraverse(alice);` |
| --- | --- |

-   当我们访问顶点时，我们会将已访问的顶点填充到这个哈希表中，并在每次递归调用中传递相同的哈希表。

-   在`function`内我们做的第一件事是将当前顶点标记为已访问。我们通过将顶点的值添加到哈希中来实现这一点：

| ​  | `visitedVertices[vertex.value]` = ​`true`​; |
| --- | --- |

-   然后我们可选地打印顶点的值，以便反馈我们确实遍历了它：

| ​  | `console.log(vertex.value);` |
| --- | --- |

-   接下来，我们迭代当前顶点的所有相邻顶点：

| ​  | ​`for`​ (​`const`​ `adjacentVertex` ​`of`​ `vertex.adjacentVertices`) { |
| --- | --- |

-   我们检查每个相邻顶点，看它是否已经被访问。如果已访问，我们什么也不做；但如果从未被访问，我们就递归调用`dfsTraverse`，传入该相邻顶点：

| ​  | ​`if`​ (!`visitedVertices[adjacentVertex.value]`) { |
| --- | --- |
| ​  | `dfsTraverse(adjacentVertex, visitedVertices);` |
| ​  | } |

-   同样，我们也传入`visitedVertices`哈希表，以便后续调用可以访问它。

-   如果我们想使用深度优先搜索来搜索特定顶点，可以使用之前`function`的修改版：

| ​  | ​`function`​ `dfs(vertex, searchValue, visitedVertices={})` { |
| --- | --- |
| ​  | `visitedVertices[vertex.value]` = ​`true`​; |
| ​  |  |
| ​  | ​`if`​ (`vertex.value` === `searchValue`) { ​`return`​ `vertex`; } |
| ​  |  |
| ​  | ​`for`​ (​`const`​ `adjacentVertex` ​`of`​ `vertex.adjacentVertices`) { |
| ​  | ​`if`​ (`adjacentVertex.value` === `searchValue`) { |
| ​  | ​`return`​ `adjacentVertex;` |
| ​  | } |
| ​  |  |
| ​  | ​`if`​ (!`visitedVertices[adjacentVertex.value]`) { |
| ​  | ​`const`​ `vertexWeAreSearchingFor` = |
| ​  | `dfs(adjacentVertex, searchValue, visitedVertices);` |
| ​  |  |
| ​  | ​`if`​ (`vertexWeAreSearchingFor`) { |
| ​  | ​`return`​ `vertexWeAreSearchingFor;` |
| ​  | } |
| ​  | } |
| ​  | } |
| ​  |  |
| ​  | ​`return`​ ​`null`​; |
| ​  | } |

-   这个实现也会递归调用自身，对于每个顶点，如果找到正确的顶点，则返回`vertexWeAreSearchingFor`。
