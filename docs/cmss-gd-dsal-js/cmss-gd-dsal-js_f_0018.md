## 搜索

正如我之前所说，搜索数组意味着查看某个特定值是否存在于数组中，以及它位于哪个索引。

从某种意义上说，这与读取是相反的。读取意味着提供一个索引给计算机，并要求它返回其中包含的值。而搜索则是提供一个值给计算机，并要求它返回该值的位置索引。

虽然这两种操作听起来相似，但在效率方面却有天壤之别。读取索引是快速的，因为计算机可以立即跳转到任何索引并发现其中包含的值。而搜索则是繁琐的，因为计算机无法立即定位特定值。

这是一个关于计算机的重要事实：计算机可以立即访问所有内存地址，但它并不知道每个内存地址包含什么值。

以我们之前的水果和蔬菜数组为例。计算机无法立即看到每个单元的实际内容。对于计算机来说，数组看起来是这样的：

![images/understanding_arrays/linear_search_1.png](images/understanding_arrays/linear_search_1.png)

要在数组中搜索一种水果，计算机别无选择，只能逐个检查单元的内容。

下图展示了计算机在我们的数组中搜索`"dates"`的过程。

首先，计算机检查索引`0`：

![images/understanding_arrays/linear_search_2.png](images/understanding_arrays/linear_search_2.png)

由于索引`0`的值是`"apples"`，而不是我们要找的`"dates"`，计算机继续检查下一个索引，如[图](#fig.ch1.linear_search_3)所示。

![images/understanding_arrays/linear_search_3.png](images/understanding_arrays/linear_search_3.png)

由于索引`1`也不包含我们要找的`"dates"`，计算机继续检查索引`2`：

![images/understanding_arrays/linear_search_4.png](images/understanding_arrays/linear_search_4.png)

我们再次失利，所以计算机移动到下一个单元：

![images/understanding_arrays/linear_search_5.png](images/understanding_arrays/linear_search_5.png)

啊！我们找到了难以捉摸的`"dates"`，现在知道`"dates"`位于索引`3`。此时，计算机无需继续检查数组的下一个单元，因为它已经找到了我们要找的内容。

在这个例子中，由于计算机必须检查四个不同的单元，直到找到我们要搜索的值，我们可以说这个特定操作总共花费了四个步骤。

在第二章，[​*算法为何重要*​](f_0024.xhtml#chp.binary_search)中，你将学习另一种搜索数组的方法，但这种基本的搜索操作——计算机逐个检查每个单元——被称为线性搜索。

那么，计算机在对数组进行`线性搜索`时，最多需要执行多少步呢？

如果我们要寻找的值恰好在数组的最后一个单元格中（比如说`"elderberries"`），那么计算机最终会搜索数组中的每一个单元格，直到找到它所寻找的值。此外，如果我们要寻找的值根本不在数组中，计算机同样需要搜索每一个单元格，以确保该值在数组中不存在。

因此，对于一个包含5个单元格的数组，`线性搜索`最多需要执行5步。对于一个包含500个单元格的数组，`线性搜索`最多需要执行500步。

换句话说，对于数组中的`N`个单元格，`线性搜索`最多需要`N`步。在这个上下文中，`N`只是一个可以被任何数字替代的变量。

无论如何，很明显搜索的效率低于读取，因为搜索可能需要多步，而读取无论数组的长度如何始终只需一步。

接下来，我们将分析`插入`操作。
