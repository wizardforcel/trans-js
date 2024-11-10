## `Dijkstra`算法

有许多算法可以解决最短路径问题，其中最著名的是`Edsger Dijkstra`于1959年发现的算法。毫不奇怪，这个算法被称为`Dijkstra`算法。

在本节中，我们将使用`Dijkstra`算法来寻找在我们的城市航班示例中的最低路径。

### `Dijkstra`算法设置

首先要注意的是，`Dijkstra`算法带来了一个免费的附加功能。当我们完成时，我们不仅会找到从`亚特兰大`到`埃尔帕索`的最低价格，还会找到从`亚特兰大`到所有已知城市的最低价格。正如你所看到的，算法就是这样工作的；我们最终收集到所有这些数据。因此，我们将知道从`亚特兰大`到`芝加哥`的最低价格，从`亚特兰大`到`丹佛`的最低价格，等等。

为了进行设置，我们将创建一种存储从起始城市到所有其他已知目的地的最低已知价格的方法。在接下来的代码中，我们将为此使用哈希表。然而，在我们的示例演示中，我们将使用如下的可视化表格：

| 从`亚特兰大`到： | `城市 #1` | `城市 #2` | `城市 #3` | 其他 |
| --- | --- | --- | --- | --- |
|  | ? | ? | ? | ? |

算法将从`亚特兰大`顶点开始，因为这是我们目前唯一知道的城市。随着我们发现新城市，我们将把它们添加到我们的表格中，并记录从`亚特兰大`到这些城市的最低价格。

当算法完成时，表格将如下所示：

| 从`亚特兰大`到： | `波士顿` | `芝加哥` | `丹佛` | `埃尔帕索` |
| --- | --- | --- | --- | --- |
|  | `$100` | `$200` | `$160` | `$280` |

在代码中，这将用一个哈希表表示，结构如下：

| ​  | `{"亚特兰大": 0, "波士顿": 100, "芝加哥": 200,` |
| --- | --- |
| ​  | `"丹佛": 160, "埃尔帕索": 280}` |

（注意，`亚特兰大`在哈希表中也有一个值为`0`。我们需要这个值使算法正常工作，但这也合理，因为从`亚特兰大`到`亚特兰大`不需要花费任何费用，因为你已经在那里！）

在我们的代码中，以及后续内容中，我们将称这个表为`cheapestPricesTable`，因为它存储从起始城市到所有其他目的地的最低价格。

现在，如果我们只想弄清楚到达特定目的地的最低价格，`cheapestPricesTable`将包含我们所需的所有数据。但我们可能还想知道实际的路径，以便获得最低价格。例如，如果我们想从`亚特兰大`到`埃尔帕索`，我们不仅想知道最低价格是`$280`；我们还想知道，为了获得这个价格，我们需要飞行`亚特兰大--丹佛--芝加哥--埃尔帕索`这条特定路径。

为了实现这一点，我们还需要另一个表格，我们称之为`cheapestPreviousStopoverCityTable`。该表的目的将在我们深入算法时变得清晰，因此我会暂时不解释。现在，展示它在算法结束时的样子就足够了。

| 从亚特兰大出发的最便宜的前停留城市： | 波士顿 | 芝加哥 | 丹佛 | 埃尔帕索 |
| --- | --- | --- | --- | --- |
|  | 亚特兰大 | 丹佛 | 亚特兰大 | 芝加哥 |

（注意，这个表格也将使用哈希表实现。）

### `Dijkstra’s Algorithm Steps`

现在一切都已设置好，以下是 Dijkstra 算法的步骤。为了清晰起见，我将以城市为例描述该算法，但您可以将“城市”一词替换为“顶点”，以使其适用于任何加权图。还要注意，当我们通过示例逐步讲解时，这些步骤会变得更加清晰。但现在，开始吧：

1.  我们访问起始城市，使其成为我们的“当前城市”。

1.  我们检查从当前城市到每个相邻城市的价格。

1.  如果从起始城市到相邻城市的价格低于`cheapestPricesTable`中当前的价格（或者相邻城市尚未在`cheapestPricesTable`中）：

    a. 我们更新`cheapestPricesTable`以反映这一更便宜的价格。

    b. 我们更新`cheapestPreviousStopoverCityTable`，使相邻城市成为键，当前城市成为值。

