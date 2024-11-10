| 方案 29 | 使用量词重复正则表达式的一部分 |
| --- | --- |

### 任务

假设你想在程序中添加一个选项，允许用户使用 PIN 码登录。使用 PIN 码而不是密码的主要好处是更快的登录。我通常在离开时把电脑设为休眠，即使是短时间的离开。方便的是，我的操作系统让我仅通过 PIN 码就能快速登录。

假设你想为你的应用程序实现类似的功能。你需要编写一个正则表达式模式，1）验证输入是数字，2）确保数字的位数在 4 到 6 位之间。

### 解决方案

在 `\d` 字符类后面加上一对大括号，指定数字应出现的次数：

[part_2/quantifiers/quantifiers_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/quantifiers/quantifiers_ex1.js)

|   | **const** re = */^**\d{4,6}**$/*; |
| --- | --- |
|   |  |
|   | re.test(*"107"*); *// → false* |
|   | re.test(*"1077"*); *// → true* |
|   | re.test(*"107781"*); *// → true* |
|   | re.test(*"1077815"*); *// → false* |

模式 `{n,m}` 允许我们将前面的项匹配至少 `n` 次，最多 `m` 次（`n` 和 `m` 必须是正整数）。

这段代码中的正则表达式以插入符号（`^`）开头，以美元符号（`$`）结尾。我们不想匹配除 4 到 6 位数字输入之外的任何内容，因此我们使用 `^` 和 `$` 来限定模式（关于插入符号和美元符号的进一步解释，请参见第 24 章，[*使用 ^ 和 $ 断言字符串的开始和结束*](f_0035.xhtml#rcp.dollar)）。

如果没有 `$`，这个模式会匹配类似“107781pass”这样的字符串：

[part_2/quantifiers/quantifiers_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/quantifiers/quantifiers_ex2.js)

|   | /**\**d{4,6}*/.test**(**"107781pass"**)**; /*/ **→** **true** |
| --- | --- |

### 讨论

我们可以使用量词重复匹配一个标记或组。{4} 是一个量词，它告诉正则表达式引擎精确地匹配它前面的项目四次。因此，模式[0-5]{4} 相当于[0-5][0-5][0-5][0-5]，但更容易阅读和编写。

如果我们使用量词重复字符类，那么整个字符类将被重复，而不仅仅是它所匹配的字符。例如，模式[car]{3} 匹配的是三个连续的字符，分别是“c”、“a”和“r”：

[part_2/quantifiers/quantifiers_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/quantifiers/quantifiers_ex3.js)

|   | **const** re = */**[**car**]{3}**/*; |
| --- | --- |
|   |  |
|   | re.test(*"car"*); *// → true* |
|   | re.test(*"arc"*); *// → true* |
|   | re.test(*"carbon"*); *// → true（匹配前面三个字符）* |

要重复字符类匹配到的相同字符，我们可以使用回溯引用（将在第46条配方中讨论，[*使用回溯引用引用匹配字符串*](f_0057.xhtml#rcp.backreference)）。

字符类是正则表达式中唯一一个量词没有特殊含义的地方。例如，/[c{3}]/ 匹配的是一个字符，可能是“c”、“{”、“3”或“}”。为了去除量词在字符类外的特殊含义，我们必须用反斜杠对其进行转义。例如：

[part_2/quantifiers/quantifiers_ex4.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/quantifiers/quantifiers_ex4.js)

|   | **const** re = */**\{**7**\}**/*; |
| --- | --- |
|   |  |
|   | re.test(*"{7}"*); *// → true* |
|   | re.test(*"7"*); *// → false* |
|   | re.test(*"abc"*); *// → false* |

在这个模式中，\{ 字符表示字面上的左花括号“{”。如果没有反斜杠，{ 则表示量词的开始。

尽管花括号是正则表达式中常见的一种量词，但也有其他类型的量词可供使用。以下部分将提供关于这些额外量词的信息。

### 量词的类型

量词指定字符、字符组或字符类要匹配的出现次数。正则表达式中有六种量词形式：零次或多次（*），一次或多次（+），零次或一次（?），恰好 n 次 {n}，至少 n 次 {n,}，以及从 n 到 m 次 {n,m}。让我们来看看每种形式以及如何使用它们。

#### 零个或多个（*）

星号（*）匹配前一个项目的零次或多次序列。假设我们想匹配“play”一词的所有动词形式，包括“played”、“plays”和“playing”。通过在字符类（\w）后使用量词，我们可以告诉正则表达式匹配“play”以及任何可能跟在它后面的字符，只要它是一个单词字符：

[part_2/quantifiers/quantifiers_ex5.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/quantifiers/quantifiers_ex5.js)

|   | **const** re = */**\b**play**\w*****\b**/*; |
| --- | --- |
|   |  |
|   | re.test(*"他为克里夫兰队效力"*); *// → true* |
|   | re.test(*"法国明天将与英格兰队比赛。"*); *// → true* |
|   | re.test(*"埃文斯踢得非常好。"*); *// → true* |
|   | re.test(*"我们来玩个不同的游戏"*); *// → true* |

请注意，这个模式也会匹配像“playful”和“playground”这样的单词。为了将匹配限制为一组特定的单词，我们可以使用竖线（请参见食谱26，[*使用竖线（|）匹配多个选择之一*](f_0037.xhtml#rcp.vertical_bar)）。

#### 一次或多次（+）

加号（+）匹配前一个项目的一个或多个序列。例如，正则表达式 /Go+al/ 尝试匹配字母 G 后跟一个或多个字母 o，然后是字母 a 和 l：

[part_2/quantifiers/quantifiers_ex6.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/quantifiers/quantifiers_ex6.js)

|   | **const** re = */Go+al!/*; |
| --- | --- |
|   |  |
|   | re.test(*"Gooooooooal!"*); *// → true* |
|   | re.test(*"Goal!"*); *// → true* |
|   | re.test(*"Gal!"*); *// → false (预期至少有一个字母 o)* |

#### 零或一（?）

问号匹配前一个项目零次或一次出现。例如，如果我们想匹配单词“apple”或其复数形式“apples”，我们可以写成\apples?\. 这个模式告诉正则表达式引擎匹配单词“apple”，后面跟着零次或一次字母“s”：

[part_2/quantifiers/quantifiers_ex7.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/quantifiers/quantifiers_ex7.js)

|   | **const** re = */apples**?**/*; |
| --- | --- |
|   |  |
|   | re.test(*"每天一个苹果，医生远离我"*); *// → true* |
|   | re.test(*"削皮并去核苹果"*); *// → true* |

#### 正好 n 次 {n}

指定前一个项目可以重复的次数。n必须是正整数。例如，我们可以使用/\b\w{3}\b/来匹配字符串中的任何三字母单词：

[part_2/quantifiers/quantifiers_ex8.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/quantifiers/quantifiers_ex8.js)

|   | **const** re = */**\b\w{3}\b**/*; |
| --- | --- |
|   |  |
|   | re.test(*"一次车祸"*); *// → true* |
|   | re.test(*"一张驾驶执照"*); *// → false* |

#### 从 n 到 m 次 {n,m}

匹配前一个项目至少 n 次，最多 m 次。n 和 m 必须是正整数。我们已经看过这个模式的应用。但是，为了更好地理解它是如何工作的，让我们看另一个例子：

[part_2/quantifiers/quantifiers_ex10.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/quantifiers/quantifiers_ex10.js)

|   | **const** re = */**\b**im**{1,2}\w*****?**/*; |
| --- | --- |
|   |  |
|   | re.test(*"完美无瑕的"*); *// → true* |
|   | re.test(*"冲击"*); *// → true* |
|   | re.test(*"疯狂的"*); *// → false* |

在这里，模式尝试匹配单词边界，后跟字母“i”，然后是一个或两个字母“m”。因此，它可以匹配任何以“im”或“imm”开头的单词。

#### 至少 n 次 {n,}

{n,} 类似于 {n,m}，它会匹配前面的项目至少 n 次，但没有第二个参数。例如，正则表达式 /\d{2,}/ 匹配两个或更多数字：

[part_2/quantifiers/quantifiers_ex9.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/quantifiers/quantifiers_ex9.js)

|   | **const** re = */**\d{2,}**/*; |
| --- | --- |
|   |  |
|   | re.test(*"1"*); *// → false* |
|   | re.test(*"12"*); *// → true* |
|   | re.test(*"123"*); *// → true* |
| 相似的量词 |
| --- |
| ![images/aside-icons/tip.png](images/aside-icons/tip.png) | 模式 {1,} 等价于量词 +，{0,} 等价于 *，而 {0,1} 等价于 ?。 |

使用量词来指定要匹配的字符或表达式的数量。不同类型的量词允许你精确地设置前面的项目应当匹配多少次。
