## 数组作为堆

由于找到最后一个节点对堆的操作至关重要，并且我们希望确保找到最后一个节点的效率，堆通常使用数组来实现。

直到现在，我们一直假设每棵树由相互连接的独立节点组成（就像链表一样），你现在会看到我们也可以使用数组来实现堆。堆本身可以是一个抽象数据类型，底层实际上使用数组。

[图示](#fig.ch16.heap_as_array)展示了如何使用数组来存储堆的值。

其工作原理是将每个节点分配给数组中的一个索引。在这个图示中，每个节点的索引在节点下方的方框中找到。如果你仔细观察，会发现我们根据特定的模式分配每个节点的索引。

![images/heaps/heap_as_array.png](images/heaps/heap_as_array.png)

根节点始终存储在索引`0`。然后我们向下移动一层，从左到右，分配每个节点到数组中的下一个可用索引。因此，在第二层，左节点（`88`）成为索引`1`，右节点（`25`）成为索引`2`。当我们到达一层的末尾时，就下移到下一层并重复此模式。

现在，我们使用数组来实现堆的原因是它解决了最后一个节点的问题。怎么解决的？

以这种方式实现堆时，最后一个节点将始终是数组的最后一个元素。由于我们在分配每个值时是从上到下、从左到右的，因此最后一个节点始终是数组中的最后一个值。在之前的示例中，你可以看到`3`，它是最后一个节点，是数组中的最后一个值。

因为最后一个节点总是位于数组的末尾，所以找到最后一个节点变得很简单：我们只需访问最后一个元素。此外，当我们向堆中插入一个新节点时，我们会将其放在数组的末尾，以使其成为最后一个节点。

在我们深入了解基于数组的堆的其他细节之前，可以开始编码其基本结构。以下是我们在 JavaScript 中实现堆的开头部分：

| ​  | ​`class`​ `Heap` { |
| --- | --- |
| ​  | ​`constructor`​() { |
| ​  | ​`this`.data = []; |
| ​  | } |
| ​  |  |
| ​  | `rootNode()` { |
| ​  | ​`return` ​`this`.data[0]; |
| ​  | } |
| ​  |  |
| ​  | `lastNode()` { |
| ​  | ​`return` ​`this`.data[​`this`.data.length - 1]; |
| ​  | } |
| ​  | } |

如你所见，我们将堆初始化为空数组。我们有一个`rootNode`方法，它返回该数组的第一个元素，还有一个`lastNode`方法，它返回该数组的最后一个值。

### 遍历基于数组的堆

正如你所见，堆的插入和删除算法要求我们能够在堆中逐步移动。逐步移动又要求我们能够通过访问节点的父节点或子节点来遍历堆。但是，当所有值仅存储在数组中时，我们如何从一个节点移动到另一个节点呢？如果我们能简单地跟随每个节点的链接，遍历堆将是直接的。但现在堆的底层是一个数组，我们怎么知道哪些节点是相互连接的呢？

这个问题有一个有趣的解决方案。事实证明，当我们根据之前描述的模式分配堆节点的索引时，堆的以下特性总是成立：

+   要找到任何节点的左子节点，我们可以使用公式 (`index` * 2) + 1。

+   要找到任何节点的右子节点，我们可以使用公式 (`index` * 2) + 2。

再看看之前的图，关注索引为 4 的 16。要找到它的左子节点，我们将它的索引（4）乘以 2 然后加 1，结果是 9。这意味着索引 9 是索引 4 的节点的左子节点。

类似地，要找到索引 4 的右子节点，我们将 4 乘以 2 然后加 2，结果是 10。这意味着索引 10 是索引 4 的右子节点。

因为这些公式总是有效的，所以我们能够将我们的数组视为树。

让我们将这两个方法添加到我们的 `Heap` 类中：

| ​  | `leftChildIndex`(`index`) { |
| --- | --- |
| ​  | ​`return` (`index` * 2) + 1; |
| ​  | } |
| ​  |  |
| ​  | `rightChildIndex`(`index`) { |
| ​  | ​`return` (`index` * 2) + 2; |
| ​  | } |

每个方法都接受数组中的一个索引，并分别返回左或右子节点的索引。

这是基于数组的堆的另一个重要特性：

+   要找到节点的父节点，我们可以使用公式 `Math.floor((index - 1) / 2)`。

请注意，这个公式使用了向下取整运算，这意味着我们会舍弃小数点后的任何数字。例如，`Math.floor(3 / 2)` 返回 1，而不是更精确的 1.5。

再次，在我们的示例堆中，关注索引 4。如果我们取那个索引，减去 1，然后除以 2，我们得到 1。正如你在图中看到的，索引 4 的节点的父节点位于索引 1。

所以现在我们可以向 `Heap` 类中添加另一个方法：

| ​  | `parentIndex`(`index`) { |
| --- | --- |
| ​  | ​`return` `Math.floor((index - 1) / 2);` |
| ​  | } |

这个方法接受一个索引并计算其父节点的索引。

### 代码实现：`Heap` 插入

现在我们已经建立了 `Heap` 的基本元素，接下来让我们实现插入算法：

| ​  | `insert`(`value`) { |
| --- | --- |
| ​  | ​`this`.data.push(value); |
| ​  | ​`let` newNodeIndex = `this`.data.length - 1; |
| ​  |  |
| ​  | ​`while` (newNodeIndex > 0 |
| ​  | && (`this`.data[`newNodeIndex`] > `this`.data[`this`.parentIndex(`newNodeIndex`)])) { |
| ​  | ​`const` parentIndex = `this`.parentIndex(newNodeIndex); |
| ​  | [`this`.data[parentIndex], `this`.data[newNodeIndex]] = |
| ​  | [`this`.data[newNodeIndex], `this`.data[parentIndex]]; |
| ​  |  |
| ​  | newNodeIndex = parentIndex; |
| ​  | } |
| ​  | } |

和往常一样，我们来详细分析一下这个过程。

我们的 `insert` 方法接受要插入到堆中的值。我们首先做的是将这个新值作为最后一个节点，添加到数组的末尾：

| ​  | `this`.data.push(value); |
| --- | --- |

接下来，我们跟踪新节点的索引，因为稍后我们将需要它。目前，索引是数组中的最后一个索引：

| ​  | `let` newNodeIndex = `this`.data.length - 1; |
| --- | --- |

接下来，我们使用 `while` 循环将新节点逐步移动到其正确的位置：

| ​  | `while` (newNodeIndex > 0 |
| --- | --- |
| ​  | && (`this`.data[newNodeIndex] > `this`.data[`this`.parentIndex(newNodeIndex)]) { |

这个循环在满足两个条件的情况下运行。主要条件是新节点大于其父节点。我们还设置了一个条件，即新节点的索引必须大于0，因为如果我们尝试将根节点与其不存在的父节点进行比较，可能会出现奇怪的情况。

每次这个循环运行时，我们都会将新节点与其父节点交换，因为新节点当前大于父节点：

| ​  | `const` parentIndex = `this`.parentIndex(newNodeIndex); |
| --- | --- |
| ​  | [`this`.data[parentIndex], `this`.data[newNodeIndex]] = |
| ​  | [`this`.data[newNodeIndex], `this`.data[parentIndex]]; |

我们还会相应地更新新节点的索引：

| ​  | newNodeIndex = parentIndex; |
| --- | --- |

由于这个循环仅在新节点大于其父节点时运行，因此一旦新节点处于正确的位置，循环就结束了。

### 代码实现：堆删除

我们接下来将看看从堆中删除项目的实现。我们将这个方法命名为 `pop`，因为术语 `pop` 强调将被删除的值返回，以供其他代码使用，例如在优先级队列中（如我们稍后将看到的）。我们不仅仅是试图消除根值；我们还希望将该值传递给其他代码进行处理。

主要方法是 `pop` 方法，但为了简化代码，我们创建了两个辅助方法，`hasGreaterChild` 和 `findLargerChildIndex`。

下面开始：

| ​  | `pop()` { |
| --- | --- |
| ​  | `if` (`this`.data.length === 1) { |
| ​  | `const` valueToDelete = `this`.rootNode(); |
| ​  | `this`.data = []; |
| ​  | `return` valueToDelete; |
| ​  | } |
| ​  |  |
| ​  | `const` valueToDelete = `this`.rootNode(); |
| ​  | `this`.data[0] = `this`.data.pop(); |
| ​  | `let` trickleNodeIndex = 0; |
| ​  |  |
| ​  | `while` (`this`.hasGreaterChild(trickleNodeIndex)) { |
| ​  | `const` largerChildIndex = `this`.findLargerChildIndex(trickleNodeIndex); |
| ​  |  |
| ​  | [`this`.data[trickleNodeIndex], `this`.data[largerChildIndex]] = |
| ​  | [`this`.data[largerChildIndex], `this`.data[trickleNodeIndex]]; |
| ​  |  |
| ​  | trickleNodeIndex = largerChildIndex; |
| ​  | } |
| ​  |  |
| ​  | ​`return`​ `valueToDelete`; |
| ​  | } |
| ​  |  |
| ​  | `hasGreaterChild`(`index`) { |
| ​  | ​`return`​ ((​`this`​.leftChildIndex(`index`) < ​`this`​.data.length |
| ​  | && ​`this`​.data[​`this`​.leftChildIndex(`index`)] > ​`this`​.data[`index`] |
| ​  | &#124;&#124; (​`this`​.rightChildIndex(`index`) < ​`this`​.data.length |
| ​  | && ​`this`​.data[​`this`​.rightChildIndex(`index`)] > ​`this`​.data[`index`])); |
| ​  | } |
| ​  |  |
| ​  | `findLargerChildIndex`(`index`) { |
| ​  | ​`if`​ (!​`this`​.data[​`this`​.rightChildIndex(`index`)]) { |
| ​  | ​`return`​ ​`this`​.leftChildIndex(`index`); |
| ​  | } |
| ​  |  |
| ​  | ​`if`​ (​`this`​.data[​`this`​.rightChildIndex(`index`)] > |
| ​  | ​`this`​.data[​`this`​.leftChildIndex(`index`)] { |
| ​  | ​`return`​ ​`this`​.rightChildIndex(`index`); |
| ​  | } ​`else`​ { |
| ​  | ​`return`​ ​`this`​.leftChildIndex(`index`); |
| ​  | } |
| ​  | } |

让我们首先深入了解 `pop` 方法。

`pop` 方法不接受任何参数，因为我们删除的唯一节点是根节点。以下是该方法的工作方式。

首先，我们处理堆中仅包含一个元素的情况：

| ​  | ​`if`​ (​`this`​.data.length === `1`) { |
| --- | --- |
| ​  | ​`const`​ `valueToDelete` = ​`this`​.rootNode(); |
| ​  | ​`this`​.data = []; |
| ​  | ​`return`​ `valueToDelete`; |
| ​  | } |

由于这里只有一个根节点，这成为了我们要删除的值，我们将其存储在一个恰当地命名为 `valueToDelete` 的变量中。我们通过将 `this.data` 清空，使其指向一个空数组，并返回 `valueToDelete`。

`pop` 方法的其余部分处理堆中包含多个元素的情况。

首先，我们保存要删除的值，以便在方法结束时返回：

| ​  | ​`const`​ `valueToDelete` = ​`this`​.rootNode(); |
| --- | --- |

接下来，我们从数组中移除最后一个值，并将其设为第一个值：

| ​  | ​`this`​.data[`0`] = ​`this`​.data.pop(); |
| --- | --- |

这一简单的行有效地删除了原始根节点，因为我们用最后一个节点的值覆盖了根节点的值。

接下来，我们需要将新的根节点逐渐下移到它的适当位置。我们之前称之为“下移节点”，我们的代码反映了这一点。

在我们开始实际的下移之前，我们记录下下移节点的索引，因为我们稍后会需要它。目前，下移节点位于索引 `0`：

| ​  | ​`let`​ `trickleNodeIndex` = `0`; |
| --- | --- |

然后，我们使用一个 while 循环来执行下移算法。只要下移节点有任何子节点大于它，循环就会继续运行：

| ​  | ​`while`​ (​`this`​.hasGreaterChild(`trickleNodeIndex`)) { |
| --- | --- |

这一行使用了 `hasGreaterChild` 方法，该方法返回给定节点是否有任何子节点大于该节点。

在这个循环中，我们首先找到下移节点的子节点中较大的那个的索引：

| ​  | ​`const`​ `largerChildIndex` = ​`this`​.findLargerChildIndex(`trickleNodeIndex`); |
| --- | --- |

这一行使用了方法 `findLargerChildIndex`，该方法返回滴水节点的较大子节点的索引。我们将这个索引存储在一个名为 `largerChildIndex` 的变量中。

接下来，我们将滴水节点与其较大子节点交换：

|  | [`this`.data[trickleNodeIndex], `this`.data[largerChildIndex]] = |
| --- | --- |
|  | [`this`.data[largerChildIndex], `this`.data[trickleNodeIndex]]; |

我们更新滴水节点的索引，它将是刚刚交换过的索引：

|  | `trickleNodeIndex` = `largerChildIndex`; |
| --- | --- |

最后，我们返回从堆中删除的节点的值：

|  | `return` valueToDelete; |
| --- | --- |

### 备用堆实现

我们的堆实现现在已经完成。值得注意的是，尽管我们在内部使用了数组来实现堆，但也可以使用链节点来实现堆。（这种替代实现使用了不同的技巧来解决最后一个节点的问题，涉及到二进制数。）

然而，数组实现是更常见的方法，因此我在这里展示了这一点。看到如何使用数组来实现树也是很有趣的。

确实，可以使用数组来实现任何类型的二叉树，例如上一章中的二叉搜索树。然而，堆是第一个使用数组实现能提供优势的二叉树，因为它帮助我们轻松找到最后一个节点。
