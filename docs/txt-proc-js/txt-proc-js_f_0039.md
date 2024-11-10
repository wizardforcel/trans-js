| 配方 28 | 使用字符类匹配字符范围 |
| --- | --- |

### 任务

假设你的任务是搜索扫描的文档并筛选出年龄在 20 到 40 岁之间的申请者。你需要提取的信息前面会有“age:”字样。所以，你的正则表达式模式应该匹配“age”这个词，后面跟一个冒号，再跟一个空格，最后是一个 20 到 40 之间的数字范围。

根据你迄今为止学到的内容，你可以在一对圆括号中使用竖线来指定可能的匹配项，像这样：

[part_2/character_class_range/range_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/character_class_range/range_ex1.js)

|   | /Age: (2(0&#124;1&#124;2&#124;3&#124;4&#124;5&#124;6&#124;7&#124;8&#124;9)&#124;3(0&#124;1&#124;2&#124;3&#124;4&#124;5&#124;6&#124;7&#124;8&#124;9)&#124;40)/ |
| --- | --- |

但是，如果你想查找更大的数字范围怎么办？你需要一种更好的方式来定义正则表达式中的字符范围。

### 解决方案

使用字符类，并在你要查找的数字范围之间放置一个连字符：

[part_2/character_class_range/range_ex2_v1.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/character_class_range/range_ex2_v1.js)

|   | **const** re = */Age:* *(**2**[**0-9**]**&#124;3**[**0-9**]**&#124;40**)**/*; |
| --- | --- |
|   |  |
|   | re.test(*"Name: John &#124; Age: 23"*); *// → true* |
|   | re.test(*"Name: Ana &#124; Age: 54"*); *// → false* |

当连字符出现在字符类中时，它会被视为元字符。但有一个例外：如果它是字符类中的第一个或最后一个字符，它就不会定义一个范围，因此它失去其特殊含义，被视为普通字符。

你甚至可以进一步简化模式，像这样：

[part_2/character_class_range/range_ex2_v2.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/character_class_range/range_ex2_v2.js)

|   | **const** re = */Age:* *([**23**][**0-9**]**&#124;40**)**/*; |
| --- | --- |
|   |  |
|   | re.test(*"Name: John &#124; Age: 23"*); *// → true* |
|   | re.test(*"Name: Ana &#124; Age: 54"*); *// → false* |

在这里，[23] 匹配 2 或 3，[0-9] 匹配范围 0 到 9 内的单个数字。它们共同匹配一个 20 到 39 之间的数字。末尾的竖线告诉引擎要么匹配 20-39，要么匹配 40。

### 讨论

如果你的正则表达式仅涉及验证数字范围，你可以通过 JavaScript 内置方法实现相同的效果。参考以下示例：

[part_2/character_class_range/range_pure_js.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/character_class_range/range_pure_js.js)

|   | **const** str1 = *"Name: John &#124; Age: 23"*; |
| --- | --- |
|   | **const** str2 = *"Name: Ana &#124; Age: 54"*; |
|   |  |
|   | **function** verifyAge(str) { |
|   | **const** index = str.indexOf(*"Age: "*); |
|   | **const** endIndex = index + 5; |
|   | **const** age = str.slice(endIndex, endIndex + 2); |
|   | **if** (age >= 20 && age <= 40) { |
|   | **return** **true**; |
|   | } **else** { |
|   | **return** **false**; |
|   | } |
|   | } |
|   |  |
|   | console.log(verifyAge(str1)); *// → true* |
|   | console.log(verifyAge(str2)); *// → false* |

这段代码执行以下步骤：

+   它在输入字符串中查找 "Age:" 的索引

+   它将 "Age:" 子字符串的长度加到索引上，以获取数字的位置

+   它使用 slice() 方法提取数字

+   它随后使用小于等于（<=）和大于等于（>=）运算符检查提取的年龄是否在有效范围内。

让 JavaScript 来决定一个数字是否在范围内通常能减少错误。正则表达式学习者常犯的一个错误是用单个字符类定义双数字范围。模式 [12-24] 并不会匹配 12 到 24 之间的数字，而是匹配字符 “1”、"2" 或 "4"（等同于 [124]）。

这是正则引擎如何解析 [12-24]：

+   1 匹配字符 "1"

+   2-2 匹配范围“2”到“2”之间的单个字符

+   4 匹配字符“4”

要定义一个匹配双位数范围的模式，我们需要使用两个字符类和一个竖线：

[part_2/character_class_range/range_ex3_v1.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/character_class_range/range_ex3_v1.js)

|   | **const** re = */1**[**2-9**]**&#124;2**[**0-4**]**/*; |
| --- | --- |
|   |  |
|   | re.test(*"10"*); *// → false* |
|   | re.test(*"15"*); *// → true* |
|   | re.test(*"24"*); *// → true* |
|   | re.test(*"25"*); *// → false* |
|   | re.test(*"015"*); *// → true* |
|   | re.test(*"240"*); *// → true* |

这个模式中缺少了什么吗？是的，一对单词边界（\b）。没有单词边界，模式还会匹配“015”和“150”。所以，为了匹配12到24之间的双位数范围，我们的模式应该是这样的：

[part_2/character_class_range/range_ex3_v2.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/character_class_range/range_ex3_v2.js)

|   | **const** re = */**\b**1**[**2-9**]**&#124;2**[**0-4**]\b**/*; |
| --- | --- |
|   |  |
|   | re.test(*"10"*); *// → false* |
|   | re.test(*"15"*); *// → true* |
|   | re.test(*"24"*); *// → true* |
|   | re.test(*"25"*); *// → false* |
|   | re.test(*"015"*); *// → false* |
|   | re.test(*"240"*); *// → false* |

我们用连字符定义的范围不仅限于数字。我们也可以定义字母范围。例如，[a-z] 匹配任何小写字母，[A-Z] 匹配任何大写字母：

[part_2/character_class_range/range_ex4_v1.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/character_class_range/range_ex4_v1.js)

|   | **const** re = */Group* *[**A-Z**]**/*; |
| --- | --- |
|   |  |
|   | re.test(*"Group B"*); *// → true* |
|   | re.test(*"Group 2"*); *// → false* |

我们甚至可以列出多个范围，像这样：

[part_2/character_class_range/range_ex4_v2.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/character_class_range/range_ex4_v2.js)

|   | **const** re = */Group* *[**A-Z0-9**]**/*; |
| --- | --- |
|   |  |
|   | re.test(*"Group B"*); *// → true* |
|   | re.test(*"Group 2"*); *// → true* |

我们指定范围的顺序无关紧要。所以，[A-Z0-9] 与 [0-9A-Z] 是一样的。要列出我们不想包含的字符范围，可以使用插入符号（^）。如果我们使用 /Group [^A-C]/，则该类匹配“Group”后跟一个空格，再跟一个不是“A”、“B”或“C”的字符：

[part_2/character_class_range/range_ex5.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/character_class_range/range_ex5.js)

|   | **const** re = */Group* *[^**A-C**]**/*; |
| --- | --- |
|   |  |
|   | re.test(*"Group A"*); *// → false* |
|   | re.test(*"Group B"*); *// → false* |
|   | re.test(*"Group C"*); *// → false* |
|   | re.test(*"Group D"*); *// → true* |
|   | re.test(*"Group 5"*); *// → true* |

### 使用预定义的范围

匹配字符范围是正则表达式中最常见的任务之一。因此，正则表达式的各种变体提供了特殊字符，作为匹配字符范围的简写。大多数简写由反斜杠和一个字符组成，例如 \d，它匹配数字字符。句点（.）是一个例外，它是唯一一个不以反斜杠开头的简写字符类。

保留以下简写字符类列表，以备后用——它们肯定会派上用场。

#### 数字字符（\d）

\d 匹配任何 ASCII 数字字符，等同于 [0-9]。例如：

[part_2/character_class_range/range_ex6.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/character_class_range/range_ex6.js)

|   | **const** re = */**\d**/*; |
| --- | --- |
|   |  |
|   | re.test(*"5"*); *// → true* |
|   | re.test(*"a"*); *// → false* |

#### 单词字符（\w）

\w 匹配任何 ASCII 字符，等同于 [A-Za-z0-9_]。请注意，下划线在正则表达式中是字字符：

[part_2/character_class_range/range_ex7.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/character_class_range/range_ex7.js)

|   | **const** re = */**\w**/*; |
| --- | --- |
|   |  |
|   | re.test(*"5"*); *// → true* |
|   | re.test(*"a"*); *// → true* |
|   | re.test(*"_"*); *// → true* |
|   | re.test(*"*"*); *// → false* |

#### 空白字符 (\s)

\s 匹配任何 Unicode 空白字符。例如：

[part_2/character_class_range/range_ex8.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/character_class_range/range_ex8.js)

|   | **const** re = */**\s**/*; |
| --- | --- |
|   |  |
|   | re.test(*"5"*); *// → false* |
|   | re.test(*" "*); *// → true* |

正如你将在本书后面看到的，\s 有一个有趣的用法是从字符串中移除重复的空白字符（见第 62 章，[*移除重复空格*](f_0074.xhtml#rcp.removing_dup_whitespaces)）。

#### 非数字字符 (\D)

\D 匹配任何不是数字的字符，等同于 [^\d] 或 [^0-9]：

[part_2/character_class_range/range_ex9.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/character_class_range/range_ex9.js)

|   | **const** re = */**\D**/*; |
| --- | --- |
|   |  |
|   | re.test(*"5"*); *// → false* |
|   | re.test(*"a"*); *// → true* |
|   | re.test(*" "*); *// → true* |
| 取反简写形式 |
| --- |
| ![images/aside-icons/info.png](images/aside-icons/info.png) | \D, \W 和 \S 分别是 \d, \w 和 \s 的取反形式。这意味着它们匹配与正常简写字符类相反的内容。 |

#### 非字字符 (\W)

\W 匹配任何不是字母或数字的字符，等同于 [^\w] 和 [^A-Za-z0-9_]：

[part_2/character_class_range/range_ex10.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/character_class_range/range_ex10.js)

|   | **const** re = */**\W**/*; |
| --- | --- |
|   |  |
|   | re.test(*"5"*); *// → false* |
|   | re.test(*"a"*); *// → false* |
|   | re.test(*" "*); *// → true* |
|   | re.test(*"*"*); *// → true* |

#### 非空格字符 (\S)

\S 匹配除空白字符以外的任何字符。是 [^\s] 的简写：

[part_2/character_class_range/range_ex11.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/character_class_range/range_ex11.js)

|   | **const** re = */**\S**/*; |
| --- | --- |
|   |  |
|   | re.test(*"5"*); *// → true* |
|   | re.test(*"a"*); *// → true* |
|   | re.test(*" "*); *// → false* |
|   | re.test(*"*"*); *// → true* |
| 你可以在哪里使用简写？ |
| --- |
| ![images/aside-icons/tip.png](images/aside-icons/tip.png) | 简写可以出现在方括号内外。例如，\s\d 匹配一个空白字符后跟一个数字字符，而 [\s\d] 匹配一个空白字符或一个数字字符。 |

#### 单字符 (.)

句点 (.) 匹配除换行符外的任何单个字符。例如：

[part_2/character_class_range/range_ex12.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/character_class_range/range_ex12.js)

|   | **const** re = */./*; |
| --- | --- |
|   |  |
|   | re.test(*"5"*); *// → true* |
|   | re.test(*" "*); *// → true* |
|   | re.test(*"*"*); *// → true* |
|   | re.test(*"abc"*); *// → true* |

注意最后一个返回true的测试，测试的是“abc”。这里，句点匹配的是“abc”中的“a”，而不是整个字符串。如果要匹配连续的三个字符，可以使用正则表达式 /.../。另外，你也可以使用 /.{3}/，它利用量词来指定要匹配的标记数量。你将在第29条食谱中学习量词，[*使用量词重复正则表达式的部分*](f_0040.xhtml#rcp.quantifiers)。

当匹配跨越多行的字符时要小心。句点不会匹配换行符，除非你使用特殊标志（参见第42条食谱，[*强制句点匹配换行符的s标志*](f_0053.xhtml#rcp.flag_s)）。

你可以使用字符类来定义一个字符范围进行匹配。这个范围可以使用连字符（-）来指定，而且不限于数字。要匹配一个不在特定范围内的字符，可以在左方括号后立即使用插入符号（^）。为了使用更简洁的语法指定范围，你可以利用预定义的字符类。
