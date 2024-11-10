## 二分搜索

你可能在小时候玩过这个猜数字的游戏：我心里想的是一个`1`到`100`之间的数字。继续猜我心里想的哪个数字，我会告诉你是否需要猜更高或更低。

你可能直觉上知道如何玩这个游戏。你不会从猜数字`1`开始。相反，你可能会先猜`50`，它正好在中间。为什么？因为选择`50`后，无论我告诉你要猜更高还是更低，你都会自动排除掉一半的可能数字！

如果你猜了`50`，而我告诉你猜更高，你就会选择`75`，以排除剩余数字的一半。如果在猜了`75`后，我告诉你猜更低，你就会选择`62`或`63`。你会继续选择中间值，以不断排除剩余的一半数字。

让我们可视化这个过程，我们被告知要猜一个`1`到`10`之间的数字，如下图所示：[image](#fig.ch2.conversation)。

![`images/binary_search/conversation.png`](images/binary_search/conversation.png)

简而言之，这就是二分搜索。

让我们看看二分搜索是如何应用于一个有序数组的。假设我们有一个包含九个元素的有序数组。计算机并不知道每个单元格具体包含什么值，因此我们将数组描绘成这样：

![`images/binary_search/binary_search_11.png`](images/binary_search/binary_search_11.png)

假设我们想在这个有序数组中搜索值`7`。二分搜索将如何进行：

步骤 1：我们从中间单元格开始搜索。我们可以立即跳到这个单元格，因为我们可以通过将数组的长度除以`2`来计算它的索引。我们检查这个单元格的值：

![`images/binary_search/binary_search_12.png`](images/binary_search/binary_search_12.png)

因为未揭示的值是`9`，我们可以得出`7`在它的左边。我们刚刚成功排除了数组单元格的一半——也就是所有在`9`右侧的单元格（包括`9`本身）：

![`images/binary_search/binary_search_13.png`](images/binary_search/binary_search_13.png)

步骤 2：在`9`左侧的单元格中，我们检查中间值。有两个中间值，因此我们任意选择左边的那个：

![`images/binary_search/binary_search_14.png`](images/binary_search/binary_search_14.png)

它是`4`，因此`7`必须在它的右边。我们可以排除`4`和它左边的单元格：

![`images/binary_search/binary_search_15.png`](images/binary_search/binary_search_15.png)

步骤 3：还有两个单元格可能包含`7`。我们任意选择左边的一个，如下图所示：[image](#fig.ch2.binary_search_16)。

![`images/binary_search/binary_search_16.png`](images/binary_search/binary_search_16.png)

步骤 4：我们检查最后剩下的单元格。（如果没有，那就意味着在这个有序数组中没有`7`。）

![`images/binary_search/binary_search_17.png`](images/binary_search/binary_search_17.png)

我们在四步内找到了7。在这个例子中，这与线性搜索所需的步骤数相同，但我们很快将看到另一个例子，以展示二分搜索的强大。

请注意，二分搜索仅在有序数组中有效。对于经典数组，值可以是任意顺序，我们无法知道是否应该向任何给定值的左侧或右侧查找。这是有序数组的一个优势：我们有使用二分搜索的选项。

### 代码实现：二分搜索

下面是一个用JavaScript实现的二分搜索：

| ​  | `function` binarySearch(array, searchValue) { |
| --- | --- |
| ​  | `let` lowerBound = 0; |
| ​  | `let` upperBound = array.length - 1; |
| ​  |  |
| ​  | `while` (lowerBound <= upperBound) { |
| ​  | `const` midpoint = Math.floor((upperBound + lowerBound) / 2); |
| ​  | `const` valueAtMidpoint = array[midpoint]; |
| ​  |  |
| ​  | `if` (searchValue === valueAtMidpoint) { |
| ​  | `return` midpoint; |
| ​  | } `else` `if` (searchValue < valueAtMidpoint) { |
| ​  | upperBound = midpoint - 1; |
| ​  | } `else` `if` (searchValue > valueAtMidpoint) { |
| ​  | lowerBound = midpoint + 1; |
| ​  | } |
| ​  | } |
| ​  |  |
| ​  | `return` `null`; |
| ​  | } |

让我们分析一下。与`linearSearch`方法类似，`binarySearch`接受数组和`searchValue`作为参数。

下面是如何调用这个方法的一个示例：

| ​  | `console.log(binarySearch([3, 17, 75, 80, 202], 22))` |
| --- | --- |

该方法首先确定`searchValue`可能存在的索引范围。我们用以下代码实现这一点：

| ​  | `let` lowerBound = 0; |
| --- | --- |
| ​  | `let` upperBound = array.length - 1; |

因为在开始搜索时，`searchValue`可能在整个数组的任何位置，我们将`lowerBound`设为第一个索引，`upperBound`设为最后一个索引。

搜索的本质在于`while`循环中进行：

| ​  | `while` (lowerBound <= upperBound) { |
| --- | --- |

当我们仍然有一系列元素可能包含`searchValue`时，这个循环会持续运行。正如我们将很快看到的，我们的算法会随着不断迭代而逐步缩小这个范围。一旦没有更多范围可供搜索，`lowerBound <= upperBound`这个条件将不再成立，我们可以得出结论，`searchValue`不在数组中。

在循环中，我们的代码检查范围中点的值。以下代码实现了这一点：

| ​  | `const` midpoint = Math.floor((upperBound + lowerBound) / 2); |
| --- | --- |
| ​  | `const` valueAtMidpoint = array[midpoint]; |

`valueAtMidpoint`是找到的范围中心的项。

现在，如果`valueAtMidpoint`是我们正在寻找的`searchValue`，那么我们就找到了目标，可以返回`searchValue`所在的索引：

| ​  | `if` (searchValue === valueAtMidpoint) { |
| --- | --- |
| ​  | `return` midpoint; |

如果`searchValue`小于`valueAtMidpoint`，这意味着`searchValue`必须在数组的某个更早的位置被找到。然后，我们可以通过将`upperBound`设为`midpoint`左侧的索引来缩小搜索范围，因为`searchValue`不可能在更远的位置找到：

| ​  | } ​`else`​ ​`if`​ (`searchValue < valueAtMidpoint`) { |
| --- | --- |
| ​  | `upperBound = midpoint - 1;` |
| ​  | } |

相反，如果`searchValue`大于`valueAtMidpoint`，这意味着`searchValue`只能在`midpoint`的右侧找到，因此我们适当地提高`lowerBound`：

| ​  | } ​`else`​ ​`if`​ (`searchValue > valueAtMidpoint`) { |
| --- | --- |
| ​  | `lowerBound = midpoint + 1;` |
| ​  | } |

一旦范围缩小到0个元素，我们就返回`null`，并且我们可以确定`searchValue`在数组中不存在。
