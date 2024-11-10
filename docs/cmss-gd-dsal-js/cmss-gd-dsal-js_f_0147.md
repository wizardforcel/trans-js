## 插入

正如我之前提到的，二叉搜索树在插入时表现最佳。现在我们将看到原因。

假设我们想将数字45插入我们的示例树。我们首先需要找到合适的节点来附加45。为了开始搜索，我们从根节点开始，如下图所示：

![images/binary_trees/bst_6.png](images/binary_trees/bst_6.png)

由于45小于50，我们向左子节点深入：

![images/binary_trees/bst_10.png](images/binary_trees/bst_10.png)

由于45大于25，我们必须检查右子节点：

![images/binary_trees/bst_11.png](images/binary_trees/bst_11.png)

由于45大于33，我们检查33的右子节点：

![images/binary_trees/bst_12.png](images/binary_trees/bst_12.png)

此时，我们到达了一个没有子节点的节点，因此无处可去。这意味着我们准备执行插入操作。

由于45大于40，我们将其作为40的右子节点插入：

![images/binary_trees/bst_13.png](images/binary_trees/bst_13.png)

在这个例子中，插入共进行了五步，包括四步搜索和一步插入。插入总是比搜索多一步，这意味着插入需要(`log N`) + 1步。在忽略常数的情况下，用大O记法表示就是`O(log N)`。

相比之下，在有序数组中，插入需要`O(N)`，因为除了搜索外，我们还必须将大量数据向右移动以为要插入的值腾出空间。

这就是为什么二叉搜索树如此高效的原因。虽然有序数组的搜索时间复杂度为`O(log N)`，插入时间复杂度为`O(N)`，但二叉搜索树的搜索和插入时间复杂度都是`O(log N)`。在需要频繁更改数据的应用中，这一点尤其关键。

### 代码实现：二叉搜索树插入

这里是一个将新值插入二叉搜索树的JavaScript实现。与搜索功能一样，它是递归的：

| ​  | `import` TreeNode `from` *'./tree_node.js'*; |
| --- | --- |
| ​  |  |
| ​  | `function` insert(value, node) { |
| ​  | `if` (value < node.value) { |
| ​  | `if` (!node.leftChild) { |
| ​  | `node.leftChild = new TreeNode(value);` |
| ​  | } `else` { |
| ​  | insert(value, node.leftChild); |
| ​  | } |
| ​  | } `else` `if` (value > node.value) { |
| ​  | `if` (!node.rightChild) { |
| ​  | `node.rightChild = new TreeNode(value);` |
| ​  | } `else` { |
| ​  | insert(value, node.rightChild); |
| ​  | } |
| ​  | } |
| ​  | } |

插入函数接受我们要插入的值和作为祖先节点的节点，该节点的后代将是我们的值。

首先，我们检查该值是否小于当前节点的值：

| ​  | `if` (value < node.value) { |
| --- | --- |

如果值小于节点值，我们知道需要在节点的左侧后代中插入该值。

然后我们检查当前节点是否有左子节点。如果节点没有左子节点，我们就将值作为左子节点，因为这正是值应该所在的位置：

| ​  | `if` (!`node.leftChild`) { |
| --- | --- |
| ​  | `node.leftChild = new TreeNode(value);` |
| ​  | } |

这是基本情况，因为我们不需要进行任何递归调用。

然而，如果节点已经有左子节点，我们不能将值放在那里。相反，我们对左子节点递归调用`insert`，继续搜索可以放置值的位置：

| ​  | `else` { |
| --- | --- |
| ​  | `insert(value, node.leftChild);` |
| ​  | } |

最终，我们会遇到一个没有子节点的后代节点，值将放在那里。

剩余的函数是完全相反的；它处理值大于当前节点的情况。

### 插入的顺序

重要的是要注意，只有在创建随机排序数据的树时，树通常才会最终变得平衡。然而，如果我们将有序数据插入树中，树可能会变得不平衡且效率降低。例如，如果我们按照以下顺序插入数据——1, 2, 3, 4, 5——我们会得到如下的树：

![`images/binary_trees/bst_14.png`](images/binary_trees/bst_14.png)

这棵树是完全线性的，因此在这棵树中搜索5将花费`O(N)`。

然而，如果我们按以下顺序插入相同的数据——3, 2, 4, 1, 5——树将会均衡：

![`images/binary_trees/bst_15.png`](images/binary_trees/bst_15.png)

只有平衡的树才能使搜索时间为`O(log N)`。

因此，如果你想将有序数组转换为二叉搜索树，首先要随机化数据的顺序。

结果表明，在最坏的情况下，当树完全不平衡时，搜索是`O(N)`。在最佳情况下，当树完全平衡时，搜索是`O(log N)`。在典型情况下，当数据以随机顺序插入时，树会比较平衡，搜索大约需要`O(log N)`。
