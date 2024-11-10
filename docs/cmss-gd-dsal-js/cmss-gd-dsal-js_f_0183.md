## `广度优先搜索`

`广度优先搜索`，通常缩写为`BFS`，是另一种搜索图的方法。与深度优先搜索不同，`广度优先搜索`不使用递归。相反，算法围绕我们的老朋友——队列。正如你所记得的，队列是一种`FIFO`数据结构，先入先出。

让我们看看广度优先搜索的算法。与我们的深度优先搜索的演示一样，我们将专注于使用广度优先搜索进行图的遍历；也就是说，我们将访问我们示例社交网络中的每个顶点。

这是`BFS`遍历算法：

1.  从图中的任何顶点开始。我们将其称为起始顶点。

1.  将起始顶点添加到哈希表中，以标记其已被访问。

1.  将起始顶点添加到队列中。

1.  开始一个循环，只要队列不为空就运行。

1.  在这个循环中，从队列中移除第一个顶点。我们将其称为当前顶点。

1.  遍历当前顶点的所有邻接顶点。

1.  如果邻接顶点已经被访问，则忽略它。

1.  如果邻接顶点尚未被访问，通过将其添加到哈希表中来标记为已访问，并将其添加到队列中。

1.  重复此循环（从第四步开始），直到队列为空。

### `广度优先搜索演示`

这并没有看起来那么复杂。让我们逐步走过遍历过程。

为了设置，让我们将`Alice`作为我们的起始顶点。我们将她标记为已访问并添加到队列中：

![images/graphs/visit_and_queue_alice.png](images/graphs/visit_and_queue_alice.png)

我们现在开始核心算法。

第一步：我们从队列中移除第一个顶点并将其设为当前顶点。这将是`Alice`，因为她此时是队列中唯一的项。所以此时队列为空。

由于`Alice`是当前顶点，我们继续遍历`Alice`的邻接顶点。

第二步：我们将从`Bob`开始。我们将他标记为已访问并添加到队列中：

![images/graphs/visit_and_queue_bob.png](images/graphs/visit_and_queue_bob.png)

请注意，`Alice`仍然是当前顶点，如周围的线所示。然而，我们仍然将`Bob`标记为已访问并将他添加到队列中。

第三步：我们继续处理`Alice`的其他邻接顶点。让我们选择`Candy`；我们将她标记为已访问并添加到队列中：

![images/graphs/visit_and_queue_candy.png](images/graphs/visit_and_queue_candy.png)

第四步：然后我们将`Derek`标记为已访问并添加到队列中：

![images/graphs/visit_and_queue_derek.png](images/graphs/visit_and_queue_derek.png)

第五步：我们对`Elaine`也做同样的处理：

![images/graphs/visit_and_queue_elaine.png](images/graphs/visit_and_queue_elaine.png)

