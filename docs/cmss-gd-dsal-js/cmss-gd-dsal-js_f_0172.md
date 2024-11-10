## 构建自动完成

我们就要准备构建一个真正的自动完成功能了。为了稍微简化一下，让我们首先构建一个稍微简单一些的函数，以帮助我们实现这个功能。

### 收集所有单词

我们接下来要在我们的 `Trie` 类中添加的方法是一个返回字典树中所有单词数组的方法。现在，列出整个字典的情况很少发生。然而，我们将允许这个方法接受字典树的任何节点作为参数，以便它可以列出从该节点开始的所有单词。

以下方法称为 `collectAllWords`，从特定节点开始收集字典树中所有单词的列表：

| ​  | `collectAllWords(words, node=` `null` `, word=` `''` `) { |
| --- | --- |
| ​  | `const` currentNode = `node` ` | | ` `this`.root; |
| ​  |  |
| ​  | `for` (`const` [key, childNode] `of` `Object.entries(currentNode.children)) { |
| ​  | `if` (key === `'*'`) { |
| ​  | words.push(word); |
| ​  | } `else` { |
| ​  | `this`.collectAllWords(words, childNode, word + key); |
| ​  | } |
| ​  | } |
| ​  |  |
| ​  | `return` words; |
| ​  | } |

该方法在很大程度上依赖于递归，因此让我们仔细分解一下。

该方法接受三个主要参数：`words`、`node` 和 `word`。

当我们首次调用此方法时，必须将 `words` 作为空数组传入。随着方法的进行，它将用字典树中的单词填充这个数组。最终，当我们用所有所需单词填满它后，方法会返回这个数组。

节点参数允许我们指定从字典树中的哪个节点开始收集单词。如果我们不传入此参数，我们的方法将从根节点开始，收集整个字典树中的每个单词。

`word` 参数默认为空字符串。随着我们在字典树中的移动，我们将字符添加到这个单词中。当我们到达 `"*"` 时，单词被视为完成，我们将其添加到 `words` 数组中。

现在让我们逐行分析代码。

我们首先要做的是设置 `currentNode`：

| ​  | `const` currentNode = `node` ` | | ` `this`.root; |
| --- | --- | --- | --- |

默认情况下，`currentNode` 将是根节点，除非我们将其他节点作为方法的第一个参数传入。假设现在 `currentNode` 确实是根节点。

接下来，我们开始一个循环，遍历 `currentNode` 的子节点哈希表中的所有键值对：

