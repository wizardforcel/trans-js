| Recipe 32 | 使用非捕获组排除结果中的组 |
| --- | --- |

### 任务

假设你需要根据从运动博客上球员的个人资料中抓取的信息来跟踪某个高尔夫球员的排名。排名信息以字符串的形式出现，带有序数指示符，比如“3rd”或“4th”。你只关心数字，不关心后缀，并希望使用捕获组提取出来以便进一步处理。

如果你使用 /(\d{1,2})(st|nd|rd|th)/，第二个括号也会捕获后缀，这是多余的。你需要一种方式告诉正则表达式引擎不要捕获这些字母。

### 解决方案

在开括号后加一个问号（?）和冒号（:），就创建了一个非捕获组：

[part_2/non_capturing_group/non_capturing_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/non_capturing_group/non_capturing_ex1.js)

|   | **const** re = */**(\d{1,3})(?:**st&#124;nd&#124;rd&#124;th**)**/*; |
| --- | --- |
|   | **const** str = *"泰格·伍兹目前在最新的世界高尔夫排名中位列第16。"*; |
|   |  |
|   | **const** match = str.match(re); |
|   |  |
|   | **if** (match) { |
|   | console.log(*"球员排名："* + match[1]); *// → 球员排名：16* |
|   | } |

现在，你的正则表达式能够匹配“16th”这种序数数字，并且你可以在结果数组的第二项中访问该数字。

### 讨论

本示例中的模式匹配一个序数数字，但只记住第一个捕获组：数字。第二个组是非捕获组，因为在开括号后紧跟着一个问号和冒号。

所以，与捕获组不同，非捕获组不会捕获它匹配的子字符串。在这里，“16th”是我们想要匹配的字符串，“16”是我们想要捕获的子字符串，而“th”是我们想要排除的子字符串。

让我们仔细看看这个模式：

|   | /(\d{1,3})(?:st&#124;nd&#124;rd&#124;th)/ |
| --- | --- |
|   |  |
|   | ● (\d{1,3}) 第一个捕获组 |
|   | ○ \d 匹配一个数字（等价于 [0-9]） |
|   | ○ {1,3} 匹配前一个符号 1 到 3 次 |
|   | ● (?:st&#124;nd&#124;rd&#124;th) 非捕获分组 |
|   | ○ 第一种替代方案：st 字面上匹配字符 st |
|   | ○ 第二种替代方案：nd 字面上匹配字符 nd |
|   | ○ 第三种替代方案：rd 字面上匹配字符 rd |
|   | ○ 第四种替代方案：th 字面上匹配字符 th |

match() 方法返回关于结果的丰富信息。在此例中，我们只关心数组中的第二项，即没有序号指示符的排名数字，因此我们使用 str.match(re)[1]。

非捕获分组可以像常规分组一样带有量词。在以下示例中，最后的问号使该分组变为可选，因此该模式也能匹配非序号数字：

[part_2/non_capturing_group/non_capturing_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/non_capturing_group/non_capturing_ex2.js)

|   | **常量** re = */**(\d{1,3})(?:**st&#124;nd&#124;rd&#124;th**)?**/*; |
| --- | --- |
|   | **常量** str = *"老虎·伍兹在最新的世界高尔夫排名中排第16。"*; |
|   |  |
|   | **常量** match = str.match(re); |
|   |  |
|   | **如果** (match) { |
|   | console.log(*"玩家排名: "* + match[1]); *// → 玩家排名: 16* |
|   | } |

正则表达式末尾的问号与分组中的问号无关。它只是告诉正则引擎匹配零次或一次该分组。

请记住，若要避免捕获匹配的子字符串，请使用非捕获分组而不是常规分组。当向现有模式添加更多分组时，你的代码也能从使用非捕获分组中受益。这样，在修改模式时，你就不必做大幅更改。一些引擎在性能上也有细微改进，因为 JavaScript 无需将分组添加到结果中。
