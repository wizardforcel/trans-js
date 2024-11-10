## 第14章

这些是本节中找到的练习的解决方案[​*Exercises*​](f_0142.xhtml#pitting.linked.lists.against.arrays.exercises)。

1.  一种方法是使用简单的`while`循环：

    | ​  | printList() { |
    | --- | --- |
    | ​  | `let` currentNode = `this`.firstNode; |
    | ​  |  |
    | ​  | `while` (currentNode) { |
    | ​  | console.log(currentNode.data); |
    | ​  | currentNode = currentNode.nextNode; |
    | ​  | } |
    | ​  | } |

1.  使用双向链表，我们可以立即访问最后的节点，并通过它们的“前一个节点”链接访问前一个节点。这段代码基本上是上一个练习的反向：

    | ​  | reversePrint() { |
    | --- | --- |
    | ​  | `let` currentNode = `this`.lastNode; |
    | ​  |  |
    | ​  | `while` (currentNode) { |
    | ​  | console.log(currentNode.data); |
    | ​  | currentNode = currentNode.previousNode; |
    | ​  | } |
    | ​  | } |

1.  在这里，我们使用`while`循环遍历每个节点。然而，在向前移动之前，我们使用节点的链接检查是否有下一个节点：

    | ​  | last() { |
    | --- | --- |
    | ​  | `let` currentNode = `this`.firstNode; |
    | ​  |  |
    | ​  | `while` (currentNode.nextNode) { |
    | ​  | currentNode = currentNode.nextNode; |
    | ​  | } |
    | ​  |  |
    | ​  | `return` currentNode.data; |
    | ​  | } |

    有趣的是，这里有一个使用递归的替代实现：

    | ​  | recursiveLast(currentNode = `null`) { |
    | --- | --- |
    | ​  | `if` (!currentNode) { |
    | ​  | currentNode = `this`.firstNode; |
    | ​  | } |
    | ​  |  |
    | ​  | `if` (currentNode.nextNode) { |
    | ​  | `return` `this`.recursiveLast(currentNode.nextNode); |
    | ​  | } `else` { |
    | ​  | `return` currentNode.data; |
    | ​  | } |
    | ​  | } |

1.  反转经典链表的一种方法是遍历链表，同时跟踪三个变量。

    主要变量是`currentNode`，它是我们正在迭代的主要节点。我们还跟踪`next_node`，即紧接在`currentNode`之后的节点。同时，我们还跟踪`previousNode`，即紧接在`currentNode`之前的节点。请参见以下图示：

    ![images/pitting_linked_lists_against_arrays/solution_4_a.png](images/pitting_linked_lists_against_arrays/solution_4_a.png)

    注意，当我们第一次开始时，`currentNode`是第一个节点，`previousNode`指向`null`；在第一个节点之前没有节点。

    一旦我们设置好三个变量，就开始我们的算法，这将启动一个循环。

    在循环内部，我们首先将`currentNode`的链接更改为指向`previousNode`：

    ![images/pitting_linked_lists_against_arrays/solution_4_b.png](images/pitting_linked_lists_against_arrays/solution_4_b.png)

    然后我们将所有变量向右移动：

    ![images/pitting_linked_lists_against_arrays/solution_4_c.png](images/pitting_linked_lists_against_arrays/solution_4_c.png)

    我们再次开始循环，重复这个过程，将`currentNode`的链接指向`previousNode`，直到我们到达列表的末尾。一旦我们到达末尾，列表将完全反转。

这是这个算法的实现：

|  | `reverse() {` |
| --- | --- |
|  | `let previousNode = null;` |
|  | `let currentNode = this.firstNode;` |
|  |  |
|  | `while (currentNode) {` |
|  | `const nextNode = currentNode.nextNode;` |
|  | `currentNode.nextNode = previousNode;` |
|  |  |
|  | `previousNode = currentNode;` |
|  | `currentNode = nextNode;` |
|  | `}` |
|  |  |
|  | `this.firstNode = previousNode;` |
|  | `}` |

1.  信不信由你，我们可以在没有访问任何前驱节点的情况下删除一个中间节点。

    下面是一个示例情况的图示。我们有四个节点，但我们只能访问节点`"b"`。这意味着我们无法访问节点`"a"`，因为在经典的链表中链接只指向前方。我们用虚线表示这一点；即我们无法访问虚线左侧的任何节点：

    ![`images/pitting_linked_lists_against_arrays/solution_5_a.png`](images/pitting_linked_lists_against_arrays/solution_5_a.png)

    现在，这里是如何删除节点`"b"`的（尽管我们没有访问节点`"a"`）。为了清晰起见，我们将这个节点称为“访问节点”，因为这是我们能够访问的第一个节点。

    首先，我们获取访问节点后的下一个节点，并将其数据复制到访问节点中，覆盖访问节点的数据。在我们的示例中，这意味着将字符串`"c"`复制到我们的访问节点：

    ![`images/pitting_linked_lists_against_arrays/solution_5_b.png`](images/pitting_linked_lists_against_arrays/solution_5_b.png)

我们接着改变访问节点的链接，使其指向右侧两个节点的节点。这实际上删除了原来的`"c"`节点：

![`images/pitting_linked_lists_against_arrays/solution_5_c.png`](images/pitting_linked_lists_against_arrays/solution_5_c.png)

这段代码简短而优雅：

|  | `function deleteNode(node) {` |
| --- | --- |
|  | `node.data = node.nextNode.data;` |
|  | `node.nextNode = node.nextNode.nextNode;` |
|  | `}` |