1.  然后我们访问从起始城市出发的未访问城市中价格最低的城市，使其成为当前城市。

1.  我们重复步骤 2 到 4，直到访问每个已知城市。

再次强调，当我们逐步讲解示例时，这一切会更容易理解。

### `Dijkstra’s Algorithm Walk-Through`

让我们逐步讲解 Dijkstra 算法。

为了开始，我们的`cheapestPricesTable`仅包含亚特兰大：

| 从亚特兰大到： |
| --- |
| `$0` |

在算法开始时，亚特兰大是我们唯一可以访问的城市；我们尚未“发现”其他城市。

步骤 1：我们正式访问亚特兰大，并使其成为`currentCity`。

为了表明这是`currentCity`，我们会用线将其包围。并且为了记录我们已经访问过它，我们会加上一个勾号：

![images/graphs/weighted_graph_4.png](images/graphs/weighted_graph_4.png)

在接下来的步骤中，我们将检查每个`currentCity`的相邻城市。这就是我们发现新城市的方式；如果我们能够访问的城市有我们之前不知道的相邻城市，我们可以将它们添加到我们的地图中。

步骤 2：与亚特兰大相邻的一座城市是波士顿。正如我们所见，从亚特兰大到波士顿的价格是`$100`。然后我们检查`cheapestPricesTable`，看看这是否是从亚特兰大到波士顿的已知最便宜价格，但结果是我们还没有记录从亚特兰大到波士顿的任何价格。这意味着这是从亚特兰大到波士顿的已知最便宜航班（截至目前），因此我们将其添加到`cheapestPricesTable`：

| 从亚特兰大到： | 波士顿 |
| --- | --- |
| `$0` | `$100` |

由于我们对`cheapestPricesTable`进行了更改，现在也需要修改`cheapestPreviousStopoverCityTable`，将相邻城市（`波士顿`）作为键，`currentCity`作为值：

| 从亚特兰大出发的最便宜的前停留城市： | `波士顿` |
| --- | --- |
|  | `亚特兰大` |

将这些数据添加到此表中意味着为了获得从`亚特兰大`到`波士顿`的最便宜已知价格（`$100`），我们需要在访问`波士顿`之前立即访问`亚特兰大`。此时，这显而易见，因为`亚特兰大`是我们知道的到达`波士顿`的唯一途径。然而，随着我们的进行，我们会看到为什么第二个表变得有用。

第3步：我们已经查看了`Boston`，但`Atlanta`还有另一个相邻城市，`Denver`。我们检查价格（`$160`）是否是从`Atlanta`到`Denver`的最便宜已知路线，但`Denver`在`cheapestPricesTable`中根本没有，因此我们将其添加为已知最便宜航班：

| 从`Atlanta`到： | `Boston` | `Denver` |
| --- | --- | --- |
| `$0` | `$100` | `$160` |

然后，我们还将`Denver`和`Atlanta`作为键值对添加到`cheapestPreviousStopoverCityTable`中：

| 从`Atlanta`到的最便宜的前一个中转城市： | `Boston` | `Denver` |
| --- | --- | --- |
|  | `Atlanta` | `Atlanta` |

第4步：到这时，我们已经检查了`Atlanta`的所有相邻城市，所以是时候访问下一个城市了。但我们需要弄清楚下一个要访问哪个城市。

现在，正如之前算法步骤中所述，我们只会继续访问尚未访问的城市。此外，在未访问的城市中，我们总是选择首先访问从起始城市到达的最便宜已知路线的城市。我们可以从`cheapestPricesTable`中获取这些数据。

在我们的例子中，我们知道的唯一尚未访问的城市是`Boston`或`Denver`。通过查看`cheapestPricesTable`，我们可以看到，从`Atlanta`到`Boston`的价格比从`Atlanta`到`Denver`的价格更便宜，因此我们接下来要访问`Boston`。

第5步：我们访问`Boston`并将其指定为`currentCity`：

![images/graphs/weighted_graph_5.png](images/graphs/weighted_graph_5.png)

接下来，我们将检查`Boston`的相邻城市。

