## `双向链表`

链表有多种不同的变种。我们到目前为止讨论的链表是经典链表，但通过一些轻微的修改，我们可以赋予链表额外的超能力。

链表的一种变体是双向链表。

双向链表类似于链表，只是每个节点有两个链接——一个指向下一个节点，另一个指向上一个节点。此外，双向链表总是跟踪头节点和尾节点，而不仅仅是头节点。

这是双向链表的外观：

![images/pitting_linked_lists_against_arrays/doubly_linked_list.png](images/pitting_linked_lists_against_arrays/doubly_linked_list.png)

我们可以像这样在 JavaScript 中实现双向链表的核心。首先，我们必须创建一种新的“双端”节点：

| ​  | `class Node {` |
| --- | --- |
| ​  | `constructor(data) {` |
| ​  | `this.data = data;` |
| ​  | `this.nextNode = null;` |
| ​  | `this.previousNode = null;` |
| ​  | } |
| ​  | } |
| ​  |  |
| ​  | `export default Node;` |

你会注意到每个节点现在不仅包含一个`nextNode`属性，还包含一个`previousNode`属性。

一旦我们有了这个，我们现在可以实现我们的双向链表：

| ​  | `import Node from './double_ended_node.js';` |
| --- | --- |
| ​  |  |
| ​  | `class DoublyLinkedList {` |
| ​  | `constructor(firstNode=null, lastNode=null) {` |
| ​  | `this.firstNode = firstNode;` |
| ​  | `this.lastNode = lastNode;` |
| ​  | } |
| ​  | } |

由于双向链表总是知道它的头部和尾部，我们可以在一个步骤内访问它们，或者说是 O(1)。因此，正如我们可以在 O(1) 中从链表的开头读取、插入或删除一样，我们也可以在 O(1) 中从链表的末尾执行相同的操作。

这是在双向链表末尾插入的示意图：

![images/pitting_linked_lists_against_arrays/insert_into_doubly_linked_list.png](images/pitting_linked_lists_against_arrays/insert_into_doubly_linked_list.png)

如你所见，我们创建了一个新节点（"Sue"），并让它的`previousNode`指向原来的`lastNode`（"Greg"）。然后我们将`lastNode`（"Greg"）的`nextNode`更改为指向这个新节点（"Sue"）。最后，我们将新节点（"Sue"）声明为链表的`lastNode`。

### 代码实现：双向链表插入

接下来，我们将查看可以添加到`DoublyLinkedList`类的新`append`方法的实现。`append`方法并不是在链表中的任意位置插入值，而是简单地在链表的末尾添加一个新值。我们专注于追加，而不是经典插入，旨在突出显示向双向链表追加是多么简单和快速。以下是`append`方法：

| ​  | `append(value) {` |
| --- | --- |
| ​  | `const newNode = new Node(value);` |
| ​  |  |
| ​  | `if (!this.firstNode) {` |
| ​  | ​`this`​.firstNode = `newNode`; |
| ​  | ​`this`​.lastNode = `newNode`; |
| ​  | } ​`else`​ { |
| ​  | `newNode`.previousNode = ​`this`​.lastNode; |
| ​  | ​`this`​.lastNode.nextNode = `newNode`; |
| ​  | ​`this`​.lastNode = `newNode`; |
| ​  | } |
| ​  | } |

让我们强调这个方法中最重要的部分。

首先，我们创建新的节点：

| ​  | ​`const`​ `newNode` = ​`new`​ `Node(value)`; |
| --- | --- |

起初，我们的代码处理链表为空的情况。但让我们跳到追加到现有链表的情况。

我们将`newNode`的previousNode链接指向在此之前的最后一个节点：

| ​  | `newNode`.previousNode = ​`this`​.lastNode; |
| --- | --- |

然后我们改变最后一个节点的链接（在此之前是`null`），并让它指向我们的`newNode`：

| ​  | ​`this`​.lastNode.nextNode = `newNode`; |
| --- | --- |

最后，我们告诉我们的`DoublyLinkedList`实例，它的最后一个节点是我们的`newNode`：

| ​  | ​`this`​.lastNode = `newNode`; |
| --- | --- |

### 向前和向后移动

在经典的链表中，我们只能向前移动；也就是说，我们可以访问第一个节点并跟随链接找到链表中的所有其他节点。但是我们无法向后移动，因为没有节点知道前一个节点是什么。

一个双向链表允许更多的灵活性，因为我们可以向前和向后移动。实际上，我们甚至可以从尾部开始，向后移动到头部。
