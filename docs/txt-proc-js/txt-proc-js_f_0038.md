| 配方 27 | 使用字符类匹配多个字符中的一个 |
| --- | --- |

### 任务

假设你想在文档中找到一个单词，即使它被拼错了。例如，“license”是英语中最常见的拼写错误之一。你想写一个模式来匹配文档中的“license”、“licence”、“lisence”或“lisense”。

### 解决方案

使用字符类：

[part_2/character_class/character_class_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/character_class/character_class_ex1.js)

|   | **const** re = */li**[**sc**]**en**[**sc**]**e/*; |
| --- | --- |
|   |  |
|   | re.test(*"A driver's license"*); *// → true* |
|   | re.test(*"A driver's lisense"*); *// → true* |
|   | re.test(*"A driver's licence"*); *// → true* |
|   | re.test(*"A shopping list"*); *// → false* |

字符类只匹配指定字符中的一个。在这段代码中，指定的字符是“s”和“c”，所以正则表达式会匹配“license”、“licence”、“lisense”或“lisence”，但不匹配“liscense”。请记住，字符类只匹配一个字符。

### 讨论

某些字符会改变字符类的行为。如果你在方括号开头放置一个插入符号（^），它会否定整个字符类。这意味着字符类将匹配任何不是指定字符的字符。

所以，/[^license]/ 将匹配任何不是“l”、“i”、“c”、“n”、“s”和“e”的字符：

[part_2/character_class/character_class_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/character_class/character_class_ex2.js)

|   | **const** re = */**[^**license**]**/*; |
| --- | --- |
|   |  |
|   | re.test(*"lie"*); *// → false* |
|   | re.test(*"list"*); *// → true* |

这个模式匹配“list”中的“t”，因此test()返回true。你可能已经注意到，插入符号（^）与匹配字符串开始的符号是相同的（配方24，[*使用^和$断言字符串的开始或结束*](f_0035.xhtml#rcp.dollar)）。尽管字符相同，但其含义完全不同。

就像英文单词“arm”在不同的语境中可以有不同的意思（有时是身体的一部分，有时是指武器）。

同时，请记住，插入符号（^）只有在紧接着字符类的开括号后面使用时才有特殊意义。因此，/ [a^bc] / 不会否定字符类，因为“^”会被当作字面字符处理。

与普通的类一样，否定类必须匹配一个字符才能成功。例如，模式/Number[^5]/会匹配“Number6”，但不会匹配“Number”，因为该类期望一个字符：

[part_2/character_class/character_class_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/character_class/character_class_ex3.js)

|   | **const** re = */Number**[^**5**]**/*; |
| --- | --- |
|   |  |
|   | re.test(*"Number6"*); *// → true* |
|   | re.test(*"Number"*); *// → false* |

使用字符类来匹配多个字符中的一个，例如当你想考虑拼写错误或美式英语和英式英语中的拼写差异时。

使用否定字符类列出你不希望出现在字符串中的字符。字符类的一个有趣特点是它能够匹配一系列字符，你将在下一个配方中学习到这一点。
