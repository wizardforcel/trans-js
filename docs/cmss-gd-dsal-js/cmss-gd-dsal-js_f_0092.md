## 队列

队列是另一种数据结构，旨在处理临时数据。在许多方面，它与栈类似，只是处理数据的顺序不同。与栈一样，队列也是一种抽象数据类型。

你可以将队列看作电影剧院排队的人。排在最前面的人是第一个离开队列并进入剧院的人。对于队列来说，最先添加到队列的项是最先被移除的项。这就是计算机科学家将FIFO（先进先出）这个缩写应用于队列的原因。

与排队的人一样，队列通常被横向表示。通常也称队列的前端为“前”，队列的末端为“后”。

像栈一样，队列是具有三项限制的数组（只是一组不同的限制）：

+   数据只能在队列的末尾插入。（这与栈的行为相同。）

+   数据只能从队列的前面删除。（这与栈的行为相反。）

+   只有队列前面的元素可以被读取。（这同样与栈的行为相反。）

让我们看看一个正在运行的队列，从一个空队列开始。

首先，我们插入一个5（插入到队列中的常用术语是入队，但我们将交替使用插入和入队这两个术语）：

![images/stacks_and_queues/insert_5.png](images/stacks_and_queues/insert_5.png)

接下来，我们插入一个9：

![images/stacks_and_queues/insert_9.png](images/stacks_and_queues/insert_9.png)

接下来，我们插入一个100：

![images/stacks_and_queues/insert_100.png](images/stacks_and_queues/insert_100.png)

到目前为止，队列的功能就像一个栈。然而，移除数据的顺序是相反的，因为我们是从队列的前面移除数据。（从队列中移除元素也称为出队。）

如果我们想要移除数据，我们必须从5开始，因为它在队列的前面：

![images/stacks_and_queues/remove_5.png](images/stacks_and_queues/remove_5.png)

接下来，我们移除9：

![images/stacks_and_queues/remove_9.png](images/stacks_and_queues/remove_9.png)

我们的队列现在只包含一个元素，100。

### 队列实现

我提到过队列是一种抽象数据类型。与许多其他抽象数据类型一样，它在许多编程语言中并没有实现。以下是队列的一种实现：

| ​  | ​`class`​ `Queue` { |
| --- | --- |
| ​  | ​`constructor`​() { |
| ​  | ​`this`.data = []; |
| ​  | } |
| ​  |  |
| ​  | `enqueue(element)` { |
| ​  | ​`this`.data.push(element); |
| ​  | } |
| ​  |  |
| ​  | `dequeue()` { |
| ​  | ​`if`​ (`this`.data.length > 0) { |
| ​  | ​`return`​ ​`this`.data.shift(); |
| ​  | } ​`else`​ { |
| ​  | ​`return`​ ​`null`​; |
| ​  | } |
| ​  | } |
| ​  |  |
| ​  | `read()` { |
| ​  | ​`if`​ (`this`.data.length > 0) { |
| ​  | ​`return`​ ​`this`.data[0]; |
| ​  | } ​`else`​ { |
| ​  | ​`return`​ ​`null`​; |
| ​  | } |
| ​  | } |
| ​  | } |
| ​  | ​`export`​ ​`default`​ `Queue`; |

再次，我们的`Queue`类用一个接口封装了数组，限制了我们与数据的交互，只允许我们以特定的方式处理数据。`enqueue`方法允许我们在数组的末尾插入数据，而`dequeue`则移除数组中的第一个项目。`read`方法允许我们查看数组的第一个元素。
