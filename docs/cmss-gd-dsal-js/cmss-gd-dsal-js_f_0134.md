## 搜索

正如你所知道的，搜索意味着在列表中查找一个值并返回它的索引。我们已经看到，数组的线性搜索速度为 O(N)，因为计算机需要逐个检查每个值。

链表的搜索速度也是 O(N)。为了搜索一个值，我们需要经过一个类似于读取的过程；也就是说，我们从头节点开始，沿着每个节点的链接前往下一个节点。在这个过程中，我们检查每个值，直到找到我们要找的内容。

### 代码实现：链表搜索

下面是我们如何在 JavaScript 中实现搜索操作。我们将这个方法称为`search`，并传入我们要搜索的值：

| ​  | `search(value) {` |
| --- | --- |
| ​  | `let` currentNode = `this`.firstNode; |
| ​  | `let` currentIndex = 0; |
| ​  |  |
| ​  | `while` (`true`) { |
| ​  | `if` (currentNode.data === value) { |
| ​  | `return` currentIndex; |
| ​  | } |
| ​  |  |
| ​  | currentNode = currentNode.nextNode; |
| ​  |  |
| ​  | `if` (!currentNode) { |
| ​  | `break`; |
| ​  | } |
| ​  |  |
| ​  | currentIndex += 1; |
| ​  | } |
| ​  |  |
| ​  | `return` `null`; |
| ​  | } |

然后，我们可以在列表中搜索任何值，如下所示：

| ​  | `list.search`(`'time'`); |
| --- | --- |

使用这个方法，我们可以得到`time`在列表中的索引。在我们上面的例子中，这个索引是 3。

正如你所看到的，搜索的机制类似于读取。主要的区别在于循环并不会停在特定的索引，而是一直运行，直到我们找到值或到达列表的末尾。
