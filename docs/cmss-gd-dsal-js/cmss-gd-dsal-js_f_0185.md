## 加权图

我们已经看到图可以有多种不同的形式。另一种有用的图类型，称为加权图，为图的边添加额外信息。

这是一个加权图，表示美国几个主要城市的基本地图：

![images/graphs/weighted_graph_1.png](images/graphs/weighted_graph_1.png)

在这个图中，每条边都伴随着一个数字，表示连接这些城市的边的距离（以英里为单位）——例如，芝加哥与纽约市之间714英里。

也可以有加权图是方向性的。在下面的例子中，我们可以看到，虽然从达拉斯到多伦多的航班费用是$138，但从多伦多返回达拉斯的航班费用是$216：

![images/graphs/weighted_graph_2.png](images/graphs/weighted_graph_2.png)

### 加权图在代码中

我们需要对我们的代码进行一些小修改，如果我们想要为图添加权重。实现这一点的一种方法是使用哈希表来表示相邻顶点，而不是使用数组：

| ​  | `class` `WeightedGraphVertex` { |
| --- | --- |
| ​  | `constructor`(value) { |
| ​  | `this`.value = value; |
| ​  | `this`.adjacentVertices = `new` `Map`(); |
| ​  | } |
| ​  |  |
| ​  | `addAdjacentVertex`(vertex, weight) { |
| ​  | `this`.adjacentVertices.`set`(vertex, weight); |
| ​  | } |
| ​  | } |

正如你所看到的，`this.adjacentVertices`现在是一个哈希表，而不是数组。哈希表将包含键值对，每个对中的相邻顶点是键，权重（从该顶点到相邻顶点的边的权重）是值。

当我们使用`addAdjacentVertex`方法添加相邻顶点时，我们现在同时传入相邻顶点和权重。

由于我们将继续处理一个描述各城市之间航班票价的图，我们将创建一个名为`City`的特殊类。这与前面的`WeightedGraphVertex`实现相同，但使用适合我们用例的类名和变量名：

| ​  | `class` `City` { |
| --- | --- |
| ​  | `constructor`(name) { |
| ​  | `this`.name = name; |
| ​  | `this`.routes = `new` `Map`(); |
| ​  | } |
| ​  |  |
| ​  | `addRoute`(city, price) { |
| ​  | `this`.routes.`set`(city, price); |
| ​  | } |
| ​  | } |

所以如果我们想从之前创建达拉斯–多伦多航班价格图，可以运行以下代码：

| ​  | `let` dallas = `new` `City`(`*'达拉斯'*`); |
| --- | --- |
| ​  | `let` toronto = `new` `City`(`*'多伦多'*`); |
| ​  |  |
| ​  | `dallas.addRoute(toronto, 138);` |
| ​  | `toronto.addRoute(dallas, 216);` |

### `最短路径问题`

加权图在建模各种数据集时非常有用，它们还带有一些强大的算法，帮助我们充分利用这些数据。

让我们利用这些算法为自己节省一点钱。

这是一个图，演示了五个不同城市之间可用航班的费用：

![images/graphs/weighted_graph_3.png](images/graphs/weighted_graph_3.png)

现在，假设我在亚特兰大，想要飞往埃尔帕索。不幸的是，我们可以在这个图中看到，目前从亚特兰大到埃尔帕索没有直飞的路线。然而，如果我愿意在其他城市停留，我就能到达那里。例如，我可以从亚特兰大飞往丹佛，然后再从丹佛飞往埃尔帕索。但也有其他路径，而且每条路径的价格不同。亚特兰大–丹佛–埃尔帕索的路径让我花费$300，而亚特兰大–丹佛–芝加哥–埃尔帕索的路径只需$280。

现在的问题是：我们如何创建一个算法来找到我到达目的地所需支付的最低价格？假设我们不关心需要停多少次；我们只是想找到最便宜的票价。

这种类型的难题被称为最短路径问题。这个问题也可以有其他形式。例如，如果图中显示的是城市之间的距离，我们可能想要找到距离最短的路径。但在这里，我们寻找的最短路径是价格最低的，因为权重代表的是航班价格。