| ​  | `for` (`const` [key, childNode] `of` `Object.entries(currentNode.children)) { |
| --- | --- |

JavaScript 语法 `Object.entries` 允许我们遍历哈希表，并一次访问每个键及其关联值。

在循环的每次迭代中，键总是一个单字符字符串，值 `childNode` 是另一个 `TrieNode` 的实例。

让我们跳到 else 子句，因为这里是魔法发生的地方：

| ​  | `this`.collectAllWords(words, childNode, word + key); |
| --- | --- |

这一行递归调用了 `collectAllWords` 函数。

第一个参数是 `words` 数组。通过在每次递归调用中传递这个数组，我们能够填充完整的单词，有效地在遍历字典树时构建这个列表。

第二个参数是`childNode`。这使我们能够在子节点上递归调用`collectAllWords`方法，继续从子节点及其后收集所有单词。

第三个参数是`word + key`，这样当我们在trie的每个节点上移动时，我们将`key`添加到当前单词中，逐步构建单词。

基础情况是当我们到达`"*"`键时，表示我们已完成一个单词。此时，我们可以将单词添加到`words`数组中：

| ​  | `if` (key === `'*'`) { |
| --- | --- |
| ​  | `words.push(word);` |
| ​  | } |

在函数结束时，我们返回`words`数组。如果我们在没有传递特定节点的情况下调用此函数，它将返回trie中的完整单词列表。

### 递归过程演示

让我们通过一个简单的trie快速演示一下。这棵trie包含两个单词，`"can"`和`"cat"`：

![images/tries/simple_trie.png](images/tries/simple_trie.png)

调用1：在`collectAllWords`的第一次调用中，`currentNode`开始于根节点，`word`是一个空字符串，`words`数组是空的：

![images/tries/simple_trie_setup.png](images/tries/simple_trie_setup.png)

我们遍历根节点的子节点。根节点只有一个子键`"c"`，它指向一个子节点。在我们递归调用`collectAllWords`在这个子节点上之前，我们需要将当前调用添加到调用栈中。

然后我们在`"c"`子节点上递归调用`collectAllWords`。我们还将`word + key`作为单词参数传递。`word + key`是字符串`"c"`，因为`word`是空的，`key`是`"c"`。我们还将仍然为空的`words`数组传递进去。下一张图片显示了我们在进行这个递归调用时的位置：

![images/tries/simple_trie_c.png](images/tries/simple_trie_c.png)

调用2：我们遍历当前节点的子节点。它只有一个子键，`"a"`。在递归调用`collectAllWords`之前，我们将当前调用添加到调用栈中。在接下来的图示中，我们称这个当前节点为`"a"`节点，意思是它有`"a"`作为子节点。

然后我们递归调用`collectAllWords`。我们传入子节点`"ca"`（即`word + key`）和仍然为空的`words`数组：

![images/tries/simple_trie_ca.png](images/tries/simple_trie_ca.png)

调用3：我们遍历当前节点的子节点，分别是`"n"`和`"t"`。我们将首先处理`"n"`。不过，在进行任何递归调用之前，我们需要先将当前调用添加到我们的调用栈中。在接下来的图示中，我们称这个当前节点为`"n/t"`节点，意思是它的子节点有`"n"`和`"t"`。

当我们在`"n"`子节点上调用`collectAllWords`时，我们还将`"can"`作为单词参数传递，以及空的`words`数组：

![images/tries/move_to_n.png](images/tries/move_to_n.png)

`Call 4`：我们遍历当前节点的子节点。在这种情况下，它只有一个子节点，即`"*"`。这是我们的基本情况。我们将当前单词，即`"can"`，添加到`words`数组中：

![images/tries/can_in_array.png](images/tries/can_in_array.png)

`Call 5`：我们现在从调用栈中弹出顶部调用，即对节点进行的`collectAllWords`调用，该节点的子键为`"n"`和`"t"`，而`word`是`"ca"`。这意味着我们现在返回到该调用（因为我们返回到我们从调用栈中弹出的任何调用）：

![images/tries/pop_n_t.png](images/tries/pop_n_t.png)

在这里我们可以提出一个微妙但重要的观点。在当前调用中，`word`又回到了`"ca"`，因为那是我们第一次启动这个调用时的单词参数。然而，`words`数组现在包含单词`"can"`，即使在我们最初进行此调用时数组是空的。

这就是为什么这有效的原因。在许多编程语言中，数组可以在调用栈中上下传递，因为即使我们向其中添加新值，数组在内存中仍然是相同的对象。这一概念同样适用于哈希表，这也是我们能够将其作为我们在[​*动态编程通过记忆化*​](f_0117.xhtml#dynamic.memoization)中探讨的记忆化技术的一部分传递的原因。

另一方面，当字符串被修改时，计算机会创建一个新字符串，而不是实际上修改原始字符串对象。因此，当我们通过将`word`从`"ca"`更改为`"can"`来更新`word`时，先前的调用仍然只能访问原始字符串`"ca"`。（在某些语言中，这可能略有不同。不过对于我们的目的来说，这就是一般思路。）

在任何情况下，我们正在进行一次调用，其中`words`包含单词`"can"`，而`word`是`"ca"`。

`Call 6`：此时，我们已经遍历过`"n"`键，因此循环现在到了`"t"`键。在递归调用`collectAllWords`到`"t"`子节点之前，我们需要再次将当前调用添加到调用栈中。（这将是我们第二次将此调用添加到调用栈中。我们之前已经将其弹出，但现在我们要再次添加它。）

当我们在`"t"`子节点上调用`collectAllWords`时，我们将`"cat"`作为单词参数传入（因为这就是`word + key`）和`words`数组：

![images/tries/move_to_t.png](images/tries/move_to_t.png)

`Call 7`：我们遍历当前节点的子节点。这里唯一的子节点是`"*"`，因此我们将当前单词`"cat"`添加到我们的`words`数组中：

![images/tries/add_cat_to_array.png](images/tries/add_cat_to_array.png)

此时，我们可以展开调用栈，逐个弹出每个调用并完成其执行，每个调用都以返回`words`数组结束。我们完成的最后一个调用——即第一次启动这一切的调用——也返回`words`。因为它包含字符串`"can"`和`"cat"`，我们成功返回了字典树的整个单词列表。
