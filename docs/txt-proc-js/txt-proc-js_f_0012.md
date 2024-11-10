| 配方 2 | 使用 includes() 检查字符串中特定的单词 |
| --- | --- |

### 任务

假设你正在构建一个在线烘焙店，并希望过滤消息，以便它们可以路由到正确的面包师。你需要检查传入电子邮件中的字符串，以考虑像“doughnut”和“donut”这样的单词的不同拼写。你不能单独使用 includes() 方法，因为它只能查找单个单词。

### 解决方案

将你想搜索的单词放入一个数组中。然后创建一个接受两个参数的函数：一个要搜索的字符串和一个单词数组。在函数内部，逐个检查字符串中的单词，如果至少有一个搜索成功，则返回 true：

[part_1/checking_specific_words/includes_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/checking_specific_words/includes_ex1.js)

|   | **const** msg = *"我想点两个donuts"*; |
| --- | --- |
|   | **const** words = [*"doughnut"*, *"donut"*]; |
|   |  |
|   | **function** hasSomeWords(str, arr) { |
|   | **return** arr.some(el => str.includes(el)); |
|   | } |
|   |  |
|   | hasSomeWords(msg, words); *// → true* |

some() 方法如果数组中的至少一个元素通过了给定函数的测试，则返回 true。在这种情况下，这意味着 includes() 首先搜索“doughnut”。由于字符串中没有这个单词，方法返回 false。第二次 includes() 搜索“donut”，这次返回 true。所以，some() 的返回值将是 true。

### 讨论

ECMAScript 在 ES2015 中添加了 includes() 方法，以便开发者轻松判断一个字符串是否包含另一个字符串。includes() 的第二个参数是可选的，它允许你指定从哪个位置开始搜索。例如：

[part_1/checking_specific_words/includes_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/checking_specific_words/includes_ex2.js)

|   | **const** quote = *"Sachertorte 是一种奥地利起源的蛋糕。"*; |
| --- | --- |
|   |  |
|   | quote.includes(*"Sachertorte"*, 15); *// → false* |

这段代码从索引15开始搜索。由于从索引15开始没有任何词与“Sachertorte”匹配，因此返回值为false。

请记住，includes()是区分大小写的。如果你在包含“SacherTorte”的字符串中搜索“Sachertorte”，结果会是false：

[part_1/checking_specific_words/includes_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/checking_specific_words/includes_ex3.js)

|   | **const** quote = *"我想点一份萨赫蛋糕。"*; |
| --- | --- |
|   | **const** word = *"Sachertorte"*; |
|   |  |
|   | quote.includes(word); *// → false* |

一些甜点可能会有内部的大写字母，因为它们由两个词组成，比如Dobostorta/DobosTorta、Leibnizkeks/LeibnizKeks和SacherTorte/Sachertorte。因此，在大多数情况下，你需要通过将字符串和关键词都转换为小写来执行不区分大小写的搜索，如下所示：

[part_1/checking_specific_words/includes_ex4.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/checking_specific_words/includes_ex4.js)

|   | **const** quote = *"我想点一份萨赫蛋糕。"*.toLowerCase(); |
| --- | --- |
|   | **const** word = *"Sachertorte"*.toLowerCase(); |
|   |  |
|   | quote.includes(word); *// → true* |

如果你想检查一个字符串是否同时包含多个词呢？在这种情况下，你应该使用every()方法。every()与some()类似，它会对数组的每个元素执行一个函数。但是，它只有在数组中的每一项都通过测试时才返回true。以下是一个示例：

[part_1/checking_specific_words/includes_ex5.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/checking_specific_words/includes_ex5.js)

|   | **const** msg = *"1个萨赫蛋糕，3个椒盐卷饼和2个甜甜圈，谢谢。"*; |
| --- | --- |
|   | **const** wordsArr1 = [*"sachertorte"*, *"甜甜圈"*]; |
|   | **const** wordsArr2 = [*"sachertorte"*, *"酸面包"*]; |
|   |  |
|   | **function** hasEveryWord(str, arr) { |
|   | **return** arr.every(el => str.includes(el)); |
|   | } |
|   |  |
|   | hasEveryWord(msg, wordsArr1); *// → true* |
|   | hasEveryWord(msg, wordsArr2); *// → false* |

在这里，“sachertorte”和“donut”通过了测试，因为它们都出现在字符串中，但“sachertorte”和“sourdough”则不行。

虽然includes()是设计用来搜索单个单词的，但通过一点努力，你可以利用它来搜索多个单词。但在查找也具有复合形式的单词时要小心。

如果你在“I’d like to order two pancakes”中搜索“cake”，includes()会返回true。如果你不希望出现这种情况，你应该使用一个称为单词边界的正则表达式标记。参见配方25，[*仅使用单词边界(\b)查找完整单词*](f_0036.xhtml#rcp.word_boundary)。