第6步：`Boston`有两个相邻城市，`Chicago`和`Denver`。（`Atlanta`不被视为相邻城市，因为我们不能从`Boston`飞往`Atlanta`。）

我们应该先访问哪个城市——`Chicago`还是`Denver`？同样，我们希望首先访问从`Atlanta`飞往该城市的价格最低的城市。那么我们来算一下。

从`Boston`到`Chicago`的价格是`$120`。查看`cheapestPricesTable`，我们可以看到从`Atlanta`到`Boston`的最便宜路线是`$100`。这意味着从`Atlanta`到`Chicago`的最便宜航班，以`Boston`作为之前的中转城市，价格为`$220`。

由于此时这是从`Atlanta`到`Chicago`的唯一已知价格，我们将其添加到`cheapestPricesTable`。我们将其插入到表的中间，以保持城市的字母顺序：

| 从`Atlanta`到： | `Boston` | `Chicago` | `Denver` |
| --- | --- | --- | --- |
| `$0` | `$100` | `$220` | `$160` |

再次，因为我们对该表进行了更改，所以我们也将修改`cheapestPreviousStopoverCityTable`。相邻城市始终成为键，而`currentCity`始终成为值，因此表格变为：

| 从`Atlanta`到的最便宜的前一个中转城市： | `Boston` | `Chicago` | `Denver` |
| --- | --- | --- | --- |
|  | `Atlanta` | `Boston` | `Atlanta` |

在寻找下一个要访问的城市的过程中，我们分析了`Chicago`。接下来我们将检查`Denver`。

第7步：现在让我们看一下`Boston`和`Denver`之间的边缘。我们可以看到价格是`$180`。由于从`Atlanta`到`Boston`的最便宜航班再次是`$100`，这意味着从`Atlanta`到`Denver`的最便宜航班通过`Boston`作为前一个中转城市的价格为`$280`。

这变得有些有趣，因为当我们检查我们的`cheapestPricesTable`时，可以看到从`Atlanta`到`Denver`的最便宜路线是`$160`，这比`Atlanta–Boston–Denver`的路线便宜。因此，我们不会修改我们的表格；我们希望将`$160`保留为从`Atlanta`到`Denver`的已知最便宜路线。

我们完成了这一步，既然我们已经查看了`Boston`的所有相邻城市，现在可以访问下一个城市。

第8步：当前已知的未访问城市是`Chicago`和`Denver`。我们下一步访问的城市——请特别注意——是从我们的起始城市（`Atlanta`）到达的最便宜已知路径的城市。

从我们的`cheapestPricesTable`来看，从`亚特兰大`到`丹佛`的费用（`$160`）比从`亚特兰大`到`芝加哥`（`$220`）便宜，因此我们接下来访问`丹佛`：

![`images/graphs/weighted_graph_6.png`](images/graphs/weighted_graph_6.png)

接下来，我们将查看`丹佛`的邻近城市。

步骤9：`丹佛`有两个邻近城市，`芝加哥`和`埃尔帕索`。我们接下来要访问哪个城市？要找出答案，我们需要分析到每个城市的价格。让我们从`芝加哥`开始。

从`丹佛`到`芝加哥`只需`$40`（非常划算！），这意味着通过`丹佛`作为前一个中转城市，从`亚特兰大`到`芝加哥`的最便宜航班费用将为`$200`，因为从`亚特兰大`到`丹佛`的最便宜路线是`$160`。

查看`cheapestPricesTable`时，我们可以看到从`亚特兰大`到`芝加哥`的当前最低价格是`$220`。这意味着我们刚刚找到的通过`丹佛`到`芝加哥`的新路线甚至更便宜，因此我们可以相应地更新`cheapestPricesTable`：

| 从`亚特兰大`到： | `波士顿` | `芝加哥` | `丹佛` |
| --- | --- | --- | --- |
| `$0` | `$100` | `$200` | `$160` |

每当我们更新`cheapestPricesTable`时，也必须更新`cheapestPreviousStopoverCityTable`。我们将邻近城市（`芝加哥`）设为键，将`当前城市`（`丹佛`）设为值。现在，在这种情况下，`芝加哥`已经存在为一个键。这意味着我们将把它的值从`波士顿`覆盖为`丹佛`：

