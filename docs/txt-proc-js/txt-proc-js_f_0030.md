| Recipe 20 | 使用 split() 计数特定单词的数量 |
| --- | --- |

### 任务

假设你想为应用程序添加搜索功能，提供一个单词在文本中出现多少次的信息。你可以使用 `includes()` 方法来判断单词是否存在于字符串中。但它并不会告诉你单词出现的频率。

你想创建一个函数，统计指定单词（在本例中是 "cougar"）的出现次数，并返回它找到的总数。

### 解决方案

使用 `split()` 方法将字符串分割为子字符串数组，通过读取数组的长度属性来计算数组中的项数，并返回结果：

[part_1/counting_a_specific_word/split_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/counting_a_specific_word/split_ex1.js)

|   | **const** str = *`Cougar 是一种适应性强的通用物种，分布于大多数* |
| --- | --- |
|   | *美国栖息地类型。猫科动物本性上较为神秘且通常孤独， cougar* |
|   | *是典型的夜行性和黎明性动物。主要的食物来源* |
|   | *它们是偶蹄目动物，尤其是鹿，但 cougar 也会捕猎较小的猎物，如* |
|   | *啮齿动物。`*; |
|   |  |
|   | **function** countWord(str, word, caseSensitivity) { |
|   | **如果** (caseSensitivity) { |
|   | **return** str.split(word).length - 1; |
|   | } **else** { |
|   | **return** str.toLowerCase().split(word).length - 1; |
|   | } |
|   | } |
|   |  |
|   | console.log(countWord(str, *"cougar"*, **true**)); *// → 2* |
|   | console.log(countWord(str, *"cougar"*, **false**)); *// → 3* |

countWord() 函数返回单词在 str 字符串中出现的总次数。

### 讨论

countWord() 函数接受三个参数：

+   str: 包含要搜索单词的文本的字符串

+   word: 表示要在文本中计数的单词的字符串

+   caseSensitivity: 一个布尔值，指示搜索是否应区分大小写

在函数内部，我们检查 caseSensitivity 的值。如果它是 false，我们首先使用 toLowerCase() 方法将字符串转换为小写字母。然后，我们在每次出现单词时用 split() 方法分割 str 输入字符串，并返回由此产生的子字符串数量，这个数量等于 word 在 str 中出现的次数。

请注意语句末尾的减法。如果我们传递一个包含一个实例“cougar”的字符串给 split()，它会返回一个包含两个项目的数组。这个减法是必要的，用来偏移一个项目，以便得到正确的计数：

[part_1/counting_a_specific_word/split_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/counting_a_specific_word/split_ex2.js)

|   | **const** str = *"单词 cougar 源自葡萄牙语 çuçuarana。"*; |
| --- | --- |
|   | **const** word = *"cougar"*; |
|   |  |
|   | str.split(word); |
|   | *// → ["单词 ", " 源自葡萄牙语 çuçuarana。"]* |

split() 是一个多功能的 JavaScript 工具，在许多不同的场景中都能派上用场。在这个示例中，我们将 split() 集成到一个函数中，用来计算特定单词出现的次数。但是正如你在示例 3 [*使用 startsWith() 和 endsWith() 匹配字符串的开始或结尾*](f_0013.xhtml#rcp.start_end) 和示例 4 [*使用 slice() 从文本中提取列表*](f_0014.xhtml#rcp.slice) 中看到的，你也可以利用 split() 来解决其他文本处理问题。
