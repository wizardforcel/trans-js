| 配方 23 | 创建你的第一个正则表达式 |
| --- | --- |

在使用第 2 部分和第 3 部分中的配方之前，你需要了解如何在代码中实现正则表达式。在 JavaScript 中，你有两种创建正则表达式的方式：可以使用 RegExp() 构造函数，也可以使用正则字面量。使用字面量形式时，你需要将模式包含在一对斜杠（/）字符中，如下所示：

[part_2/first_regex/first_regex_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/first_regex/first_regex_ex1.js)

|   | **const** re = */Hello/*; |
| --- | --- |

这个正则表达式模式由五个字符组成，指示正则引擎在字符串中找到“Hello”的直接匹配。模式可以像单个字面字符“i”一样简单。如果字符串中有多个“i”出现，它将匹配第一个。

例如，在字符串“If opportunity doesn’t knock, build a door”中，正则表达式匹配的是“opportunity”中的“i”，而不是“build”中的“i”。它也不会匹配“If”中的“I”，因为该单词使用了大写字母。正如你将在本部分后面学到的，你可以使用标志来配置正则表达式，在找到第一个匹配后继续搜索，或忽略字母大小写。

让我们来看另一个例子：

[part_2/first_regex/first_regex_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/first_regex/first_regex_ex2.js)

|   | **const** re = */123/*; |
| --- | --- |
|   |  |
|   | **const** str1 = *"123"*; |
|   | **const** str2 = *"321"*; |
|   |  |
|   | console.log(re.test(str1)); *// → true* |
|   | console.log(re.test(str2)); *// → false* |

当运行这段代码时，正则引擎会尝试找到“1”，然后是紧接着的“2”，接着是“3”。这个模式在第一个字符串中存在，因此 test() 返回 true，但尽管第二个字符串包含相同的字符，它们并没有算作匹配，因为它们的顺序不正确。

JavaScript提供了几种方法来判断一个模式是否存在于字符串中。test()方法是最简单的一种。如果给定的字符串中有匹配项，它返回true，否则返回false。

我们可以使用RegExp()构造函数获得相同的结果：

[part_2/first_regex/first_regex_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/first_regex/first_regex_ex3.js)

|   | **const** re = **new** RegExp(*"123"*); |
| --- | --- |
|   |  |
|   | **const** str1 = *"123"*; |
|   | **const** str2 = *"321"*; |
|   |  |
|   | console.log(re.test(str1)); *// → true* |
|   | console.log(re.test(str2)); *// → false* |

与字面量形式不同，RegExp()构造函数允许我们动态构建模式。例如，我们可以用它来从数组的项中构建一个模式：

[part_2/first_regex/first_regex_ex4.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/first_regex/first_regex_ex4.js)

|   | **const** str = *"调试器并不能去除错误，它们只是以慢动作展示错误。"*; |
| --- | --- |
|   | **const** arr = [*"bug"*, *"flea"*, *"mite"*, *"midge"*]; |
|   | **const** re = **new** RegExp(arr.join(*"&#124;"*)); |
|   |  |
|   | console.log(re.test(str)); *// → true* |

在正则表达式模式中，管道符号（|）的作用类似于JavaScript中的逻辑“或”(||)操作符。它匹配符号左侧的所有内容或符号右侧的所有内容。在这种情况下，我们在数组中有四个项，并且我们用管道符号连接它们，所以它就像写字面量形式的/bug|flea|mite|midge/。主要的区别是，RegExp()允许我们动态构建这个模式。

| 何时使用构造函数 |
| --- |
| ![images/aside-icons/tip.png](images/aside-icons/tip.png) | 请记住，字面量形式总是比构造函数形式更快。因此，只有在需要动态构建模式时，才使用构造函数。 |

使用这两种形式之间的另一个区别是，当使用RegExp构造函数时，需要对反斜杠和引号使用转义字符。对比一下：

[part_2/first_regex/first_regex_ex5.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/first_regex/first_regex_ex5.js)

|   | *// 一个 RegExp 模式* |
| --- | --- |
|   | **const** re1 = **new** RegExp(*"**\"***\\***d"*); |
|   |  |
|   | *// 上述模式的字面版本* |
|   | **const** re2 = */"**\d**/*; |
|   |  |
|   | console.log(re1.test(*'"3'*)); *// → true* |
|   | console.log(re2.test(*'"3'*)); *// → true* |

要匹配正则表达式模式中已经被引号括起来的引号字符，我们需要使用转义字符，表示引号字符是字符串的一部分，而不是字符串的分隔符。另一种写相同模式的方式是使用单引号作为模式字符串：new RegExp(’"\\d’)。

\d 是正则表达式中的一个元字符，用于匹配数字。如果我们不对 \d 进行转义，RegExp() 将会字面匹配一个反斜杠后跟着字母“d”：

[part_2/first_regex/first_regex_ex6.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/first_regex/first_regex_ex6.js)

|   | **const** re1 = **new** RegExp(*"***\***d"*); |
| --- | --- |
|   |  |
|   | console.log(re1.test(*"***\***d"*)); *// → true* |
|   | console.log(re1.test(*"3"*)); *// → false* |

在字面量表示法中，当模式被斜杠括起来时，我们必须使用反斜杠来转义模式中出现的任何斜杠。这是必要的，因为正则表达式字面量中的斜杠标志着模式的结束，如果不进行转义，它会被解释为结束符。对比：

[part_2/first_regex/first_regex_ex7.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/first_regex/first_regex_ex7.js)

|   | *// 一个 RegExp 模式* |
| --- | --- |
|   | **const** re1 = **new** RegExp(*"/"*); |
|   |  |
|   | *// 上述模式的字面版本* |
|   | **const** re2 = */**\/**/*; |
|   |  |
|   | console.log(re1.test(*"/"*)); *// → true* |
|   | console.log(re2.test(*"/"*)); *// → true* |
| 区分大小写 |
| --- |
| ![images/aside-icons/warning.png](images/aside-icons/warning.png) | 默认情况下，正则表达式是区分大小写的。模式 `/abc/` 不匹配 `Abc`，除非你使用一个名为 `ignoreCase` 的特殊标志来指示引擎忽略字母大小写的差异。你将在本部分稍后了解标志。 |

但找到直接匹配并不是正则表达式的最大优势。JavaScript 已经有了 `indexOf()` 方法，可以很好地完成这个任务。正则表达式旨在查找更复杂的模式，例如 `/\b(\w+)\s+\1\b/gi`，它用于查找重复的单词。

现在你已经了解如何在 JavaScript 中实现正则表达式，准备好在第二部分和第三部分中进行实际操作了。
