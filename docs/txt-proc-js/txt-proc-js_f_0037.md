| 配方 26 | 使用竖线（&#124;）匹配多个备选项 |
| --- | --- |

### 任务

假设你想匹配“week”这个词的不同变体，包括“weekend”和“weekly”，但不包括“weekday”。你希望匹配发生在单词边界处，这样像“Newsweek”这样的词就不会被当作匹配项。你需要的是一种在正则表达式中定义备选模式的方法。

### 解决方案

使用竖线（|）来形成交替。竖线字符会告诉正则表达式引擎匹配一系列模式中的任何一个：

[part_2/vertical_bar/vertical_bar_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/vertical_bar/vertical_bar_ex1.js)

|   | **const** re = */**\b**week**\b**&#124;**\b**weekend**\b**&#124;**\b**weekly**\b**/*; |
| --- | --- |
|   |  |
|   | re.test(*"How much do you earn per week?"*); *// → true* |
|   | re.test(*"Employees are paid weekly."*); *// → true* |
|   | re.test(*"The office is closed on the weekend."*); *// → true* |
|   | re.test(*"Your story could be featured on Newsweek!"*); *// → false* |

正则表达式引擎会匹配竖线左边的所有内容或右边的所有内容。这个例子中的模式有三个备选项，每个选项都被一对单词边界包围。所以，它只会匹配“week”、“weekend”或“weekly”。

### 讨论

如果你想在模式中添加其他符号，但又不希望它们成为交替的一部分，你可以使用括号。使用括号会限制交替的范围。

记住，竖线匹配的是左侧或右侧的任何内容。所以，如果你想匹配“this week”或“this weekend”，你可以写/\bthis (week|weekend)\b/：

[part_2/vertical_bar/vertical_bar_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/vertical_bar/vertical_bar_ex2.js)

|   | **const** re = */**\b**this* *(**week&#124;weekend**)\b**/*; |
| --- | --- |
|   |  |
|   | re.test(*"Are you free this weekend?"*); *// → true* |
|   | re.test(*"Are you free this week?"*); *// → true* |
|   | re.test(*"weekend"*); *// → false* |

该模式告诉正则引擎查找一个单词边界，接着是“this”加空格，然后是“week”或“weekend”，最后是另一个单词边界。

你还可以使用括号，以更简洁的形式重写本食谱中的解决方案：

[part_2/vertical_bar/vertical_bar_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/vertical_bar/vertical_bar_ex3.js)

|   | **const** re = */**\b(**week&#124;weekend&#124;weekly**)\b**/*; |
| --- | --- |
|   |  |
|   | re.test(*"你每周赚多少钱？"*); *// → true* |
|   | re.test(*"员工每周领取薪水。"*); *// → true* |
|   | re.test(*"办公室在周末关闭。"*); *// → true* |
|   | re.test(*"你的故事可能会出现在《新闻周刊》上！"*); *// → false* |

结果是相同的，但这个模式更具可读性。由于本例中的三个选项都以相同的单词开始，我们可以通过重新表述正则表达式来进一步优化正则引擎：

[part_2/vertical_bar/vertical_bar_ex4.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/vertical_bar/vertical_bar_ex4.js)

|   | **const** re = */**\b**week**(**end&#124;ly&#124;**)\b**/*; |
| --- | --- |
|   |  |
|   | re.test(*"你每周赚多少钱？"*); *// → true* |
|   | re.test(*"员工每周领取薪水。"*); *// → true* |
|   | re.test(*"办公室在周末关闭。"*); *// → true* |
|   | re.test(*"你的故事可能会出现在《新闻周刊》上！"*); *// → false* |

括号中的选项告诉正则引擎匹配“end”、“ly”或不匹配任何内容。括号末尾的空选项是必要的，以便能够匹配“week”。另外，你也可以使用量词来使括号中的模式可选，如：/\bweek(end|ly)?\b/，这种写法更为常规（参见食谱29，[*使用量词重复正则表达式的一部分*](f_0040.xhtml#rcp.quantifiers)）。

正则表达式引擎通常从左到右匹配列表中的单词。因此，将在文本中最可能出现的单词排列在列表的开头，可能会稍微提高引擎的性能。

记住，当你想匹配一组正则表达式中的某一项时，利用 alternation（交替），并添加括号来限制交替的范围。
