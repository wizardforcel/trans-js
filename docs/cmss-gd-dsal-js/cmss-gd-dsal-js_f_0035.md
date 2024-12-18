## `对数`

让我们看看为什么像`二分搜索`这样的算法被描述为`O(log N)`。究竟什么是对数？

`Log`是`对数`的缩写。首先要注意的是，`logarithm`这个词与`algorithm`没有任何关系，尽管这两个词看起来和听起来非常相似。

`对数`是指数的逆。下面是关于指数的快速复习：

`2³`相当于

`2 * 2 * 2`。

这正好是`8`。

现在，`log[2] 8`是反向的。它的意思是：你需要多少次将`2`自乘才能得到`8`的结果？

因为你需要将`2`自乘三次才能得到`8`，所以`log[2] 8 = 3`。

这里还有一个例子：

`2⁶`可以转化为

`2 * 2 * 2 * 2 * 2 * 2 = 64`。

因为我们需要将`2`自乘六次才能得到`64`，因此我们有，

`log[2] 64 = 6`。

虽然前面的解释是对数的“教科书”定义，但我喜欢用另一种方式描述同一概念，因为很多人发现这样更容易理解，尤其是在涉及`大 O`记号时。

解释`log[2] 8`的另一种方法是：如果我们不断将`8`除以`2`直到结果为`1`，我们的方程中有多少个`2`？

`8 / 2 / 2 / 2 = 1`

换句话说，我们需要将`8`减半多少次才能得到`1`？在这个例子中，我们需要三次。因此，

`log[2] 8 = 3`。

同样，我们可以这样解释`log[2] 64`：我们需要将`64`减半多少次才能得到`1`？

`64 / 2 / 2 / 2 / 2 / 2 / 2 = 1`

由于有六个`2`，所以`log[2] 64 = 6`。

现在你明白了对数的含义，`O(log N)`背后的意义就会变得清晰。
