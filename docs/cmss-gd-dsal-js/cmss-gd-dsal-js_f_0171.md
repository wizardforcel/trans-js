## Trie 插入

将新单词插入 trie 类似于搜索现有单词。我们首先检查该单词是否已存在于 trie 中。如果不存在，我们插入新单词。

算法的步骤如下：

1.  我们建立一个名为 `currentNode` 的变量。在算法开始时，这指向根节点。

1.  我们迭代搜索字符串的每个字符。在这里，我们的搜索字符串代表我们要插入的新单词。我们称之为搜索字符串，因为我们还要检查该字符串是否已存在于 trie 中。

1.  当我们指向搜索字符串的每个字符时，我们查看 `currentNode` 是否有以该字符为键的子节点。

1.  如果存在，我们将 `currentNode` 更新为该子节点，然后回到第 2 步，继续处理我们搜索字符串的下一个字符。

1.  如果 `currentNode` 没有匹配当前字符的子节点，我们就创建一个这样的子节点，并将 `currentNode` 更新为这个新节点。然后我们回到第 2 步，继续处理我们搜索字符串的下一个字符。

1.  在我们插入新单词的最后一个字符后，我们为最后一个节点添加一个 `"*"` 子节点，以表示单词已完成。

让我们通过将单词 `"can"` 插入到之前的示例 trie 中来看一下这个过程。

设置：我们将 `currentNode` 设置为根节点。我们还指向字符串的第一个字符，即 `"c"`，如顶部 [图示](#fig.ch17.insert_point_to_c) 所示。

![images/tries/insert_point_to_c.png](images/tries/insert_point_to_c.png)

第 1 步：根节点有一个 `"c"` 子键，因此我们将该键的值设为 `currentNode`。我们还指向新单词的下一个字符，即 `"a"`，如底部 [图示](#fig.ch17.insert_point_to_a) 所示。

![images/tries/insert_point_to_a.png](images/tries/insert_point_to_a.png)

第 2 步：我们检查 `currentNode` 是否有键为 `"a"` 的子节点。确实有一个，因此我们将其设为 `currentNode`，并指向我们字符串的下一个字符，即 `"n"`，如顶部 [图示](#fig.ch17.insert_point_to_n) 所示。

![images/tries/insert_point_to_n.png](images/tries/insert_point_to_n.png)

第 3 步：`currentNode` 没有 `"n"`，所以我们需要创建这个子节点，如底部 [图示](#fig.ch17.insert_n) 所示。

![images/tries/insert_n.png](images/tries/insert_n.png)

第 4 步：我们已经完成了将 `"can"` 插入到我们的 trie 中，因此我们用一个 `"*"` 的子节点结束它：

![images/tries/cap_off.png](images/tries/cap_off.png)

我们完成了！

### 代码实现：Trie 插入

这是我们 `Trie` 类的插入方法。你会注意到大部分内容与之前的搜索方法相似：

| ​  | `insert`(word) { |
| --- | --- |
| ​  | `let` `currentNode` = `this`.root; |
| ​  |  |
| ​  | `for` (`const` `char` `of` word) { |
| ​  | `if` (`currentNode.children[` `char` `]) { |
| ​  | `currentNode` = `currentNode.children[` `char` `]; |
| ​  | } `else` { |
| ​  | `const` newNode = `new` TrieNode(); |
| ​  | `currentNode.children['char'] = newNode;` |
| ​  | `currentNode = newNode;` |
| ​  | } |
| ​  | } |
| ​  |  |
| ​  | `currentNode.children['*'] = null;` |
| ​  | } |

该方法的第一部分与搜索相同。当`currentNode`没有匹配当前字符的子节点时，它分叉。在这种情况下，我们向`currentNode`的哈希表中添加一个新的键值对，键为当前字符，值为一个新的`TrieNode`：

| ​  | `const newNode = new TrieNode();` |
| --- | --- |
| ​  | `currentNode.children['char'] = newNode;` |

我们然后更新`currentNode`为这个新节点：

| ​  | `currentNode = newNode;` |
| --- | --- |

我们然后重复这个循环，直到插入新单词完成。一旦完成，我们向最终节点的哈希表中添加一个`"*"`键，值为`null`：

| ​  | `currentNode.children['*'] = null;` |
| --- | --- |

与搜索一样，字典树插入大约需要`O(K)`步。如果算上最后添加`"*"`，技术上是`K + 1`步，但因为我们省略常数，所以速度表示为`O(K)`。
