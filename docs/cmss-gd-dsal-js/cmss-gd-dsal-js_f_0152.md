## 练习

以下练习为你提供了练习二叉搜索树的机会。这些练习的解决方案在[`第15章`](f_0220.xhtml#binary.trees.solutions)中找到。

1.  想象一下，你将一个空的二叉搜索树按以下顺序插入数字：[1, 5, 9, 2, 4, 10, 6, 3, 8]。

    绘制一个图示，显示二叉搜索树的样子。记住，数字是按照此处呈现的顺序插入的。

1.  如果一个平衡良好的二叉搜索树包含1,000个值，搜索其中一个值最多需要多少步？

1.  编写一个算法，以在二叉搜索树中找到最大值。

1.  在文本中，我演示了如何使用中序遍历打印所有书名的列表。遍历树的另一种方式称为前序遍历。以下是应用于我们的书籍应用程序的相关代码：

    | ​  | `function` `traverseAndPrint(node) {` |
    | --- | --- |
    | ​  | `if` (!node) { `return`; } |
    | ​  |  |
    | ​  | `console.log(node.value);` |
    | ​  | `traverseAndPrint(node.leftChild);` |
    | ​  | `traverseAndPrint(node.rightChild);` |
    | ​  | } |

    在文本中的示例树（包含“白鲸”和其他书名）上，写出使用前序遍历打印书名的顺序。作为提醒，这里是示例树：

    ![images/binary_trees/bst_26.png](images/binary_trees/bst_26.png)

1.  另一种遍历形式称为后序遍历。以下是应用于我们的书籍应用程序的相关代码：

    | ​  | `function` `traverseAndPrint(node) {` |
    | --- | --- |
    | ​  | `if` (!node) { `return`; } |
    | ​  |  |
    | ​  | `traverseAndPrint(node.leftChild);` |
    | ​  | `traverseAndPrint(node.rightChild);` |
    | ​  | `console.log(node.value);` |
    | ​  | } |

    在文本中的示例树（也出现在之前的练习中），写出使用后序遍历打印书名的顺序。

版权所有 © 2024, The Pragmatic Bookshelf.
