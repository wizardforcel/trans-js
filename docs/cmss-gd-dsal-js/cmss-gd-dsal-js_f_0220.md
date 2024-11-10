## 第15章

这些是位于章节[`练习`](f_0152.xhtml#binary.trees.exercises)中的练习解决方案。

1.  这个树应该看起来像这样。注意它不是很好地平衡，因为根节点只有一个右子树而没有左子树：

    ![images/binary_trees/solution_1.png](images/binary_trees/solution_1.png)

1.  在平衡的二叉搜索树中，搜索最多需要大约`log(N)`步。因此，如果`N`为1,000，搜索最多应该需要大约10步。

1.  在二叉搜索树中，最大的值总是最右下角的节点。我们可以通过递归地跟踪每个节点的右子节点，直到到达底部：

    | ​  | ​`function`​ `max(node)` { |
    | --- | --- |
    | ​  | ​`if`​ (`node.rightChild`) { |
    | ​  | ​`return`​ `max(node.rightChild)`; |
    | ​  | } ​`else`​ { |
    | ​  | ​`return`​ `node.value`; |
    | ​  | } |
    | ​  | } |

1.  这是前序遍历的顺序：

    ![images/binary_trees/solution_4.png](images/binary_trees/solution_4.png)

1.  这是后序遍历的顺序：

    ![images/binary_trees/solution_5.png](images/binary_trees/solution_5.png)
