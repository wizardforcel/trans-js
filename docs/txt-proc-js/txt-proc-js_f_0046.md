| 配方 35 | 去除替换模式的特殊含义 |
| --- | --- |

### 任务

假设你的任务是将不同服务的定价添加到网站的博客中。更具体地说，你需要添加汽车服务中心换轮胎的费用。在你的第一次尝试中，你提出了如下的解决方案：

[part_2/neutralizing_replacement/nrp_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/neutralizing_replacement/nrp_ex1.js)

|   | **const** str = *"在我们的商店，换轮胎大约需要 15 分钟。"*; |
| --- | --- |
|   | **const** re = */**\b(**tire change**)\b**/*; |
|   |  |
|   | str.replace(re, *"$1 (每个轮胎收费$10)"*); |
|   | *// → "在我们的商店，换轮胎（每个轮胎收费$10）* |
|   | *// 大约需要 15 分钟。"* |

这个正则表达式试图在字符串中找到“换轮胎”短语并在括号中添加费用。它使用了 $1 的特殊替换模式，但由于正则表达式将 $10 视为特殊的替换模式，结果是不可用的。

你需要一种方法来去除 $1 在 $10 中的特殊含义，$1 在模式中有一个对应的捕获组，并且需要将字符按字面意义使用。

### 解决方案

用另一个美元符号转义美元符号：

[part_2/neutralizing_replacement/nrp_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/neutralizing_replacement/nrp_ex2.js)

|   | **const** str = *"在我们的商店，换轮胎大约需要 15 分钟。"*; |
| --- | --- |
|   | **const** re = */**\b(**tire change**)\b**/*; |
|   |  |
|   | str.replace(re, *"$1 (每个轮胎收费$$10)"*); |
|   | *// → "在我们的商店，换轮胎（每个轮胎收费$10）需要* |
|   | *// 大约需要 15 分钟。"* |

成功的结果！美元符号中和了 $1 的特殊含义，因此正则表达式引擎将其识别为字面字符。

### 讨论

在这个示例中，正则表达式有一个捕获组。但是，如果你尝试引用一个实际上不存在的组会发生什么呢？如果你在替换文本中输入$2，它将不会对应任何内容。例如：

[part_2/neutralizing_replacement/nrp_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/neutralizing_replacement/nrp_ex3.js)

|   | **const** str = *"在我们的商店，轮胎更换大约需要15分钟。"*; |
| --- | --- |
|   | **const** re = */**\b(**tire change**)\b**/*; |
|   |  |
|   | str.replace(re, *"$1（每个轮胎需要$20）"*); |
|   | *// → "在我们的商店，轮胎更换（每个轮胎需要$20）大约需要* |
|   | *// 15分钟。"* |

如果你在替换字符串中使用两位数的引用，结果将取决于模式中的捕获组数量。如果你有十个捕获组并使用$10，它将引用第十个捕获组。如果你有更少的捕获组，$10只会使用第一位数字引用第一个捕获组，并将0作为文字替换字符串。这就是本示例中第一个例子的情况：“cost $10”中的“$1”引用了“tire change”，而“0”被当作文字字符处理。

本示例的重点是使用$来中和替换模式的特殊含义。
