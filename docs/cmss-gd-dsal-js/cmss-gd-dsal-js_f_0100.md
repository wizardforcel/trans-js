## 计算机眼中的递归

为了完整理解递归，我们需要看到计算机如何处理递归函数。这对于人类来说，使用早期的“餐巾纸”方法推理递归是一回事。然而，计算机必须完成从函数内部调用函数的复杂工作。因此，让我们分解计算机执行递归函数的过程。

假设我们调用 `factorial(3)`。由于 `3` 不是基本情况，计算机到达了这一行：

| ​  | ​`return`​ `number * factorial(number - 1)`; |
| --- | --- |

这就启动了 `factorial(2)` 函数。

但有个问题。当计算机开始运行 `factorial(2)` 时，计算机是否已经完成了 `factorial(3)` 的运行？

这就是让计算机觉得递归棘手的原因。在计算机到达 `factorial(3)` 的结束关键字之前，它并没有完成 `factorial(3)`。所以我们进入了一个奇怪的情况。计算机尚未完成执行 `factorial(3)`，却在 `factorial(3)` 的中间开始运行 `factorial(2)`。

而且 `factorial(2)` 并不是故事的结束，因为 `factorial(2)` 会触发 `factorial(1)`。所以这是个疯狂的事情：在运行 `factorial(3)` 的过程中，计算机又调用了 `factorial(2)`。而在运行 `factorial(2)` 时，计算机又运行 `factorial(1)`。结果是，`factorial(1)` 在 `factorial(2)` 和 `factorial(3)` 的运行过程中同时进行。

计算机是如何跟踪这一切的？它需要某种方式来记住在完成 `factorial(1)` 后，需要返回并完成 `factorial(2)` 的运行。然后它需要记住在完成 `factorial(2)` 后再完成 `factorial(3)`。

### 调用栈

幸运的是，你最近在第9章学习了堆栈，[`*使用堆栈和队列编写优雅代码*`](f_0087.xhtml#chp.stacks_queues)。计算机使用堆栈来跟踪它正在调用的函数。这种堆栈被称为调用栈。

这是在我们的阶乘示例中调用栈的工作方式。

计算机首先调用 `factorial(3)`。然而，在方法完成执行之前，`factorial(2)` 被调用。为了跟踪计算机仍处于 `factorial(3)` 的中间，计算机将该信息推入调用栈：

![images/recursively_recurse_with_recursion/call_stack_push_factorial_3.png](images/recursively_recurse_with_recursion/call_stack_push_factorial_3.png)

这表明计算机正在运行 `factorial(3)` 的中间阶段。（实际上，计算机还需要保存它当前所在的行，以及一些其他信息，如变量值，但我将图示保持简单。）

计算机接着执行 `factorial(2)`。现在，`factorial(2)` 又调用 `factorial(1)`。不过，在计算机进入 `factorial(1)` 之前，它需要记住自己仍然处于 `factorial(2)` 的中间阶段，因此它也将这个信息推入调用栈：

![images/recursively_recurse_with_recursion/call_stack_push_factorial_2.png](images/recursively_recurse_with_recursion/call_stack_push_factorial_2.png)

计算机接着执行`factorial(1)`。由于`1`是基本情况，`factorial(1)`在没有再次调用`factorial`方法的情况下完成。

在计算机完成`factorial(1)`后，它检查调用栈以查看是否在其他函数中。如果调用栈中还有东西，意味着计算机仍然有工作要做——也就是说，需要结束它正在处理的其他函数。

如果你还记得，栈是有限制的，我们只能弹出其顶部元素。这对递归来说是理想的，因为顶部元素将是最近调用的函数，而这正是计算机需要接下来结束的函数。这是一个后进先出（LIFO）情况：最后被调用的函数（即最近调用的）是我们需要首先完成的函数。

计算机接下来的操作是弹出调用栈的顶部元素，当前是`factorial(2)`：

![images/recursively_recurse_with_recursion/call_stack_pop_factorial_2.png](images/recursively_recurse_with_recursion/call_stack_pop_factorial_2.png)

计算机接着完成`factorial(2)`的执行。

现在，计算机从栈中弹出下一个项目。这时，栈中只剩下`factorial(3)`，因此计算机弹出它，从而完成运行`factorial(3)`。

此时，栈为空，因此计算机知道它已经完成所有方法的执行，递归完成。

从鸟瞰的角度回顾这个例子，你会看到计算机计算`factorial(3)`的顺序如下：

1.  `factorial(3)`被第一次调用。在它完成之前……

1.  `factorial(2)`被第二次调用。在它完成之前……

1.  `factorial(1)`被第三次调用。

1.  `factorial(1)`首先完成。

1.  `factorial(2)`基于`factorial(1)`的结果完成。

1.  最后，`factorial(3)`基于`factorial(2)`的结果完成。

`factorial`函数是基于递归的计算。最终的计算是由`factorial(1)`将其结果（即`1`）传递给`factorial(2)`。然后`factorial(2)`将这个`1`乘以`2`，得到`2`，并将这个结果传递给`factorial(3)`。最后，`factorial(3)`将这个结果乘以`3`，计算出结果`6`。

有人将这个概念称为将值通过调用栈向上传递；也就是说，每个递归函数将其计算值返回给其“父”函数。最终，最初被调用的函数计算出最终值。

### `栈溢出`

让我们回顾一下本章开头的无限递归示例。记得`blah()`无限调用自身吗？你认为调用栈会发生什么？

在无限递归的情况下，计算机不断将相同的`function`重复推入调用栈。调用栈不断增长，直到最终，计算机达到一个点，此时其短期内存中根本没有足够的空间来容纳所有这些数据。这会导致一个错误，称为`栈溢出`——计算机会直接停止递归并说：“我拒绝再次调用这个`function`，因为我快没内存了！”
