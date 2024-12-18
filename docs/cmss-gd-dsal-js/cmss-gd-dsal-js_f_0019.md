## `Insertion`

在数组中插入新数据的效率取决于你插入的位置。

假设我们想要将`"figs"`添加到购物清单的末尾。这样的插入只需要一步。

这是真的，因为计算机在分配数组时，总是会跟踪数组的长度。

当我们将这与计算机知道数组开始的内存地址结合起来时，计算数组最后一个项的内存地址就变得轻而易举：如果数组从内存地址1010开始，且长度为5，那么它的最后一个内存地址就是1014。因此，要在那之后插入一个项，就意味着将其添加到下一个内存地址，即1015。

一旦计算机计算出要将新值插入到哪个内存地址，它可以在一步内完成。

这就是将`"figs"`插入数组末尾的样子：

![images/understanding_arrays/array_10.png](images/understanding_arrays/array_10.png)

但是有一个问题。因为计算机最初仅为数组分配了五个内存单元，而现在我们要添加第六个元素，计算机可能需要为这个数组分配额外的单元。在许多编程语言中，这是在后台自动完成的，但每种语言的处理方式不同，所以我不打算深入细节。

我们已经处理了数组末尾的插入，但在数组开头或中间插入新数据是另一回事。在这些情况下，我们需要移动数据以为插入的内容腾出空间，这会导致额外的步骤。

例如，假设我们想要将`"figs"`添加到数组的索引2。看看下面的图示：

![images/understanding_arrays/array_11.png](images/understanding_arrays/array_11.png)

为此，我们需要将`"cucumbers"`、`"dates"`和`"elderberries"`向右移动，以便为`"figs"`腾出空间。这需要多个步骤，因为我们首先需要将`"elderberries"`向右移动一个单元，以便为`"dates"`腾出空间。接着，我们需要移动`"dates"`以腾出空间给`"cucumbers"`。让我们来逐步了解这个过程。

`Step 1`: 我们将`"elderberries"`向右移动：

![images/understanding_arrays/array_12.png](images/understanding_arrays/array_12.png)

`Step 2`: 我们现在将`"dates"`向右移动：

![images/understanding_arrays/array_13.png](images/understanding_arrays/array_13.png)

`Step 3`: 我们现在将`"cucumbers"`向右移动：

![images/understanding_arrays/array_14.png](images/understanding_arrays/array_14.png)

`Step 4`: 最后，我们可以将`"figs"`插入到索引2：

![images/understanding_arrays/array_15.png](images/understanding_arrays/array_15.png)

注意在前面的例子中，插入花费了四个步骤。三个步骤涉及将数据向右移动，而一个步骤涉及新值的实际插入。

对于数组的插入操作，最坏的情况是当我们在数组的开头插入数据。这是因为在数组开头插入时，我们必须将所有其他值向右移动一个单元格。

我们可以说，在最坏情况下，对于一个包含`N`个元素的数组，插入可能需要`N + 1`步。这是因为我们需要移动所有`N`个元素，然后最后执行实际的插入步骤。

现在我们已经涵盖了插入操作，接下来是数组的最后一个操作：删除。
