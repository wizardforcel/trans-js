## 练习

以下练习为你提供了练习递归的机会。这些练习的解决方案可以在章节[​*第11章*​](f_0216.xhtml#learning.to.write.in.recursive.solutions)中找到。

1.  使用递归编写一个`function`，接受一个字符串数组，并返回所有字符串中字符的总数。例如，如果输入数组是["ab", "c", "def", "ghij"]，那么输出应该是10，因为总共有十个字符。

1.  使用递归编写一个`function`，接受一个数字数组并返回一个仅包含偶数的新数组。

1.  特定的数列被称为三角形数。这个模式开始于1、3、6、10、15、21，并继续下去。要计算序列中的下一个数字，我们将序列中的前一个数字加上`N`，其中`N`对应于该数字在序列中的位置。例如，序列中的第七个数字是28，因为它是模式中的第七个数字，所以我们将数字7加上21（序列中的前一个数字）。编写一个`function`，接受一个数字`N`并返回该序列中的正确数字；也就是说，如果`function`传入数字7，`function`将返回28。

1.  使用递归编写一个`function`，接受一个字符串并返回包含字符“`x`”的第一个索引。例如，字符串"abcdefghijklmnopqrstuvwxyz"在索引23处有一个“`x`”。为了简化问题，假设字符串至少有一个“`x`”。

1.  这个问题被称为唯一路径问题。假设你有一个行和列的网格。编写一个`function`，接受行数和列数，并计算从左上角到右下角的所有可能的“最短”路径的数量。

    例如，这里是一个包含三行和七列的网格。你要从`S`（起点）到`F`（终点）。

    ![images/learning_to_write_in_recursive/unique_paths_setup.png](images/learning_to_write_in_recursive/unique_paths_setup.png)

    所谓“最短”路径，我是指在每一步，你要么向右移动一步：

    ![images/learning_to_write_in_recursive/unique_paths_move_right.png](images/learning_to_write_in_recursive/unique_paths_move_right.png)

    或者你向下移动一步：

    ![images/learning_to_write_in_recursive/unique_paths_move_down.png](images/learning_to_write_in_recursive/unique_paths_move_down.png)

    再次，你的`function`应该计算最短路径的数量。

版权所有 © 2024, The Pragmatic Bookshelf。
