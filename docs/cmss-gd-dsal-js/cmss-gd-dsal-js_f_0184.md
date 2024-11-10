## 图搜索的效率

让我们使用`Big O`符号分析图搜索的时间复杂度。

在`深度优先搜索`和`广度优先搜索`中，我们在最坏情况下遍历所有顶点。最坏情况下，可能是我们打算进行全图遍历，或者我们可能正在搜索一个不存在于图中的顶点。或者，我们要搜索的顶点可能正好是我们检查的最后一个顶点。

无论如何，我们会接触到图中的所有顶点。乍一看，这似乎是`O(N)`，其中`N`是顶点的数量。

然而，在两种搜索算法中，对于每个我们遍历的顶点，我们还会遍历所有相邻的顶点。如果一个相邻顶点已经被访问过，我们可以忽略它，但我们仍然需要花一步去检查该顶点是否已被访问。

所以，对于每个我们访问的顶点，我们还花步骤检查每个顶点的相邻邻居。这似乎很难用`Big O`符号来确定，因为每个顶点可能有不同数量的相邻顶点。

让我们分析一个简单的图以便明确：

`![images/graphs/abcde_graph.png](images/graphs/abcde_graph.png)`

在这里，`Vertex A`有四个邻居。相反，`B`、`C`、`D`和`E`各有三个邻居。让我们计算搜索该图所需的步骤数。

至少，我们必须访问每个五个顶点。这本身就需要五步。

然后，对于每个顶点，我们遍历它的每个邻居。

这将增加以下步骤：

`A`：4步遍历4个邻居

`B`：3步遍历3个邻居

`C`：3步遍历3个邻居

`D`：3步遍历3个邻居

`E`：3步遍历3个邻居

这产生了十六次迭代。

我们访问了五个顶点，加上对相邻邻居的十六次迭代。这总共是二十一步。

但这是另一个有五个顶点的图：

`![images/graphs/vwxyz_graph.png](images/graphs/vwxyz_graph.png)`

这个图有五个顶点，但对相邻邻居的迭代次数如下：

`V`：4步遍历4个邻居

`W`：1步遍历1个邻居

`X`：1步遍历1个邻居

`Y`：1步遍历1个邻居

`Z`：1步遍历1个邻居

总共进行八次迭代。

我们访问了五个顶点，加上对相邻邻居的八次迭代。这总共是十三步。

因此，我们有两个图，每个图包含五个顶点。然而，搜索一个需要二十一步，而搜索另一个只需十三步。

结果表明，我们不能仅仅计算图中有多少个顶点。相反，我们还需要考虑每个顶点有多少个相邻的邻居。

因此，为了有效地描述图搜索的效率，我们需要使用两个变量。我们需要一个来表示图中顶点的数量，另一个来表示每个顶点的总相邻邻居数量。

### `O(V + E)`

有趣的是，大O符号并不使用变量`N`来描述这两者。相反，它使用变量`V`和`E`。

`V`是比较简单的。`V`代表顶点，表示图中顶点的数量。

`E`，有趣的是，代表边，意味着图中边的数量。

现在，计算机科学家将图搜索的效率描述为`O(V + E)`。这意味着步骤的数量是图中顶点的数量加上图中边的数量。让我们看看为什么这是图搜索的效率，因为这并不是立刻直观的。

特别是，如果你看看我们之前的两个例子，你会注意到`V + E`似乎并不准确。

在`A-B-C-D-E`图中，有五个顶点和八条边。这将总共是十三个步骤。然而，我们注意到实际上总共有二十一条步骤。

在`V-W-X-Y-Z`图中，有五个顶点和四条边。`O(V + E)`表示图搜索将有九个步骤。但我们看到实际上有十三个步骤。

造成这种差异的原因是，虽然`O(V + E)`只计算边的数量一次，但实际上图搜索多次接触每一条边。

在`V-W-X-Y-Z`图中，例如，只有四条边。然而，`V`和`W`之间的边被使用了两次；也就是说，当`V`是当前顶点时，我们通过那条边找到它的相邻邻居`W`。但当`W`是当前顶点时，我们又通过那条边找到它的相邻顶点`V`。

考虑到这一点，描述`V-W-X-Y-Z`图中图搜索效率的最准确方式是计算五个顶点，加上以下内容：

`2 * edge`在`V`和`W`之间

`2 * edge`在`V`和`X`之间

`2 * edge`在`V`和`Y`之间

`2 * edge`在`V`和`Z`之间

所以这得出结果为`V + 2E`，因为我们访问所有顶点一次（那就是`V`），并且每条边使用两次（那就是`2E`）。

在这个例子中，`V`是5，因为我们访问了5个顶点。由于我们每条边都使用了两次，`2E`结果是8。这是`V + 2E`给我们一个总共的十三个步骤。

不过，为什么我们称之为`O(V + E)`，是因为大O忽略了常数。虽然实际上步骤的数量是`V + 2E`，我们将其简化为`O(V + E)`。

因此，尽管`O(V + E)`最终只是一种近似，但它足够好，所有的大O表达式也是如此。

然而，明确的一点是，增加边的数量将增加步骤的数量。毕竟，`A-B-C-D-E`和`V-W-X-Y-Z`图都有五个顶点，但由于`A-B-C-D-E`图有更多的边，因此需要的步骤明显更多。

最终，图搜索在最坏情况下是`O(V + E)`，即我们搜索的顶点是最后一个找到的（或根本不存在于图中）。这对广度优先搜索和深度优先搜索都是正确的。

然而，我们之前看到，根据图的形状和我们要搜索的数据，选择`广度优先`还是`深度优先`可以优化我们的搜索，期望在不必遍历整个图之前找到我们的顶点。正确的搜索方法可以提高我们不陷入最坏情况的几率，并且能够早期找到顶点。

在接下来的部分中，你将学习一种特定类型的`图`，它具有自己的一套搜索方法，可以用来解决一些复杂但有用的问题。

`图数据库`

由于图在处理涉及关系的数据（例如社交网络中的朋友）时非常高效，因此在实际软件应用中，通常使用特殊的`图`数据库来存储这类数据。这些数据库运用了你在本章中学习的概念，以及其他`图论`的元素，以优化此类数据操作的效率。实际上，许多社交网络应用的后台都是由`图`数据库提供支持的。

一些`图`数据库的例子包括`Neo4j`^([[7]](f_0188.xhtml#FOOTNOTE-7))和`ArangoDB`^([[8]](f_0188.xhtml#FOOTNOTE-8))。如果你有兴趣了解`图`数据库的工作原理，这些网站是一个不错的起点。