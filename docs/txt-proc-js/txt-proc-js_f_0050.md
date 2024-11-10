| 例子 39 | 使用 g 和 i 标志进行全局和不区分大小写的匹配 |
| --- | --- |

### 任务

假设你的任务是为一个现有公司网站创建美国版。你需要搜索网页内容，找到“tyre”一词的所有实例，包括它的复数形式“tyres”，并将它们每个都替换为美国拼写的“tire”。搜索必须忽略字母大小写，因此也能匹配句首的“Tyre”。

另一个要求是找到字符串中所有可能的匹配项。所以，搜索不能在找到第一个匹配项后就停止，而是必须继续在剩余的字符串中查找更多匹配项。手动完成这些操作需要很多时间。幸运的是，正则表达式的标志可以解决这个问题。

| 再来一次？ |
| --- |
| ![images/aside-icons/info.png](images/aside-icons/info.png) | 你已经在前面的示例中看到过 i 和 g 标志的作用。这个例子会再讲解一次它们，帮助你加深理解。 |

### 解决方案

在模式末尾添加 i 和 g：

[part_2/flag_global_insensitive/gi_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/flag_global_insensitive/gi_ex1.js)

|   | **const** str = *`轮胎气压以每平方英寸磅（PSI）表示* |
| --- | --- |
|   | *(PSI)。适当的轮胎气压对于最佳操控非常重要。* |
|   | *每月检查轮胎的磨损情况很重要。`*; |
|   |  |
|   | **const** re = */**\b(**t**)**yre**(**s**)?\b**/gi*; |
|   |  |
|   | str.replace(re, *"$1ire$2"*); |
|   | *// → "轮胎气压以每平方英寸磅（PSI）表示。* |
|   | *// 合适的轮胎气压对于最佳操控非常重要。它很重要* |
|   | *// 每月检查轮胎的磨损情况。"* |

任务完成！字符串中的所有“tyre”都已被替换为“tire”。

### 讨论

在正则表达式字面量中，可以通过在模式后面的斜杠添加单字母标志（也称为修饰符）来指定选项。通常，replace()方法仅替换字符串中指定模式的第一个出现。但在这里，我们使用了全局搜索标志（g），它指示引擎继续搜索其他模式的出现。

i标志与g标志互补，要求引擎以不区分大小写的方式进行匹配。以下是正则表达式中每个标记的作用：

|   | /\b(t)yre(s)?\b/gi |
| --- | --- |
|   |  |
|   | ● \b表示单词边界的位置 |
|   | ● (t) 第一个捕获组 |
|   | ○ t字面匹配字符"t" |
|   | ● yre字面匹配字符"yre" |
|   | ● (s)? 第二个捕获组 |
|   | ○ s字面匹配字符"s" |
|   | ○ ?表示前一个标记匹配零次或一次（贪婪模式） |
|   | ● \b表示单词边界的位置 |
|   | ● 标志 |
|   | ○ g全局匹配 |
|   | ○ i不区分大小写的匹配 |

请注意replace()方法第二个参数中的特殊字符$1和$2。这些字符在替换字符串中有特殊含义。模式$1表示第一个捕获组匹配到的值。

在这里，$1指的是第一个捕获组匹配到的字符，$2指的是第二个捕获组匹配到的字符。因此，如果模式匹配到以大写字母“T”开头的单词“Tyre”，该单词会被替换为“Tire”。

类似地，如果模式匹配到单词“tyres”中的可选“s”，该单词将被替换为“tires”。欲了解更多关于特殊替换模式的信息，请参见第34条[*使用特殊替换模式*](f_0045.xhtml#rcp.replacement_patterns)。

JavaScript的正则表达式风格支持七个可选标志，包括d、g、i、m、s、u和y。与g类似，这些标志可以放在字面量的闭合定界符后面，或者作为第二个参数传递给RegExp()构造函数。我们将在接下来的教程中逐一介绍这些标志。