## 第17章

这些是本节[**练习**](f_0176.xhtml#tries.exercises)中练习的解决方案。

1.  这个字典树存储了以下单词：“tag”、“tan”、“tank”、“tap”、“today”、“total”、“we”、“well”和“went”。

1.  这里是一个字典树，存储了单词“get”、“go”、“got”、“gotten”、“hall”、“ham”、“hammer”、“hill”和“zebra”：

    ![images/tries/solution_2.png](images/tries/solution_2.png)

1.  以下代码从字典树的节点开始，迭代每个子节点。对于每个子节点，它打印键，然后在子节点上递归调用自身：

    | ​  | `traverse(node =` `null`) { |
    | --- | --- |
    | ​  | `const` currentNode = node ` | | ` `this`.root; |
    | ​  |  |
    | ​  | `for` (`const` [key, childNode] `of` Object.entries(currentNode.children)) { |
    | ​  | `console.log(key);` |
    | ​  |  |
    | ​  | `if` (key !== `'*'`) { |
    | ​  | `this.traverse(childNode);` |
    | ​  | } |
    | ​  | } |
    | ​  | } |

1.  我们的自动纠正实现是搜索和`collectAllWords`函数的组合：

    | ​  | `autocorrect(word)` { |
    | --- | --- |
    | ​  | `let` currentNode = `this`.root; |
    | ​  | `let` wordFoundSoFar = `''`; |
    | ​  |  |
    | ​  | `for` (`const` `char` `of` word) { |
    | ​  | `if` (currentNode.children[`char`]) { |
    | ​  | `wordFoundSoFar +=` `char`; |
    | ​  | `currentNode = currentNode.children[`char`];` |
    | ​  | } `else` { |
    | ​  | `return` wordFoundSoFar + `this.collectAllWords([], currentNode)[0];` |
    | ​  | } |
    | ​  | } |
    | ​  |  |
    | ​  | `return` word; |
    | ​  | } |

    基本思路是，我们首先搜索字典树以找到尽可能多的前缀。当我们遇到死胡同时，而不是像搜索函数那样返回`null`，我们在当前节点调用`collectAllWords`来收集所有来自该节点的后缀。然后我们使用数组中的第一个后缀并将其与前缀连接，以向用户建议一个新单词。
