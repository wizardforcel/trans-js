| 食谱 33 | 使用命名捕获组轻松读取组 |
| --- | --- |

### 任务

假设你需要通过搜索日志文件来找出错误发生的确切时间。你知道时间的格式是小时、分钟、秒钟以及AM/PM标识符（HH:MM:SS XM）。为了提取每个时间段，你创建了一个可以识别并单独捕获每个段的模式。然而，随着模式中捕获组数量的增加，本已晦涩的正则表达式语法变得更加难以阅读。考虑这个例子：

[part_2/named_capturing_group/ncg_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/named_capturing_group/ncg_ex1.js)

|   | **const** re = */**(\d{2})**:**(\d{2})**:**(\d{2})\s(\w{2})**/*; |
| --- | --- |
|   | **const** match = *"09:30:00 AM"*.match(re); |
|   |  |
|   | console.log(match[1]); |
|   | console.log(match[2]); |
|   | console.log(match[3]); |
|   | console.log(match[4]); |

这些匹配项中，哪一个表示分钟？哪一个表示秒钟？使用更具表现力的语法来分组各个部分，可以大大减少代码中出现问题的可能性。

### 解决方案

使用命名捕获组：

[part_2/named_capturing_group/ncg_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/named_capturing_group/ncg_ex2.js)

|   | **const** re = */**(?<**hour>**\d{2})**:**(?<**min>**\d{2})**:**(?<**sec>**\d{2})\s(?<**period>**\w{2})**/*; |
| --- | --- |
|   | **const** match = *"09:30:00 AM"*.match(re); |
|   |  |
|   | console.log(match.groups.hour); *// → 09* |
|   | console.log(match.groups.min); *// → 30* |
|   | console.log(match.groups.sec); *// → 00* |
|   | console.log(match.groups.period); *// → AM* |

命名捕获组使用更为扩展的语法形式 `(?<name>...)`。因此，带有多个捕获组的模式可以更容易地读取和编辑。

### 讨论

命名捕获组是ES2018引入的一种语法。有效的捕获组名称必须是一个以字母开头的字母数字序列。为了避免与现有属性名称发生冲突，JavaScript将所有命名组分配给一个单独的对象，称为groups。

如果一个模式有一个可选的命名捕获组且该组没有参与匹配，它仍然会在groups对象中为该组创建一个属性。让我们通过在代码中的最后一个捕获组后面加上问号，使其变为可选，以看看会发生什么：

[part_2/named_capturing_group/ncg_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/named_capturing_group/ncg_ex3.js)

|   | **const** re = */**(?<**hour>**\d{2})**:**(?<**min>**\d{2})**:**(?<**sec>**\d{2})\s?(?<**period>**\w{2})?**/*; |
| --- | --- |
|   |  |
|   | *// 无AM/PM的时间戳* |
|   | **const** str = *"09:30:00"*; |
|   |  |
|   | **const** match = str.match(re); |
|   |  |
|   | console.log(match.groups); |
|   | *// → {hour: "09", min: "30", sec: "00", period: undefined}* |

在这个例子中，period没有参与匹配，但它仍然被包含在groups对象中。即使正则表达式中没有命名组，groups对象仍会在结果中可用。

[part_2/named_capturing_group/ncg_ex4.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/named_capturing_group/ncg_ex4.js)

|   | **const** re = */**\w**+/*; |
| --- | --- |
|   | **const** match = *"abc"*.match(re); |
|   |  |
|   | console.log(*"groups"* **in** match); *// → true* |

也可以使用数字引用来访问命名组。当然，使用数字引用会破坏我们方法的目的（轻松读取组的值）。然而，当你只想提高代码中正则部分的可读性时，数字引用可能会非常有用：

[part_2/named_capturing_group/ncg_ex5.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/named_capturing_group/ncg_ex5.js)

|   | **const** re = */**(?<**hour>**\d{2})**:**(?<**minute>**\d{2})**:**(?<**second>**\d{2})**/*; |
| --- | --- |
|   | **const** match = *"09:30:00"*.match(re); |
|   |  |
|   | console.log(match[0]); *// → 09:30:00* |
|   | console.log(match[1]); *// → 09* |
|   | console.log(match[2]); *// → 30* |
|   | console.log(match[3]); *// → 00* |

利用命名捕获组语法，在编写包含多个捕获组的模式时，可以轻松编辑模式并读取结果。
