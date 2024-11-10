## 练习

以下练习为您提供了使用图的机会。这些练习的解决方案在章节[​`第18章`​](f_0223.xhtml#graphs.solutions)中找到。

1.  第一个[`graph`](#fig.ch18.recommendation_graph)为电子商务商店的推荐引擎提供支持。每个顶点代表商店网站上可用的产品。边连接每个产品与其他“类似”产品，网站会在用户浏览特定商品时推荐给他们。

    如果用户正在浏览`“nails”`，将向用户推荐哪些其他产品？

1.  如果我们在第二个[`graph`](#fig.ch18.exercise_2_graph)上执行深度优先搜索，从`A`顶点开始，我们将以什么顺序遍历所有顶点？假设在选择访问多个相邻顶点时，我们首先访问字母表中最靠前的节点。

    ![`images/graphs/recommendation_graph.png`](images/graphs/recommendation_graph.png)![`images/graphs/exercise_2_graph.png`](images/graphs/exercise_2_graph.png)

1.  如果我们从`A`顶点开始在前面的图上执行广度优先搜索，我们将以什么顺序遍历所有顶点？假设在选择访问多个相邻顶点时，我们首先访问字母表中最靠前的节点。

1.  在本章中，我仅提供了广度优先遍历的代码，如在[​`广度优先搜索`​](f_0183.xhtml#sect.breadth-first-search)中讨论的那样；也就是说，代码只是打印每个顶点的值。修改代码，使其能够对传递给函数的顶点值进行实际搜索。（我们在深度优先搜索中做过这件事。）换句话说，如果函数找到它正在搜索的顶点，它应该返回该顶点的值。否则，它应该返回`null`。

1.  在[​`Dijkstra算法`​](f_0186.xhtml#sect.dijkstras-algorithm)中，我们看到了Dijkstra算法如何帮助我们找到加权图中的最短路径。然而，最短路径的概念在无权图中也存在。如何存在呢？

    在经典的（无权）图中，最短路径是从一个顶点到另一个顶点所需经过的最少顶点数量的路径。

    这在社交网络应用中尤其有用。以下是一个示例网络：

    ![`images/graphs/exercise_5_graph.png`](images/graphs/exercise_5_graph.png)

    如果我们想知道`Idris`与`Lina`的连接方式，我们会发现她从两个不同的方向与她相连；也就是说，`Idris`通过`Kamil`与`Lina`是二度连接，但她通过`Talia`又是五度连接。现在，我们可能对`Idris`与`Lina`的紧密连接程度感兴趣，因此考虑到他们也是二度连接，五度连接的事实就不那么重要了。

    编写一个函数，该函数接受图中的两个顶点，并返回它们之间的最短路径。该函数应返回一个包含精确路径的数组，例如`["Idris", "Kamil", "Lina"]`。

    提示：该算法可能包含广度优先搜索和Dijkstra算法的元素。

#### 注释

`[[7]](f_0184.xhtml#FNPTR-7)`

`http://neo4j.com`

`[[8]](f_0184.xhtml#FNPTR-8)`

`https://www.arangodb.com`

版权所有 © 2024, The Pragmatic Bookshelf.
