## `链表的实际应用`

链表表现突出的一个场景是当我们检查一个单一列表并从中删除多个元素时。举个例子，我们正在构建一个应用程序，它遍历现有的电子邮件地址列表并删除任何格式无效的电子邮件地址。

无论列表是数组还是链表，我们都需要逐个检查整个列表中的每个电子邮件地址。这自然需要`N`步。然而，让我们来看看每次实际删除电子邮件地址时会发生什么。

使用数组时，每次删除电子邮件地址，我们需要额外的`O(N)`步将剩余数据向左移动以填补空缺。在我们检查下一个电子邮件地址之前，所有这些移动操作都必须先完成。

假设`10`个电子邮件地址中有`1`个是无效的。如果我们有一个`1,000`个电子邮件地址的列表，那么大约会有`100`个无效地址。因此，我们的算法将需要`1,000`步来读取所有`1,000`个电子邮件地址。除此之外，删除可能需要额外的`100,000`步，因为对于每个被删除的`100`个地址，我们可能需要将多达`1,000`个其他元素向上移动。

然而，使用链表时，当我们浏览列表时，每次删除只需要一步，因为我们可以简单地改变节点的链接指向适当的节点，然后继续前进。因此，对于我们的`1,000`封电子邮件，我们的算法只需`1,100`步，因为有`1,000`次读取步骤和`100`次删除步骤。

因此，链表被证明是一种出色的数据结构，可以在进行插入或删除时遍历整个列表，因为我们在进行插入或删除时从不需要担心移动其他数据。
