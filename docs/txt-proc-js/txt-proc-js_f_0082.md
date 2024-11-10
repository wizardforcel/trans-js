| 配方70 | 匹配邻近单词 |
| --- | --- |

### 任务

假设你想在教程数据库中搜索术语“client-side”，因为你被要求评估新员工是否已充分掌握客户端相关问题。如果你编写的正则表达式仅匹配确切的单词，它将无法检索那些包含“client”和“side”这两个词，但它们之间并不相邻的实例。例如，包含“client- 和 server-side”或“client 和 server side”等短语的教程将不会包含在搜索结果中。

但是，如果你指定一个邻近搜索，要求单词出现在彼此相距一定字符数以内，这将帮助你找到更相关的结果。所以，你需要创建一个模式来定位这些单词，只要它们出现在彼此特定距离以内。

### 解决方案

要查找彼此靠近的单词，可以使用以下函数：

[part_3/proximity_search/proximity_search_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_3/proximity_search/proximity_search_ex1.js)

|   | **function** findNearbyWords(text, word1, word2, maxDistance) { |
| --- | --- |
|   | **const** regex = **new** RegExp(*`*${word1}*.{0,*${maxDistance}*}*${word2}*`*, *"gi"*); |
|   | **const** matches = text.match(regex); |
|   | **return** matches; |
|   | } |
|   |  |
|   | **const** text = *"客户端和服务器端脚本必须验证表单数据。"*; |
|   | **const** word1 = *"client"*; |
|   | **const** word2 = *"side"*; |
|   | **const** maxDistance = 20; |
|   |  |
|   | findNearbyWords(text, word1, word2, maxDistance); |
|   | *// → ["client- 和 server-side"]* |

该函数执行一个邻近搜索，用于查找“client”和“side”这两个词，在彼此相距不超过20个字符的情况下，并检索包含它们的字符串部分。

### 讨论

我们通过使用模板字面量构造模式，该字面量包含 word1 和 word2 变量，以及作为量词 {0,${maxDistance}} 的 maxDistance 变量，用于匹配 word1 和 word2 之间的内容。请注意，${word1}、${maxDistance} 和 ${word2} 是用于执行替换的 JavaScript 占位符，它们与正则表达式语法完全不同。让我们更深入地了解一下：

|   | ${word1}.{0,${maxDistance}}${word2} |
| --- | --- |
|   |  |
|   | ● ${word1} 被替换为 "client" |
|   | ● . 匹配任何不是换行符的字符 |
|   | ○ {0,${maxDistance}} 被替换为 {0,20}，因此匹配之前的内容 |
|   | token 出现 0 到 20 次 |
|   | ● ${word2} 被替换为 "side" |

此外，我们向正则表达式添加了 g 和 i 标志，使其成为全局和大小写不敏感的。然后，我们在文本上调用 match() 方法，并将正则表达式对象作为参数。输出将是一个包含 word1 和 word2 在最大距离字符范围内的匹配项数组。

接近性搜索技术在搜索复杂或技术性信息时特别有用。通过指定我们希望看到某些单词或短语出现在彼此附近的结果，我们可以更准确地找到我们要找的文本。
