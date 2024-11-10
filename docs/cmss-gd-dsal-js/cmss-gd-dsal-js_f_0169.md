## Trie `Search`

最经典的 trie 操作是`search`——即确定字符串是否存在于 trie 中。`Search`有两种形式：我们可以搜索以查看字符串是否是完整的单词，或者我们可以搜索以查看字符串是否至少是一个单词前缀（即单词的开头）。这两个版本相似，但我们将实现后者，其中我们的`search`将查找前缀。这个`search`最终也会找到完整的单词，因为完整的单词至少和前缀一样好。

前缀`search`的算法执行以下步骤（当我们通过接下来的示例进行说明时，它们会变得更加清晰）：

1.  我们建立一个名为`currentNode`的变量。在算法开始时，这指向根节点。

1.  我们遍历搜索字符串的每个字符。

1.  当我们指向搜索字符串中的每个字符时，我们查看`currentNode`是否有一个以该字符为键的子节点。

1.  如果没有找到，我们返回 `null`，这意味着我们的搜索字符串在 trie 中不存在。

1.  如果`currentNode`确实有一个以当前字符为键的子节点，我们就将`currentNode`更新为该子节点。然后我们回到第2步，继续遍历搜索字符串中的每个字符。

1.  如果我们到达搜索字符串的末尾，这意味着我们找到了我们的搜索字符串。

让我们通过在之前的 trie 中搜索字符串 `"cat"` 来看看这个过程的实际应用。

设置：我们将`currentNode`设置为根节点。（`currentNode`在接下来的页面的图示中以粗体表示。）我们还指向字符串的第一个字符，即 `"c"`，如顶部 [图示](#fig.ch17.point_to_c)所示。

![images/tries/point_to_c.png](images/tries/point_to_c.png)

第1步：由于根节点有 `"c"` 作为子键，我们将`currentNode`更新为该键的值。我们还继续遍历搜索字符串中的字符，因此我们指向下一个字符，即 `"a"`，如底部 [图示](#fig.ch17.point_to_a)所示。

![images/tries/point_to_a.png](images/tries/point_to_a.png)

第2步：我们检查`currentNode`是否有一个键为 `"a"` 的子节点。它有一个，所以我们将该子节点设为新的`currentNode`。然后我们继续搜索字符串中的下一个字符，即 `"t"`：

![images/tries/point_to_t.png](images/tries/point_to_t.png)

第3步：我们现在指向搜索字符串中的 `"t"`。由于`currentNode`有一个 `"t"` 子节点，我们跟随它，如 [图示](#fig.ch17.follow_the_t)所示。由于我们已到达搜索字符串的末尾，这意味着我们在 trie 中找到了 `"cat"`。

![images/tries/follow_the_t.png](images/tries/follow_the_t.png)

### 代码实现：Trie `Search`

让我们通过在`Trie`类中添加一个`search`方法来实现 trie 的 `search`：

| ​  | `search(word)` { |
| --- | --- |
| ​  | ​`let`​ `currentNode` = `this`.root; |
| ​  |  |
| ​  | ​`for`​ (`const` `char` `of` `word`) { |
| ​  | ​`if`​ (`currentNode.children[`**char**`]) { |
| ​  | `currentNode` = `currentNode`.children[`char`]; |
| ​  | } `else` { |
| ​  | `return` `null`; |
| ​  | } |
| ​  | } |
| ​  |  |
| ​  | `return` currentNode; |
| ​  | } |

我们的搜索方法接受一个表示要搜索的单词（或前缀）的字符串。

首先，我们将根节点设为`currentNode`：

| ​  | `let` currentNode = `this`.root; |
| --- | --- |

然后我们遍历搜索单词的每个字符：

| ​  | `for` (`const` `char` `of` word) { |
| --- | --- |

在每一轮循环中，我们检查当前节点是否有任何子节点，其当前字符作为键。如果存在这样的子节点，我们更新当前节点为子节点：

| ​  | `if` (`currentNode`.children[`char`]) { |
| --- | --- |
| ​  | `currentNode` = `currentNode`.children[`char`]; |
| ​  | } |

如果没有这样的子节点，我们返回`null`，因为这意味着我们遇到了死胡同，搜索的单词不在`trie`中。

如果我们通过了循环的结束，这意味着我们在`trie`中找到了整个单词。在这种情况下，我们返回`currentNode`。我们返回当前节点的原因，而不是仅仅返回`true`，是为了帮助我们实现自动补全功能，稍后我会解释。
