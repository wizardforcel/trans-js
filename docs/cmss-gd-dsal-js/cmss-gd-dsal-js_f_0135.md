## 插入

不可否认的是，从性能的角度来看，链表尚未给我们留下深刻印象。它们在搜索方面不比数组好，在读取方面更糟。但不用担心——链表将有它们的时刻。实际上，那一刻就是现在。

插入是链表在某些情况下相对于数组具有明显优势的一项操作。

回想一下，插入数组的最坏情况是程序在索引`0`插入数据，因为它首先必须将其余数据向右移动一个单元，这最终导致效率为`O(N)`。然而，在链表中，在列表的开头插入只需一步——即`O(1)`。让我们看看为什么。

假设我们有以下链表：

![images/pitting_linked_lists_against_arrays/linked_list_2.png](images/pitting_linked_lists_against_arrays/linked_list_2.png)

如果我们想将`"yellow"`添加到列表的开头，我们所要做的就是创建一个新节点，并使其链接指向包含`"blue"`的节点：

![images/pitting_linked_lists_against_arrays/insert_yellow_node.png](images/pitting_linked_lists_against_arrays/insert_yellow_node.png)

（在我们的代码中，我们还需要更新`LinkedList`实例，以便其`firstNode`属性现在指向这个`"yellow"`节点。）

与数组相比，链表提供了在不需要移动任何数据的情况下向列表前面插入数据的灵活性。这多么甜美啊？

事实是，从理论上讲，在链表中任何位置插入数据只需一步，但有一个小问题。让我们继续我们的例子。

这是我们现在的链表：

![images/pitting_linked_lists_against_arrays/linked_list_3.png](images/pitting_linked_lists_against_arrays/linked_list_3.png)

假设我们现在想在索引`2`插入`"purple"`（这将位于`"blue"`和`"green"`之间）。实际插入只需一步；也就是说，我们可以创建新的`"purple"`节点，并简单地将`"blue"`节点的链接指向`"purple"`节点，如下所示：

![images/pitting_linked_lists_against_arrays/insert_purple_node.png](images/pitting_linked_lists_against_arrays/insert_purple_node.png)

但是，为了让计算机做到这一点，它首先需要到达索引`1`的节点（`"blue"`），以便它可以修改其链接指向新创建的节点。如我们所见，从链表中读取——即访问给定索引处的项——已经需要`O(N)`。让我们看看这个过程。

我们知道我们想在索引`1`之后添加一个新节点。因此，计算机需要到达列表的索引`1`。为此，我们必须从列表的开头开始：

![images/pitting_linked_lists_against_arrays/linked_list_4.png](images/pitting_linked_lists_against_arrays/linked_list_4.png)

然后通过跟随第一个链接访问下一个节点：

![images/pitting_linked_lists_against_arrays/linked_list_5.png](images/pitting_linked_lists_against_arrays/linked_list_5.png)

现在我们已经找到了索引`1`，我们终于可以添加新节点：

![images/pitting_linked_lists_against_arrays/insert_purple_node.png](images/pitting_linked_lists_against_arrays/insert_purple_node.png)

在这种情况下，添加`"purple"`花费了三步。如果我们要将其添加到列表末尾，则需要五步：四步访问索引`3`，一步插入新节点。

从实际角度来看，在链表中插入是`O(N)`，因为在列表末尾插入的最坏情况将需要`N + 1`步。

然而，我们已经看到在列表开头插入的最好情况仅为`O(1)`。

有趣的是，我们的分析表明，数组和链表的最好和最坏情况是相互对立的。下表对此进行了详细说明：

| 场景 | 数组 | 链表 |
| --- | --- | --- |
| 在开头插入 | 最坏情况 | 最好情况 |
| 在中间插入 | 平均情况 | 平均情况 |
| 在末尾插入 | 最好情况 | 最坏情况 |

正如你所看到的，数组更倾向于在末尾插入，而链表则更倾向于在开头插入。

我们现在发现了链表在某一方面的优越性——在列表开头插入东西。在本章稍后，我们将看到一个很好的实际例子，说明我们可以利用这一点。

### 代码实现：链表插入

让我们为我们的`LinkedList`类添加一个插入方法。我们将其命名为`insert`：

| ​  | `insert(index, value)` { |
| --- | --- |
| ​  | `const` newNode = `new` `Node`(value); |
| ​  |  |
| ​  | `if` (index === 0) { |
| ​  | `newNode.nextNode` = `this`.firstNode; |
| ​  | `this`.firstNode = `newNode`; |
| ​  | `return`; |
| ​  | } |
| ​  |  |
| ​  | `let` currentNode = `this`.firstNode; |
| ​  | `let` currentIndex = 0; |
| ​  |  |
| ​  | `while` (currentIndex < (index - 1)) { |
| ​  | `currentNode` = `currentNode.nextNode`; |
| ​  | `currentIndex` += 1; |
| ​  | } |
| ​  |  |
| ​  | `newNode.nextNode` = `currentNode.nextNode`; |
| ​  |  |
| ​  | `currentNode.nextNode` = `newNode`; |
| ​  | } |

要使用该方法，我们需要传入新的值以及要插入的位置索引。

例如，要在索引2插入“purple”，我们可以这样做：

| ​  | `list.insert(2, "purple");` |
| --- | --- |

让我们来分析这个插入方法。

首先，我们创建一个新的 `Node` 实例，并将值传递给我们的方法：

| ​  | `const` newNode = `new` `Node`(value); |
| --- | --- |

（这里，`node.Node`中的节点是指我们在文件开头导入的节点模块，因为我们将`Node`类放在与`LinkedList`类不同的文件中。）

接下来，我们处理插入到索引0的情况——即在列表的开头。这个情况下的算法与我们在列表的其他地方插入时不同，因此我们单独处理这个情况。

要在列表的开头插入，我们只需让我们的`newNode`链接到列表的第一个节点，并声明我们的`newNode`为接下来的第一个节点：

| ​  | `if` (index === 0) { |
| --- | --- |
| ​  | `newNode.nextNode` = `this`.firstNode; |
| ​  | `this`.firstNode = `newNode`; |
| ​  | `return`; |
| ​  | } |

`return`关键字提前结束方法，因为没有其他事情需要做。

其余的代码处理的是在开头以外的任何地方插入的情况。

与读取和搜索一样，我们首先访问列表的头：

| ​  | `let` currentNode = `this`.firstNode; |
| --- | --- |
| ​  | `let` currentIndex = 0; |

我们然后使用`while`循环访问我们想要插入`newNode`的前一个节点：

| ​  | `while` (currentIndex < (index - 1)) { |
| --- | --- |
| ​  | `currentNode` = `currentNode.nextNode`; |
| ​  | `currentIndex` += 1; |
| ​  | } |

此时，`currentNode`是将立即位于我们`newNode`之前的节点。

接下来，我们将`newNode`的链接设置为指向`currentNode`后面的节点：

| ​  | `newNode.nextNode` = `currentNode.nextNode`; |
| --- | --- |

最后，我们将`currentNode`（再次强调，它是位于`newNode`之前的节点）的链接更改为指向我们的`newNode`：

| ​  | `currentNode.nextNode` = `newNode`; |
| --- | --- |

并且我们完成了！