| 从`亚特兰大`出发的最便宜的中转城市： | `波士顿` | `芝加哥` | `丹佛` |
| --- | --- | --- | --- |
|  | `亚特兰大` | `丹佛` | `亚特兰大` |

`这意味着要获得从亚特兰大到芝加哥的最便宜航班，我们需要在前往芝加哥之前，先在丹佛停留；也就是说，丹佛应该是我们到芝加哥之前的倒数第二个停留点。只有这样我们才能省下最多的钱。`

`这些信息将有助于确定从亚特兰大到我们的目的地城市的最便宜路径，稍后你会看到。等等，我们快到了！`

`步骤10：丹佛有另一个邻近城市，埃尔帕索。从丹佛到埃尔帕索的价格是$140。我们现在可以构建从亚特兰大到埃尔帕索的第一个已知价格。cheapestPricesTable告诉我们从亚特兰大到丹佛的最低价格是$160。这意味着如果我们再从丹佛到埃尔帕索，将增加$140，使从亚特兰大到埃尔帕索的总价格为$300。我们可以将其添加到cheapestPricesTable中：`

| 从亚特兰大到： | 波士顿 | 芝加哥 | 丹佛 | 埃尔帕索 |
| --- | --- | --- | --- | --- |
| $0 | $100 | $200 | $160 | $300 |

`我们还必须将埃尔帕索-丹佛的键值对添加到我们的cheapestPreviousStopoverCityTable中：`

| 从亚特兰大出发的最便宜的中转城市： | 波士顿 | 芝加哥 | 丹佛 | 埃尔帕索 |
| --- | --- | --- | --- | --- |
|  | 亚特兰大 | 丹佛 | 亚特兰大 | 丹佛 |

`这意味着为了在从Atlanta到El Paso的航班中节省最多的钱，我们的倒数第二个停留应该是Denver。`

`我们已经查看了currentCity的所有相邻城市，因此是时候访问下一个城市。`

`第11步：我们有两个已知的未访问城市，Chicago和El Paso。由于从Atlanta到Chicago的费用（$200）比从Atlanta到El Paso的费用（$300）更便宜，因此我们接下来访问Chicago，如下图所示：`

![images/graphs/weighted_graph_7.png](images/graphs/weighted_graph_7.png)

`第12步：Chicago只有一个相邻城市，El Paso。从Chicago到El Paso的价格是$80（不错）。有了这个信息，我们现在可以计算从Atlanta到El Paso的最便宜价格，假设Chicago是我们的倒数第二个停留城市。`

`cheapestPricesTable告诉我们，从Atlanta到Chicago的最便宜路径是$200。再加上$80，意味着从Atlanta到El Paso的最便宜价格，假设Chicago是倒数第二个停留，将花费$280。`

`等等！这比目前已知的从Atlanta到El Paso的最便宜路径更便宜。在我们的cheapestPricesTable中，我们看到已知的最便宜价格是$300。然而，当我们经由Chicago时，价格是$280，更便宜。`

`因此，我们需要更新cheapestPricesTable，以指示我们新找到的到El Paso的最便宜路径：`

| 从Atlanta到： | Boston | Chicago | Denver | El Paso |
| --- | --- | --- | --- | --- |
| $0 | $100 | $200 | $160 | $280 |

`我们还需要更新cheapestPreviousStopoverCityTable，以`El Paso`为键，`Chicago`为值：`

| 从Atlanta出发的最便宜前一个停留城市： | Boston | Chicago | Denver | El Paso |
| --- | --- | --- | --- | --- |
|  | Atlanta | Denver | Atlanta | Chicago |

`Chicago`没有更多相邻城市，所以我们现在可以访问下一个城市。

第13步：`El Paso`是唯一已知的未访问城市，因此让我们将其设为`currentCity`，如图所示：

![images/graphs/weighted_graph_8.png](images/graphs/weighted_graph_8.png)

第14步：`El Paso`只有一个出境航班，即飞往`Boston`。该航班费用为`$100`。现在，`cheapestPricesTable`揭示从`Atlanta`到`El Paso`的最便宜价格为`$280`。因此，如果我们从`Atlanta`飞往`Boston`，而`El Paso`是倒数第二个停留城市，我们的总费用将为`$380`。这比从`Atlanta`到`Boston`的最便宜已知价格（`$100`）更贵，因此我们不会更新任何表格。