第6步：现在我们已经遍历了当前顶点（`Alice`）的所有邻居，我们从队列中删除第一个项目并使其成为当前顶点。在我们的案例中，`Bob`在队列的前面，所以我们将他出队并使他成为当前顶点，如[图](#fig.ch18.dequeue_bob)所示。

![`images/graphs/dequeue_bob.png`](images/graphs/dequeue_bob.png)

由于`Bob`是当前顶点，我们将遍历他的所有相邻顶点。

第7步：Alice已经被访问过，所以我们忽略她。

第8步：`Fred`尚未被访问，因此我们将他标记为已访问并将他添加到队列中：

![`images/graphs/visit_and_queue_fred.png`](images/graphs/visit_and_queue_fred.png)

第9步：`Bob`没有更多的相邻顶点。这意味着我们将队列中的第一个项目取出，并使其成为当前顶点。这将是`Candy`：

![`images/graphs/dequeue_candy.png`](images/graphs/dequeue_candy.png)

我们遍历`Candy`的相邻顶点。

第10步：`Alice`已经被访问过，所以我们再次忽略她。

第11步：另一方面，Helen尚未被访问。我们将`Helen`标记为已访问并将她添加到队列中：

![`images/graphs/visit_and_queue_helen.png`](images/graphs/visit_and_queue_helen.png)

第12步：我们完成了遍历`Candy`的相邻顶点，因此我们从队列中取出第一个项目（`Derek`），并使其成为当前顶点：

![`images/graphs/dequeue_derek.png`](images/graphs/dequeue_derek.png)

`Derek`有三个相邻顶点，所以我们遍历它们。

第13步：`Alice`已经被访问过，所以我们忽略她。

第14步：`Elaine`也是如此。

第15步：这留下了`Gina`，所以我们将她标记为已访问，并将她添加到队列中：

![`images/graphs/visit_and_queue_gina.png`](images/graphs/visit_and_queue_gina.png)

第16步：我们已经访问了Derek的所有直接朋友，因此我们将Elaine从队列中取出并指定她为当前顶点：

![`images/graphs/dequeue_elaine.png`](images/graphs/dequeue_elaine.png)

第17步：我们遍历`Elaine`的相邻顶点，从`Alice`开始。不过，她已经被访问过了。

第18步：我们也已经访问过`Derek`。

第19步：我们从队列中取出下一个人（`Fred`）并将他转变为当前顶点：

![`images/graphs/dequeue_fred.png`](images/graphs/dequeue_fred.png)

第20步：我们遍历`Fred`的邻居。`Bob`已经被访问过。

第21步：`Helen`也已经被访问过。

第22步：由于`Helen`在队列的前面，我们将`Helen`出队并使她成为当前顶点：

![`images/graphs/dequeue_helen.png`](images/graphs/dequeue_helen.png)

第23步：`Helen`有两个相邻顶点。我们已经访问过`Fred`。

第24步：我们也已经访问过`Candy`。

第25步：我们从队列中移除`Gina`并使她成为当前顶点：

![`images/graphs/dequeue_gina.png`](images/graphs/dequeue_gina.png)

第26步：我们遍历`Gina`的邻居。`Derek`已经被访问过。

第27步：`Gina` 有一个未访问的相邻朋友 `Irena`，因此我们访问 `Irena` 并将她添加到队列中：

![`images/graphs/visit_and_queue_irena.png`](images/graphs/visit_and_queue_irena.png)

我们现在已经完成对 Gina 邻居的遍历。

第28步：我们从队列中移除第一个（也是唯一的）元素 `Irena`。她成为当前顶点：

![`images/graphs/dequeue_irena.png`](images/graphs/dequeue_irena.png)

第29步：Irena 只有一个相邻顶点 Gina，但 Gina 已经被访问过了。

我们现在应该移除队列中的下一个元素，但队列是空的！这意味着我们的遍历已完成。

### 代码实现：广度优先搜索

这是我们用于广度优先遍历的代码：

| ​  | `import` Queue `from` `'./queue_implementation.js'`; |
| --- | --- |
| ​  |  |
| ​  | `function` bfsTraverse(startingVertex) { |
| ​  | `const` queue = `new` Queue(); |
| ​  |  |
| ​  | `const` visitedVertices = {}; |
| ​  | visitedVertices[startingVertex.value] = `true`; |
| ​  | queue.enqueue(startingVertex); |
| ​  |  |
| ​  | `while` (queue.read()) { |
| ​  | `const` currentVertex = queue.dequeue(); |
| ​  | console.log(currentVertex.value); |
| ​  |  |
| ​  | `for` (`const` adjacentVertex `of` currentVertex.adjacentVertices) { |
| ​  | `if` (!visitedVertices[adjacentVertex.value]) { |
| ​  | visitedVertices[adjacentVertex.value] = `true`; |
| ​  | queue.enqueue(adjacentVertex); |
| ​  | } |
| ​  | } |
| ​  | } |
| ​  | } |

我们首先导入一个 Queue 模块。这就是我们在 [`队列实现`](f_0092.xhtml#queue.implementation) 中创建的相同队列实现。

`bfsTraverse` 方法接受一个 startingVertex，这是我们搜索的起始顶点。

我们首先创建一个用于支持算法的队列：

| ​  | `const` queue = `new` Queue(); |
| --- | --- |

我们还创建了 visitedVertices 哈希表，用于跟踪我们已经访问过的顶点：

| ​  | `const` visitedVertices = {}; |
| --- | --- |

然后我们将 startingVertex 标记为已访问并将其添加到队列中：

| ​  | visitedVertices[startingVertex.value] = `true`; |
| --- | --- |
| ​  | queue.enqueue(startingVertex); |

我们开始一个循环，只要队列不为空就继续：

| ​  | `while` (queue.read()) { |
| --- | --- |

我们从队列中移除第一个元素，并将其设为当前顶点：

| ​  | `const` currentVertex = queue.dequeue(); |
| --- | --- |

接下来，我们打印顶点的值，以便在控制台中查看我们的遍历是否正常工作：

| ​  | console.log(currentVertex.value); |
| --- | --- |

然后我们遍历当前顶点的所有相邻顶点：

| ​  | `for` (`const` adjacentVertex `of` currentVertex.adjacentVertices) { |
| --- | --- |

对于每个尚未访问的相邻顶点，我们将其添加到哈希表中以标记为已访问，然后将其添加到队列中：

| ​  | `if` (!visitedVertices[adjacentVertex.value]) { |
| --- | --- |
| ​  | visitedVertices[adjacentVertex.value] = `true`; |
| ​  | queue.enqueue(adjacentVertex); |
| ​  | } |

这就是其要点。

### DFS 与 BFS

如果你仔细观察广度优先搜索的顺序，你会注意到我们首先遍历了Alice的所有直接连接。然后我们螺旋向外，逐渐远离Alice。然而在深度优先搜索中，我们会立即尽可能远离Alice，直到不得不返回她那里。

所以我们有两种搜索图的方法：`深度优先`和`广度优先`。哪种方法更好呢？

正如你现在可能已经意识到的，这取决于你的具体情况。在某些场景中，`深度优先`可能更快，而在其他场景中，`广度优先`可能是更好的选择。

通常，决定使用哪种算法的主要因素之一是你所搜索的图的性质以及你在寻找什么。这里的关键是，正如前面提到的，`广度优先搜索`会在移动到更远处之前遍历所有离起始顶点最近的顶点。而`深度优先搜索`则会立即尽可能远离起始顶点，只有在搜索到达死胡同时才会返回起始顶点。

所以假设我们想找到一个社交网络中一个人的所有直接连接。例如，我们可能想在之前的示例图中找到所有`Alice`的实际朋友。我们不关心她朋友的朋友是谁——我们只想要她直接连接的列表。

如果你查看`广度优先搜索`，你会发现我们首先找到了`Alice`的所有直接朋友（`Bob`，`Candy`，`Derek`，和`Elaine`），然后才移动到她的“二级”关系。

然而，当我们使用`深度优先算法`遍历图时，我们最终会接触到`Fred`和`Helen`（两个不是`Alice`朋友的人），才找到`Alice`的其他朋友。在一个更大的图中，我们可能会浪费更多的时间遍历许多不必要的顶点。

但是让我们考虑另一种情况。假设我们的图表示一个家谱，可能如下所示：

![`images/graphs/family_tree.png`](images/graphs/family_tree.png)

这个家谱显示了所有`伟大祖母Ruby`的后代，她是一位了不起的家庭家长。假设我们知道`Ruth`是`Ruby`的一个曾孙女，我们想在图中找到`Ruth`。

现在，有一件事。如果我们使用`广度优先搜索`，我们最终会遍历所有的Ruby的孩子和孙子，才会到达第一个曾孙女。

然而，如果我们使用`深度优先搜索`，我们会立即向下移动图，仅需几步就能到达第一个曾孙女。虽然可能需要遍历整个图才能找到`Ruth`，但我们至少有机会快速找到她。而使用`广度优先搜索`，我们没有选择，必须遍历所有非大孙子才能开始检查大孙子。

因此，始终要问的问题是，我们在搜索过程中是否希望靠近起始顶点，还是特别想要远离。`广度优先搜索`适合保持接近，而`深度优先搜索`则非常适合快速远离。
