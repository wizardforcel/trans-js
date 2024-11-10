## `删除`

链表在删除方面也表现出色，特别是在从列表的开头删除时。

要从链表的开头删除一个节点，我们只需执行一步：将链表的 `firstNode` 更改为指向第二个节点。

让我们回到包含值 `"once"`、`"upon"`、`"a"` 和 `"time"` 的链表示例。如果我们想要删除值 `"once"`，我们可以简单地将链表的起始点改为 `"upon"`：

| ​  | `list`.firstNode = `node2`; |
| --- | --- |

与数组对比，在数组中删除第一个元素意味着将所有剩余数据向左移动一个单元，这需要 `O(N)` 的时间。

在删除链表的最后一个节点时，实际删除只需一步——我们只需将倒数第二个节点的链接设为 null。然而，要访问倒数第二个节点则需要 `N` 步，因为我们需要从链表的开头开始，跟随链接直到达到它。

下表对比了数组和链表的各种删除场景。注意这与插入是相同的：

| 情况 | 数组 | 链表 |
| --- | --- | --- |
| 在开头删除 | 最坏情况 | 最好情况 |
| 在中间删除 | 平均情况 | 平均情况 |
| 在末尾删除 | 最好情况 | 最坏情况 |

虽然从链表的开头或结尾删除是直接的，但从中间的任何位置删除稍微复杂一些。

假设我们想从示例颜色链表中删除索引为 2 (`"purple"`) 的值，如下图所示：

![images/pitting_linked_lists_against_arrays/list_of_colors.png](images/pitting_linked_lists_against_arrays/list_of_colors.png)

为了实现这一点，我们需要先访问我们要删除的节点（`"blue"`）前面的节点。然后我们将其链接更改为指向删除节点后面的节点（`"green"`）。

下面的可视化演示了我们将 `"blue"` 节点的链接从 `"purple"` 更改为 `"green"`：

![images/pitting_linked_lists_against_arrays/linked_list_6.png](images/pitting_linked_lists_against_arrays/linked_list_6.png)

有趣的是，每当我们从链表中删除一个节点时，该节点在内存中仍然存在。我们只是通过确保链表中的其他节点不再链接到它来将其从链表中移除。这会导致节点在链表中被删除，即使该节点在内存中仍然存在。

（不同的编程语言以各种方式处理这些被删除的节点。有些会自动检测到它们不再被使用，并进行“垃圾回收”，释放内存。）

### `代码实现`：`链表删除`

下面是我们 `LinkedList` 类中的删除操作可能的样子。它被称为 `delete`，我们传入要删除的索引：

| ​  | ​`delete`(index) { |
| --- | --- |
| ​  | ​`if` (index === 0) { |
| ​  | ​`this`.firstNode = `this`.firstNode.nextNode; |
| ​  | `return`; |
| ​  | } |
| ​  |  |
| ​  | `let` currentNode = `this`.firstNode; |
| ​  | `let` currentIndex = 0; |
| ​  |  |
| ​  | `while` (currentIndex < (index - 1)) { |
| ​  | currentNode = currentNode.nextNode; |
| ​  | currentIndex += 1; |
| ​  | } |
| ​  |  |
| ​  | `const` nodeAfterDeletedNode = currentNode.nextNode.nextNode; |
| ​  | currentNode.nextNode = nodeAfterDeletedNode; |
| ​  | } |

这个方法与我们之前看到的插入方法非常相似。让我们突出一些新颖之处。

该方法首先处理一个索引为0的情况，意味着我们打算删除列表的第一个节点。对此的代码简单得离谱：

| ​  | `if` (index === 0) { |
| --- | --- |
| ​  | `this`.firstNode = `this`.firstNode.nextNode; |
| ​  | `return`; |
| ​  | } |

我们所做的就是将列表的`firstNode`指向当前的第二个节点，然后完成！

剩下的方法处理从列表中其他位置的删除。为此，我们使用一个`while`循环来访问我们想要删除的节点之前的节点。这成为我们的`currentNode`。

我们然后获取紧跟在我们要删除的节点之后的节点，并将其存储在名为`nodeAfterDeletedNode`的变量中：

| ​  | `const` nodeAfterDeletedNode = currentNode.nextNode.nextNode; |
| --- | --- |

请注意我们访问那个节点的小技巧。它只是紧跟在`currentNode`之后的两个节点！

然后我们修改`currentNode`的链接，使其指向`nodeAfterDeletedNode`：

| ​  | currentNode.nextNode = nodeAfterDeletedNode; |
| --- | --- |