由于我们已访问每个已知城市，现在我们拥有找到从`Atlanta`到`El Paso`最便宜路径所需的所有信息。

### 寻找最短路径

如果我们只想知道从`Atlanta`到`El Paso`的最便宜价格，我们可以在`cheapestPricesTable`中查看，发现是`$280`。但如果我们想找出飞往获得该低价的确切路径，我们还有最后一件事要做。

还记得`cheapestPreviousStopoverCityTable`吗？现在是使用这些数据的时候了。

目前，`cheapestPreviousStopoverCityTable`看起来是这样的：

| 从`Atlanta`出发的最便宜的前一个停留城市： | `Boston` | `Chicago` | `Denver` | `El Paso` |
| --- | --- | --- | --- | --- |
|  | `Atlanta` | `Denver` | `Atlanta` | `Chicago` |

我们可以利用这个表来绘制从`Atlanta`到`El Paso`的最短路径——如果我们向后走的话。

让我们查看`El Paso`。它对应的城市是`Chicago`。这意味着从`Atlanta`到`El Paso`的最便宜路线涉及在飞往`El Paso`之前停留在`Chicago`。让我们将其写下来：

| ​  | `Chicago -> El Paso` |
| --- | --- |

现在，如果我们在`cheapestPreviousStopoverCityTable`中查找`Chicago`，可以看到它对应的值是`Denver`。这意味着从`Atlanta`到`Chicago`的最便宜路线涉及在`Chicago`之前停留在`Denver`。让我们将其添加到我们的图示中：

| ​  | `Denver -> Chicago -> El Paso` |
| --- | --- |

如果我们然后在`cheapestPreviousStopoverCityTable`中查找`Denver`，可以看到从`Atlanta`到`Denver`的最便宜航班是直接从`Atlanta`飞往`Denver`：

| ​  | `Atlanta -> Denver -> Chicago -> El Paso` |
| --- | --- |

现在，`Atlanta`恰好是我们的起始城市，因此这条路线正是我们从`Atlanta`到`El Paso`获取最便宜价格的确切路径。

让我们回顾一下我们用来连接最便宜路径的逻辑。

请记住，`cheapestPreviousStopoverCityTable`包含每个目的地在到达该目的地之前的倒数第二个停留城市，以便在从`Atlanta`飞往时获得最便宜的价格。

因此，从`cheapestPreviousStopoverCityTable`中，我们可以看到从`Atlanta`到`El Paso`的最便宜价格意味着：

+   我们需要直接从`Chicago`飞往`El Paso`，并且

+   我们需要直接从`Denver`飞往`Chicago`，并且

+   我们需要直接从`Atlanta`飞往`Denver`。

这意味着以下内容是我们最便宜的路径：

| ​  | `Atlanta -> Denver -> Chicago -> El Paso` |
| --- | --- |

而且…就是这样。哇！

### 代码实现：Dijkstra算法

在我们进入实际算法之前，我们可以使用以下代码设置我们之前的示例：

| ​  | `const`​ `atlanta` = `new`​ `City`(`'Atlanta'`); |
| --- | --- |
| ​  | `const`​ `boston` = `new`​ `City`(`'Boston'`); |
| ​  | `const`​ `chicago` = `new`​ `City`(`'Chicago'`); |
| ​  | `const`​ `denver` = `new`​ `City`(`'Denver'`); |
| ​  | `const`​ `elPaso` = `new`​ `City`(`'El Paso'`); |
| ​  |  |
| ​  | `atlanta.addRoute`(`boston`, 100); |
| ​  | `atlanta.addRoute`(`denver`, 160); |
| ​  | `boston.addRoute`(`chicago`, 120); |
| ​  | `boston.addRoute`(`denver`, 180); |
| ​  | `chicago.addRoute`(`elPaso`, 80); |
| ​  | `denver.addRoute`(`chicago`, 40); |
| ​  | `denver.addRoute`(`elPaso`, 140); |
| ​  | `elPaso.addRoute`(`boston`, 100); |

最后，这是Dijkstra算法的代码。它并不轻松阅读，而且可能是本书中最复杂的代码。不过，如果你准备好仔细研究它，继续阅读吧。

