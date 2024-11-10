## 双向链表作为队列

因为双向链表可以立即访问列表的前端和末尾，它们可以在任一侧以 O(1) 插入数据，也可以在任一侧以 O(1) 删除数据。

因为双向链表可以在 O(1) 时间内在末尾插入数据，并在 O(1) 时间内从前面删除数据，因此它们是队列的完美底层数据结构。

我们看过[​*队列*​](f_0092.xhtml#sect.queues)，你会记得它们是只能在末尾插入数据、从开头移除数据的项列表。你了解到队列是抽象数据类型的一个示例，我们能够使用数组在底层实现它们。

现在，由于队列在末尾插入并从开头删除，数组作为底层数据结构的效果有限。虽然数组在末尾插入的时间复杂度是 O(1)，但在开头删除的时间复杂度是 O(N)。

双向链表在末尾插入和从开头删除的时间复杂度都是 O(1)。这使它非常适合作为队列的底层数据结构。

### 代码实现：基于双向链表的队列

在实现队列之前，我们首先要为`DoublyLinkedList`类添加一个方法。这个`popHead`方法从列表中移除头节点并返回它：

| ​  | popHead() { |
| --- | --- |
| ​  | `const` poppedNode = `this`.firstNode; |
| ​  | `this`.firstNode = `this`.firstNode.nextNode; |
| ​  | `this`.firstNode.previousNode = `null`; |
| ​  | `return` poppedNode; |
| ​  | } |

如你所见，我们通过将列表的`this.firstNode`更改为当前的第二个节点，实际上删除了第一个节点。我们还确保新的头节点不链接到任何先前的节点。最后，我们返回刚刚删除的节点。

有了这一点，我们现在可以创建一个基于双向链表的队列实现：

| ​  | `import` DoublyLinkedList `from` *'./doubly_linked_list.js'*; |
| --- | --- |
| ​  |  |
| ​  | `class` Queue { |
| ​  | `constructor`() { |
| ​  | `this`.data = `new` DoublyLinkedList(); |
| ​  | } |
| ​  |  |
| ​  | enqueue(element) { |
| ​  | `this`.data.append(element); |
| ​  | } |
| ​  |  |
| ​  | dequeue() { |
| ​  | `const` dequeuedNode = `this`.data.popHead(); |
| ​  | `return` dequeuedNode.data; |
| ​  | } |
| ​  |  |
| ​  | read() { |
| ​  | `if` (!`this`.data.firstNode) { `return` `null`; } |
| ​  |  |
| ​  | `return` `this`.data.firstNode.data; |
| ​  | } |
| ​  | } |

`Queue`类在我们的`DoublyLinkedList`之上实现其方法。`enqueue`方法依赖于我们`DoublyLinkedList`的`append`方法：

| ​  | enqueue(element) { |
| --- | --- |
| ​  | `this`.data.append(element); |
| ​  | } |

同样，`dequeue`方法利用链表从列表前端删除的能力：

| ​  | dequeue() { |
| --- | --- |
| ​  | `const` dequeuedNode = `this`.data.popHead(); |
| ​  | `return` dequeuedNode.data; |
| ​  | } |

通过使用双向链表实现我们的队列，我们现在可以以快速的 O(1) 速度在队列中插入和删除。这真是太棒了。
