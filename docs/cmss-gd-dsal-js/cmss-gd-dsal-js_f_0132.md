## 实现链表

一些编程语言，如Java，内置了链表。许多语言没有，但我们自己实现链表是相当简单的。

让我们使用JavaScript创建自己的链表。我们将使用两个类来实现这一点：`Node`和`LinkedList`。我们先创建`Node`类：

| ​  | `class` Node { |
| --- | --- |
| ​  | `constructor`(data) { |
| ​  | `this`.data = data; |
| ​  | `this`.nextNode = `null`; |
| ​  | } |
| ​  | } |
| ​  |  |
| ​  | `export` `default` Node; |

`Node`类有两个属性：`data`包含节点的主要值（例如字符串`"a"`），而`nextNode`包含指向列表中下一个节点的链接。我们可以如下使用这个类：

| ​  | `const` node1 = `new` Node(*'once'*); |
| --- | --- |
| ​  | `const` node2 = `new` Node(*'upon'*); |
| ​  | `const` node3 = `new` Node(*'a'*); |
| ​  | `const` node4 = `new` Node(*'time'*); |
| ​  |  |
| ​  | node1.nextNode = node2; |
| ​  | node2.nextNode = node3; |
| ​  | node3.nextNode = node4; |

使用这段代码，我们创建了一个包含四个节点的列表，这些节点包含字符串`'once'`、`'upon'`、`'a'`和`'time'`。

请注意，在我们的实现中，`nextNode`指的是另一个`Node`实例，而不是实际的内存地址号。效果是一样的——这些节点很可能分散在计算机的内存中，但我们可以使用节点的链接将列表串联起来。

接下来，我们将简单讨论每个链接指向另一个节点，而不是特定的内存地址。因此，我们将使用简化的图示来描绘链表，例如这个：

![images/pitting_linked_lists_against_arrays/once_upon_a_time.png](images/pitting_linked_lists_against_arrays/once_upon_a_time.png)

此图中的每个节点由两个单元组成。第一个单元包含节点的数据，第二个单元指向下一个节点。

这反映了我们对`Node`类的实现。在其中，`data`方法返回节点的数据，而`nextNode`方法返回列表中的下一个节点。在这个上下文中，`nextNode`方法作为节点的链接。

尽管我们仅凭`Node`类就能够创建这个链表，但我们仍然需要一个简单的方法来告诉程序链表的起始位置。为此，我们将创建一个`LinkedList`类，除了之前的`Node`类。下面是`LinkedList`类的基本形式：

| ​  | `import` Node `from` *'./node.js'*; |
| --- | --- |
| ​  |  |
| ​  | `class` LinkedList { |
| ​  | `constructor`(firstNode=`null`) { |
| ​  | `this`.firstNode = firstNode; |
| ​  | } |
| ​  | } |

请注意，我们在代码开始时导入了node，因为我们将`Node`类放在了与`LinkedList`类不同的文件中。

此时，所有`LinkedList`实例做的就是跟踪列表的第一个节点。

之前我们创建了一个包含`node1`、`node2`、`node3`和`node4`的节点链。现在我们可以使用我们的`LinkedList`类来引用这个列表，通过写以下代码：

| ​  | ​`const`​ list = ​`new`​ `LinkedList(node1)`; |
| --- | --- |

这个列表变量现在作为链表的句柄，因为它是`LinkedList`的一个实例，具有访问列表第一个节点的能力。

一个重要的观点出现了：在处理链表时，我们只能立即访问它的头节点。这将会带来严重的后果，正如我们将很快看到的那样。

乍一看，链表和数组是相似的——它们都是一系列的元素。但是，当我们深入分析时，会看到这两种数据结构在性能上的一些显著差异！让我们深入了解四个经典操作：读取、搜索、插入和删除。
