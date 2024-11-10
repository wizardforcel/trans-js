| 配方 34 | 使用特殊的替换模式 |
| --- | --- |

### 任务

假设你有一个私密的群组网页，成员们同意与其他成员分享他们的联系信息。你不想对网站接受的电话号码格式施加任何限制，只要求号码由十个数字组成。因此，用户可能输入123-456-7890、123 456 7890或(123)4567890。

但你希望将数字转换为格式化后的电话号码，以便在整个网站上都能一致地显示，例如(123) 456-7890。为此，你首先需要去除号码中已有的任何格式，然后按照你希望的方式进行格式化。

### 解决方案

通过将非数字字符替换为空字符串来去除所有格式：

[part_2/replacement_patterns/replacement_ex1_p1.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/replacement_patterns/replacement_ex1_p1.js)

|   | **const** phoneNum = *"123-456-7890"*; |
| --- | --- |
|   | **const** re = */**\D**/g*; |
|   |  |
|   | phoneNum.replace(re,*""*); *// → "1234567890"* |

要格式化号码，可以使用捕获组匹配电话号码的不同部分，并通过替换模式引用每个部分：

[part_2/replacement_patterns/replacement_ex1_p2.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/replacement_patterns/replacement_ex1_p2.js)

|   | **const** phoneNum = *"1234567890"*; |
| --- | --- |
|   | **const** re = */**(\d{3})(\d{3})(\d{4})**/*; |
|   |  |
|   | phoneNum.replace(re, *"($1) $2-$3"*); *// → "(123) 456-7890"* |

最终代码应该如下所示：

[part_2/replacement_patterns/replacement_ex1_final.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/replacement_patterns/replacement_ex1_final.js)

|   | **const** phoneNum = *"123-456-7890"*; |
| --- | --- |
|   |  |
|   | **function** formatPhoneNumber(num) { |
|   |  |
|   | *// 去除非数字字符* |
|   | num = num.replace(*/**\D**/g*,*""*); |
|   |  |
|   | *// 格式化号码* |
|   | num = num.replace(*/**(\d{3})(\d{3})(\d{4})**/*, |
|   | *"($1) $2-$3"*); |
|   |  |
|   | **return** num; |
|   | } |
|   |  |
|   | formatPhoneNumber(phoneNum); *// → "(123) 456-7890"* |

成功：你现在有了一个格式化良好的电话号码，尽管用户输入了各种不同的格式。

### 讨论

在这个方案中，我们使用replace()方法来执行正则表达式。replace()的第一个参数是一个正则表达式，它尝试在给定的字符串中查找匹配项，并用第二个参数替换它。第一个正则表达式只包含一个元字符：\D，表示匹配任何非数字字符。当我们使用全局标志(g)时，我们得到一个去除所有非数字字符的字符串。

第二个正则表达式格式化了数字。当我们使用捕获组时，匹配的输入字符串会被存储在内存中，并可以在以后调用。在这种情况下，我们通过使用特殊的替换模式分别回调第一个、第二个和第三个捕获组，形式为$1、$2和$3。

特殊的替换模式以美元符号开始，在replace()方法的第二个参数中使用时具有特殊含义。结果是一个格式化的电话号码，准备显示给最终用户。

### 探索其他特殊替换字符

除了$n外，还有其他特殊字符可以重复使用匹配文本的部分。这些字符是替换字符串中唯一接受的特殊构造，因此像\w这样的元字符在替换字符串中无效。类似地，特殊的替换字符仅在替换字符串中起作用，在正则表达式模式中没有特殊含义。

#### $<Name>

包括一个命名捕获组。如果我们使用命名捕获组编写此方案，解决方案的示例如下：

[part_2/replacement_patterns/replacement_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/replacement_patterns/replacement_ex3.js)

|   | **const** phoneNum = *"123-456-7890"*; |
| --- | --- |
|   |  |
|   | **function** formatPhoneNumber(num) { |
|   |  |
|   | *// 移除非数字* |
|   | num = num.replace(*/**\D**/g*,*""*); |
|   |  |
|   | *// 格式化数字* |
|   | num = num.replace(*/**(?<**area>**\d{3})(?<**exchange>**\d{3})(?<**line>**\d{4})**/*, |
|   | *"($<area>) $<exchange>-$<line>"*); |
|   |  |
|   | **return** num; |
|   | } |
|   |  |
|   | formatPhoneNumber(phoneNum); *// → "(123) 456-7890"* |

有关命名捕获组的进一步解释，请参见第33个配方，[*使用命名捕获组轻松读取组*](f_0044.xhtml#rcp.named_capturing_group)。

#### $n

包含第n个捕获组，其中n是正整数。你已经看到这个特殊字符的实际应用，但我们在这里包括它以便比较：

[part_2/replacement_patterns/replacement_ex7.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/replacement_patterns/replacement_ex7.js)

|   | **const** str = *"cold & hot"*; |
| --- | --- |
|   | **const** re = */**（cold**）\s**&**\s（hot**）**/*; |
|   |  |
|   | str.replace(re, *"$2 & $1"*); *// → "hot & cold"* |
| 仅在正则表达式中可用 |
| --- |
| ![images/aside-icons/important.png](images/aside-icons/important.png) | $n 和 $<Name> 仅在模式是正则表达式时具有特殊含义。在字符串中，它们被视为字面量。 |

#### $& 

包含匹配子字符串的副本。例如：

[part_2/replacement_patterns/replacement_ex4.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/replacement_patterns/replacement_ex4.js)

|   | **const** str = *"FAT是计算机文件系统架构"*; |
| --- | --- |
|   | **const** re = */FAT/*; |
|   |  |
|   | str.replace(re, *"$&（文件分配表）"*); |
|   | *// → "FAT（文件分配表）是计算机文件系统架构"* |

#### $’

以美元符号后跟撇号的形式包含输入中匹配子字符串之后的部分。例如：

[part_2/replacement_patterns/replacement_ex5.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/replacement_patterns/replacement_ex5.js)

|   | **const** str = *"#3"*; |
| --- | --- |
|   | **const** re = */#/*; |
|   |  |
|   | str.replace(re, *"#$'"*); *// → "#33"* |

#### $‘

一个美元符号后跟反引号，包含输入中匹配子字符串之前的部分：

[part_2/replacement_patterns/replacement_ex6.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/replacement_patterns/replacement_ex6.js)

|   | **const** str = *"1000 liter"*; |
| --- | --- |
|   | **const** re = */liter/*; |
|   |  |
|   | str.replace(re, *"liter = $`kg"*); *// → "1000 Liter = 1000 kg"* |

有时候，撇号和反引号之间的区别可能很难看清。记住它们的区别的一种方法是，反引号指向后方，因此给出的是匹配之前的字符串。

#### $$

包含美元符号（$）：

[part_2/replacement_patterns/replacement_ex8.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/replacement_patterns/replacement_ex8.js)

|   | **const** str = *"€700"*; |
| --- | --- |
|   | **const** re = */€/*; |
|   |  |
|   | str.replace(re, *"$$"*); *// → "$700"* |

我们将在第35个食谱中更详细地讨论这个模式，[*去除替换模式的特殊含义*](f_0046.xhtml#rcp.neutralizing_replacement)。

| 排序 |
| --- |
| ![images/aside-icons/tip.png](images/aside-icons/tip.png) | 你可以多次使用特殊替换字符，并且顺序不限。 |

利用替换字符串中的特殊替换字符来引用匹配子字符串的不同部分。需要记住的一点是，replace()方法不会修改原始字符串。相反，它会创建一个新字符串，执行替换操作，并返回编辑后的副本。