在我们的实现中，这个方法并不在`City`类内部，而是在外部。该方法接受两个`City`实例并返回它们之间的最短路径：

| ​  | `function`​ `dijkstraShortestPath`(`startingCity`, `finalDestination`) { |
| --- | --- |
| ​  | `const`​ `cheapestPricesTable` = {}; |
| ​  | `const`​ `cheapestPreviousStopoverCityTable` = {}; |
| ​  | `let`​ `unvisitedCities` = [`startingCity`]; |
| ​  | `const`​ `visitedCities` = {}; |
| ​  |  |
| ​  | `cheapestPricesTable`[`startingCity.name`] = 0; |
| ​  | `let`​ `currentCity` = `startingCity`; |
| ​  |  |
| ​  | `while`​ (`unvisitedCities.length` > 0) { |
| ​  | `visitedCities`[`currentCity.name`] = `true`; |
| ​  | `unvisitedCities` = `unvisitedCities.filter`((`city`) => `city` !== `currentCity`); |
| ​  |  |
| ​  | `for`​ (`const`​ `adjacentCity` ​`of`​ `currentCity.routes.keys()`) { |
| ​  | `const`​ `price` = `currentCity.routes.get`(`adjacentCity`); |
| ​  |  |
| ​  | `if`​ (!`visitedCities`[`adjacentCity.name`] && |
| ​  | `!unvisitedCities`[`adjacentCity`] { |
| ​  | `unvisitedCities.push`(`adjacentCity`); |
| ​  | } |
| ​  |  |
| ​  | `const`​ `priceThroughCurrentCity` = |
| ​  | (`cheapestPricesTable`[`currentCity.name`] + `price`); |
| ​  |  |
| ​  | `if`​ (!`cheapestPricesTable`[`adjacentCity.name`] &#124;&#124; `priceThroughCurrentCity` |
| ​  | < `cheapestPricesTable`[`adjacentCity.name`] < `cheapestPrice`) { |
| ​  | `cheapestPricesTable`[`adjacentCity.name`] = `priceThroughCurrentCity`; |
| ​  | `cheapestPreviousStopoverCityTable`[`adjacentCity.name`] = |
| ​  | `currentCity.name`; |
| ​  | } |
| ​  | } |
| ​  |  |
| ​  | `let`​ `cheapestPrice` = `Infinity`; |
| ​  |  |
| ​  | `for`​ (`const`​ `city` ​`of`​ `unvisitedCities`) { |
|  | `if`​ (`cheapestPricesTable`[`city.name`] < `cheapestPrice`) { |
| ​  | `cheapestPrice` = `cheapestPricesTable`[`city.name`]; |
| ​  | `currentCity` = `city`; |
| ​  | } |
| ​  | } |
| ​  | } |
| ​  |  |
| ​  | `const`​ `shortestPath` = []; |
| ​  | `let`​ `currentCityName` = `finalDestination.name`; |
| ​  |  |
| ​  | `while` (currentCityName) { |
| ​  | `shortestPath.unshift(currentCityName);` |
| ​  | `currentCityName = cheapestPreviousStopoverCityTable[currentCityName];` |
| ​  | } |
| ​  |  |
| ​  | `return` shortestPath; |
| ​  | } |

我们有相当多的代码在这里，所以让我们分解一下。

`The dijkstraShortestPath`函数接受两个顶点，代表`startingCity`和`finalDestination`。

最终，我们的函数将返回一个表示最便宜路径的字符串数组。对于我们的例子，这个函数会返回：

| ​  | ["亚特兰大", "丹佛", "芝加哥", "埃尔帕索"] |
| --- | --- |

我们的函数首先做的是设置驱动整个算法的两个主要表：

| ​  | `const` cheapestPricesTable = {}; |
| --- | --- |
| ​  | `const` cheapestPreviousStopoverCityTable = {}; |

然后我们设置方式来跟踪我们已访问的城市和尚未访问的城市：

| ​  | `let` unvisitedCities = [startingCity]; |
| --- | --- |
| ​  | `const` visitedCities = {}; |

请注意，我们预填充`unvisitedCities`，使`startingCity`成为数组中的唯一项。

似乎很奇怪的是，`unvisitedCities`是一个数组，而`visitedCities`是一个哈希表。我们将`visitedCities`设为哈希表的原因是，在接下来的代码中我们仅将其用于查找，而哈希表在时间复杂度方面是理想选择。

对于`unvisitedCities`最佳数据结构的选择则没有那么简单。在我们接下来的代码中，我们访问的下一个城市总是从起始城市到达的最便宜的未访问城市。理想情况下，我们总是希望立即获取未访问城市中最便宜的选项。如果数据结构是数组的话，我们访问这些数据的代码会更简单。

事实上，优先队列非常适合这个，因为它的整个功能是提供对一组项目中最小（或最大）值的便捷访问。正如你在第16章中看到的， [​*保持你的优先级清晰，通过堆*​](f_0153.xhtml#chp.heaps)，堆通常是实现优先队列的最佳数据结构。然而，我选择使用一个简单的数组来实现，仅仅是为了保持代码尽可能简单和小，因为 Dijkstra 的算法本身已经相当复杂。但我鼓励你尝试用优先队列替换这个数组。

接下来，我们向`cheapestPricesTable`添加第一个键值对，`startingCity`作为键，0作为值。这是合理的，因为到达`startingCity`的费用是零，因为我们已经在那儿了：

| ​  | `cheapestPricesTable[startingCity.name] = 0;` |
| --- | --- |

作为最后的设置，我们指定`startingCity`为我们的`currentCity`：

| ​  | `let` currentCity = startingCity; |
| --- | --- |

我们现在开始算法的核心，它以一个循环的形式运行，只要`unvisitedCities`包含任何城市。在这个循环中，我们通过将当前城市的名称添加到`visitedCities`哈希表中来标记`currentCity`为已访问。

|  | `while (unvisitedCities.length > 0) {` |
| --- | --- |
|  | `visitedCities[currentCity.name] = true;` |

根据定义，由于我们已经访问了`currentCity`，我们需要将其从未访问城市列表中移除：

|  | `unvisitedCities = unvisitedCities.filter((city) => city !== currentCity);` |
| --- | --- |

这个JavaScript过滤器语法创建了一个未访问城市数组的副本，除了移除了`currentCity`。

接下来，在`while`循环中，我们开始另一个循环，迭代`currentCity`的所有相邻城市：

|  | `for (const adjacentCity of currentCity.routes.keys()) {` |
| --- | --- |

在这个内部循环中，我们首先获取从`currentCity`到当前迭代的相邻城市的路线价格：

|  | `const price = currentCity.routes.get(adjacentCity);` |
| --- | --- |

然后，如果相邻城市是我们从未访问过的城市，我们将每个相邻城市添加到未访问城市的数组中。此外，只有当相邻城市不在未访问城市中时，我们才添加它：

|  | `if (!visitedCities[adjacentCity.name] && !unvisitedCities[adjacentCity]) {` |
| --- | --- |
|  | `unvisitedCities.push(adjacentCity);` |
|  | } |

接下来，我们计算从起始城市到相邻城市的最便宜的价格，假设`currentCity`是倒数第二个停靠站。我们通过使用`cheapestPricesTable`查找到`currentCity`的已知最便宜路线，然后将其与从`currentCity`到相邻城市的路线价格相加。这一计算结果存储在一个名为`priceThroughCurrentCity`的变量中：

|  | `const priceThroughCurrentCity =` |
| --- | --- |
|  | `(cheapestPricesTable[currentCity.name] + price);` |

然后我们在`cheapestPricesTable`中查看这个`price_through_currentCity`是否现在是从起始城市到相邻城市的最便宜已知航班。如果相邻城市尚未在`cheapestPricesTable`中，这个价格在定义上就是已知的最便宜价格：

|  | `if (!cheapestPricesTable[adjacentCity.name] | | priceThroughCurrentCity` |
| --- | --- | --- | --- |
|  | `< cheapestPricesTable[adjacentCity.name]) {` |

如果`priceThroughCurrentCity`现在是从起始城市到相邻城市的最便宜路线，我们更新两个主要表；即，我们在`cheapestPricesTable`中存储相邻城市的新价格，并在`cheapestPreviousStopoverCityTable`中使用相邻城市的名称作为键，`currentCity`的名称作为值：

|  | `cheapestPricesTable[adjacentCity.name] = priceThroughCurrentCity;` |
| --- | --- |
|  | `cheapestPreviousStopoverCityTable[adjacentCity.name] = currentCity.name;` |

在迭代完`currentCity`的所有相邻城市后，是时候访问下一个城市了。我们使用以下代码片段找到从起始城市可以到达的最便宜的未访问城市，并将其声明为我们的新`currentCity`：

|  | `let cheapestPrice = Infinity;` |
| --- | --- |
|  |  |
| ​  | `for` ( `const` city `of` unvisitedCities) { |
| ​  | `if` (cheapestPricesTable[city.name] < cheapestPrice) { |
| ​  | cheapestPrice = cheapestPricesTable[city.name]; |
| ​  | currentCity = city; |
| ​  | } |
| ​  | } |

上述代码创建了一个`cheapestPrice`变量并将其设置为无穷大。这是一个小技巧，以确保我们遇到的每个价格都低于`cheapestPrice`的初始值。然后，循环遍历每个`unvisitedCities`，检查每个城市与`cheapestPricesTable`。每次找到更便宜的城市时，它会将`currentCity`设置为该城市。到循环结束时，`currentCity`将确实指向最便宜的未访问城市。

主`while`循环在`unvisitedCities`数组为空时结束。这意味着我们访问了图中的所有城市！

此时，两个表已完全填充了我们需要的所有数据。如果我们愿意，我们此时可以简单地返回`cheapestPricesTable`，并查看从`startingCity`到所有已知城市的最低价格。

不过，我们继续寻找到达`finalDestination`的精确最便宜路径。

为了设置这些，我们创建一个名为`shortestPath`的数组，这是我们在函数末尾返回的内容：

| ​  | `const` shortestPath = []; |
| --- | --- |

我们还创建了一个名为`currentCityName`的变量，最初以`finalDestination`的名称开始：

| ​  | `let` currentCityName = finalDestination.name; |
| --- | --- |

我们接着开始一个`while`循环，以填充`shortestPath`。这个循环将以反向顺序插入所有城市，从`finalDestination`开始，逐步回到`startingCity`：

| ​  | `while` (currentCityName) { |
| --- | --- |
| ​  | shortestPath.unshift(currentCityName); |

然后我们使用`cheapestPreviousStopoverCityTable`来找到应该是当前`currentCityName`之前的停留城市。这个前一个城市现在变成新的`currentCityName`：

| ​  | currentCityName = cheapestPreviousStopoverCityTable[currentCityName]; |
| --- | --- |

`shortestPath`现在包含了从`finalDestination`到`startingCity`的反向路径，因此这就是我们最终返回的内容：

| ​  | `return` shortestPath; |
| --- | --- |

尽管我们的实现涉及城市和价格，但所有变量名都可以更改为处理任何加权图的最短路径。

### Dijkstra算法的效率

Dijkstra算法是找到加权图中最短路径的一般描述，但并未指定精确的代码实现。实际上，存在多种变体可供编写该算法。

在我们的代码演示中，例如，我们为`unvisitedCities`数据结构使用了简单数组，但我提到可以改用优先队列。

事实证明，精确的实现对算法的时间复杂度有相当大的影响。但至少让我们分析一下我们的实现。

当我们使用一个简单的数组来跟踪尚未访问的城市（`unvisitedCities`）时，我们的算法可能需要最多`O(V²)`步。这是因为Dijkstra算法的最坏情况是每个顶点都有一条边连接到图中的每个其他顶点。在这种情况下，对于我们访问的每个顶点，我们检查从该顶点到每个其他顶点的路径权重。这是`V`个顶点乘以`V`个顶点，即`O(V²)`。

其他实现，例如使用优先队列而不是数组，会带来更快的速度。同样，Dijkstra算法有多种变体，每种变体都需要独立分析以确定其精确的时间复杂度。

无论你选择哪种算法实现，都是比另一种选择要好的选择，后者是找到图中每一条可能的路径，然后选择最快的一条。Dijkstra算法提供了一种可靠的方法，使我们能够有条理地穿过图形，并精准找到最短路径。
