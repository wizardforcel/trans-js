## 面向对象的图实现

我展示了如何使用哈希表来实现一个图，但在接下来的工作中，我们将采用面向对象的方法。

这是使用 JavaScript 开始的一个面向对象的图实现：

| ​  | `class` Vertex { |
| --- | --- |
| ​  | `constructor`(value) { |
| ​  | `this.value = value;` |
| ​  | `this.adjacentVertices = [];` |
| ​  | `}` |
| ​  |  |
| ​  | `addAdjacentVertex(vertex) {` |
| ​  | `this.adjacentVertices.push(vertex);` |
| ​  | `}` |
| ​  | `}` |
| ​  |  |
| ​  | `export` `default` Vertex; |

`Vertex`类有两个主要属性，`value`和一个`adjacentVertices`数组。在我们的社交网络示例中，每个顶点代表一个人，而`value`可能是一个包含该人姓名的字符串。在更复杂的应用中，我们可能希望在顶点内部存储多个数据片段，例如该人的附加个人信息。

`adjacentVertices`数组包含了此顶点连接的所有顶点。我们可以使用`addAdjacentVertex`方法向给定顶点添加一个新的相邻顶点。

这是我们如何使用这个类来构建一个有向图，表示这个图中谁跟随谁：

![images/graphs/graph_2.png](images/graphs/graph_2.png)

| ​  | `let` alice = `new` Vertex(`'alice'`); |
| --- | --- |
| ​  | `let` bob = `new` Vertex(`'bob'`); |
| ​  | `let` cynthia = `new` Vertex(`'cynthia'`); |
| ​  |  |
| ​  | `alice.addAdjacentVertex(bob);` |
| ​  | `alice.addAdjacentVertex(cynthia);` |
| ​  | `bob.addAdjacentVertex(cynthia);` |
| ​  | `cynthia.addAdjacentVertex(bob);` |

现在，如果我们为社交网络构建一个无向图（所有友谊都是相互的），那么如果我们将 Bob 添加到 Alice 的朋友列表中，理应自动将 Alice 添加到 Bob 的朋友列表中。

为此，我们可以按如下方式修改我们的`addAdjacentVertex`方法：

| ​  | `addAdjacentVertex(vertex) {` |
| --- | --- |
| ​  | `this.adjacentVertices.push(vertex);` |
| ​  | `vertex.adjacentVertices.push(this);` |
| ​  | `}` |

假设我们正在对 Alice 调用此方法并将 Bob 添加到她的朋友列表中。与之前的版本一样，我们使用`this.adjacentVertices.push(vertex)`将 Bob 添加到 Alice 的相邻顶点列表中。然而，我们还在 Bob 的顶点上调用此方法，使用`vertex.adjacentVertices.push(this)`。这将 Alice 也添加到 Bob 的朋友列表中。

为了简化后续操作，我们将处理连接的图（再次强调，意味着所有顶点以某种方式互相连接）。对于这样的图，我们可以使用一个`Vertex`类来实现后续所有的算法。一般来说，如果我们仅访问一个顶点，我们可以从那里找到所有其他顶点，因为所有顶点都是连接的。

然而，需要指出的是，如果我们处理的是一个不连通的图，从一个顶点可能无法发现所有顶点。在这种情况下，我们可能需要将所有图的顶点存储在一些额外的数据结构中，例如一个数组，以便我们可以访问它们。（常见的做法是看到图的实现使用一个单独的`Graph`类来包含这个数组。）

`邻接表` vs. `邻接矩阵`

我们的图的实现使用一个简单的列表（以数组的形式）来存储一个顶点的相邻顶点。这种方法被称为`邻接表实现`。

然而，值得知道的是，还有另一种实现，它使用二维数组而不是列表。这种替代方法被称为`邻接矩阵`，在特定情况下可以提供优势。

两种方法都很流行，我决定坚持使用`adjacency list`，因为我觉得它更直观。但是我建议你也研究一下`adjacency matrix`，因为它可以很有用且特别有趣。
