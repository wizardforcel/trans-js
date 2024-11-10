| 配方 50 | 使用否定回顾测试模式 |
| --- | --- |

### 任务

假设你正在搜索医院记录，寻找名为Smith的病人，但大多数从搜索结果中得到的数据是关于Dr. Smith的。你需要一个正则表达式，它匹配“Smith”，但排除“Dr. Smith”。

### 解决方案

使用否定回顾断言，表示为(?<! ... )：

[part_2/negative_lookbehind/negative_lookbehind_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/negative_lookbehind/negative_lookbehind_ex1.js)

|   | **const** re = */**(?<**!Dr**\.\s)**Smith/*; |
| --- | --- |
|   |  |
|   | console.log(re.test(*"Dr. Smith"*)); *// → false* |
|   | console.log(re.test(*"Mr. Smith"*)); *// → true* |
|   | console.log(re.test(*"John Smith"*)); *// → true* |

你的正则表达式现在会找到所有包含“Smith”的记录，但不包括“Dr. Smith”。

### 讨论

否定版本的回顾符号用于断言回顾中的模式前面没有某个模式。在这种情况下，我们使用它来确保单词“Smith”前面没有大写字母D、小写字母r、句点（.）和空格字符（\s）。你必须使用反斜杠来转义句点；否则，正则引擎会将其解释为元字符。

| 不仅仅在开始时 |
| --- |
| ![images/aside-icons/tip.png](images/aside-icons/tip.png) | 回顾符号可以在正则表达式中的任何位置使用，而不仅仅是在开始处。 |

![images/aside-icons/info.png](images/aside-icons/info.png)

除了回顾符号，正则表达式还提供了几种类型的组，它们是通过一对括号构造的，开括号后面紧跟着一个问号。为了方便比较，我们总结了这些组的语法，表格如下。记得将此表格收藏——它一定会派上用场：

| 元字符 | 含义 |
| --- | --- |
| ( ... ) | 捕获组 |
| (?: ... ) | 非捕获组 |
| (?= ... ) | 正向前瞻 |
| (?! ... ) | 否定前瞻 |
| (?<= ... ) | 正向回顾 |
| (?<! ... ) | 负向前瞻 |

这份技巧的关键是当你想匹配一个没有被特定模式前置的模式时，使用负向前瞻。
