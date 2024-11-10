## 第18章

这些是“[练习](f_0188.xhtml#graphs.exercises)”部分中的习题解决方案。

1.  如果用户正在浏览“指甲”，网站会推荐“指甲油”、“针”、“别针”和“锤子”。

1.  深度优先搜索的顺序为A-B-E-J-F-O-C-G-K-D-H-L-M-I-N-P，如下图所示：

    ![images/graphs/solution_2_graph.png](images/graphs/solution_2_graph.png)

1.  广度优先搜索的顺序为A-B-C-D-E-F-G-H-I-J-K-L-M-N-O-P，如下图所示：

    ![images/graphs/solution_3_graph.png](images/graphs/solution_3_graph.png)

1.  以下是广度优先搜索的实现：

    | ​  | `import` Queue `from` `./queue_implementation.js`; |
    | --- | --- |
    | ​  |  |
    | ​  | `function` bfs(startingVertex, searchValue) { |
    | ​  | `const` queue = `new` Queue(); |
    | ​  | `const` visitedVertices = {}; |
    | ​  | visitedVertices[startingVertex.value] = `true`; |
    | ​  | queue.enqueue(startingVertex); |
    | ​  |  |
    | ​  | `while` (queue.read()) { |
    | ​  | `const` currentVertex = queue.dequeue(); |
    | ​  | `if` (currentVertex.value === searchValue) { |
    | ​  | `return` currentVertex; |
    | ​  | } |
    | ​  |  |
    | ​  | `for` (`const` adjacentVertex `of` currentVertex.adjacentVertices) { |
    | ​  | `if` (!visitedVertices[adjacentVertex.value]) { |
    | ​  | visitedVertices[adjacentVertex.value] = `true`; |
    | ​  | queue.enqueue(adjacentVertex); |
    | ​  | } |
    | ​  | } |
    | ​  | } |
    | ​  |  |
    | ​  | `return`​ `null`; |
    | ​  | } |

1.  在无权图中寻找最短路径，我们将使用广度优先搜索。广度优先搜索的主要特点是尽可能长时间保持靠近起始顶点。这个特点将作为找到最短路径的关键。

    让我们将其应用于我们的社交网络示例。由于广度优先搜索尽可能长时间保持靠近Idris，我们最终会通过最短路径首先找到Lina。只有在搜索的后期，我们才会通过较长的路径找到Lina。实际上，我们甚至可以在找到Lina后立即停止搜索。（以下实现并不会提前结束，但你可以修改它以实现这一点。）

    当我们第一次访问每个顶点时，我们知道当前顶点始终是从起始顶点到我们正在访问的顶点的最短路径的一部分。（记住，对于广度优先搜索，当前顶点和我们正在访问的顶点不一定相同。）

    例如，当我们第一次访问Lina时，Kamil将是当前顶点。这是因为在广度优先搜索中，我们将通过Kamil先到达Lisa，然后才通过Sasha到达她。当我们访问Lina（通过Kamil）时，我们可以在表中记录从Idris到Lina的最短路径将通过Kamil。这个表类似于Dijkstra算法中的`cheapestPreviousStopoverCityTable`。

    - 实际上，每当我们访问任何顶点时，从伊德里斯到该顶点的最短路径将经过当前顶点。我们会将所有这些数据存储在一个名为`previousVertexTable`的表中。

    - 最后，我们可以使用这些数据从莉娜回溯到伊德里斯，构建两者之间的精确最短路径。

- 这是我们的实现：

| ​  | `import` Queue `from` *'./queue_implementation.js'*; |
| --- | --- |
| ​  |  |
| ​  | `function` findShortestPath(`firstVertex`, `secondVertex`, `visitedVertices`) { |
| ​  | `const` queue = `new` Queue(); |
| ​  | `const` previousVertexTable = {}; |
| ​  |  |
| ​  | visitedVertices[`firstVertex.value`] = `true`; |
| ​  | queue.enqueue(`firstVertex`); |
| ​  |  |
| ​  | `while` (queue.read()) { |
| ​  | `const` currentVertex = queue.dequeue(); |
| ​  |  |
| ​  | `for` (`const` adjacentVertex `of` `currentVertex.adjacentVertices`) { |
| ​  | `if` (!visitedVertices[`adjacentVertex.value`]) { |
| ​  | visitedVertices[`adjacentVertex.value`] = `true`; |
| ​  | queue.enqueue(`adjacentVertex`); |
| ​  | previousVertexTable[`adjacentVertex.value`] = `currentVertex.value`; |
| ​  | } |
| ​  | } |
| ​  | } |
| ​  |  |
| ​  | `const` shortestPath = []; |
| ​  | `let` currentVertexValue = `secondVertex.value`; |
| ​  |  |
| ​  | `while` (currentVertexValue !== `firstVertex.value`) { |
| ​  | shortestPath.unshift(`currentVertexValue`); |
| ​  | `currentVertexValue` = previousVertexTable[`currentVertexValue`]; |
| ​  | } |
| ​  |  |
| ​  | shortestPath.unshift(`firstVertex.value`); |
| ​  |  |
| ​  | `return` shortestPath; |
| ​  | } |
