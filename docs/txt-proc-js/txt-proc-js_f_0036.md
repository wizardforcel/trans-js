| 配方 25 | 使用单词边界（\b）仅查找完整单词 |
| --- | --- |

### 任务

假设你想在文档中查找“green”这个单词。你尝试使用 includes() 方法，但它也会匹配其他包含“green”的单词，例如“greenhouse”和“evergreen”：

[part_2/word_boundary/word_boundary_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/word_boundary/word_boundary_ex1.js)

|   | **const** str1 = *"我们必须减少温室气体的排放。"*; |
| --- | --- |
|   | **const** str2 = *"一种常绿植物一年四季都有叶子。"*; |
|   |  |
|   | str1.includes(*"green"*); *// → true* |
|   | str2.includes(*"green"*); *// → true* |

仅仅在“green”周围加空格并不够，因为该单词后面可能跟着逗号，或者出现在换行符的前后，或者位于句子的开头/结尾等情况：

[part_2/word_boundary/word_boundary_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/word_boundary/word_boundary_ex2.js)

|   | **const** str = *"将黄色和蓝色的油漆混合在一起，得到绿色。"*; |
| --- | --- |
|   |  |
|   | str.includes(*" green "*); *// → false* |

你需要一个解决方案，使得只有当“green”是一个独立单词时才匹配它。

### 解决方案

在正则表达式模式中，在“green”前后加上 \b 来排除其他单词：

[part_2/word_boundary/word_boundary_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/word_boundary/word_boundary_ex3.js)

|   | **const** re = */**\b**green**\b**/*; |
| --- | --- |
|   | **const** str1 = *"我们必须减少温室气体的排放。"*; |
|   | **const** str2 = *"一种常绿植物一年四季都有叶子。"*; |
|   | **const** str3 = *"将黄色和蓝色的油漆混合在一起，得到绿色。"*; |
|   |  |
|   | re.test(str1); *// → false* |
|   | re.test(str2); *// → false* |
|   | re.test(str3); *// → true* |

成功了！你只在“green”是一个独立单词时匹配它，而不是当它是其他单词的一部分时。你还能够在单词周围有标点符号的情况下找到“green”。让我们看看\b如何工作以找到完整的单词。

### 讨论

元字符\b匹配的是一个被称为单词边界的位置。简而言之，这个元字符让你只能寻找“完整单词”。只有当单词字符前后没有其他单词字符时，某个位置才被视为单词边界。

因此，\b匹配的是单词的第一个字符之前或最后一个字符之后的位置。单词字符包括a-z、A-Z、0-9和下划线。因此，像空格（green beans）、引号（"green"）、逗号（green,）和句点（green.）这样的符号都被视为单词边界。

| 什么是元字符？ |
| --- |
| ![images/aside-icons/info.png](images/aside-icons/info.png) | 当某些字符在正则表达式中使用时，它们赋予搜索语法特殊的含义。这些字符被称为元字符（或特殊字符），它们允许你执行比仅仅搜索一段文本更为高级的匹配。元字符可以表示如位置、数量或字符类型等概念。 |

需要仅匹配完整单词（如black，但不是blacksmith）是非常常见的，\b非常适合这个用途，但单词边界的使用远比你想象的要复杂一些。让我们更深入地探讨一下如何使用\b。

\bgreen\b不会匹配“_green”或“green4”，因为下划线和数字都是单词字符，并且单词字符之间没有边界：

[part_2/word_boundary/word_boundary_ex4.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/word_boundary/word_boundary_ex4.js)

|   | **const** re = */**\b**green**\b**/*; |
| --- | --- |
|   |  |
|   | re.test(*"_green"*); *// → false* |
|   | re.test(*"green4"*); *// → false* |

连字符则被认为是单词边界。因此，在我们的示例中，green-eyed 将会匹配。我们人类可能会将 green-eyed 视为一个词，但正则表达式并不这么认为：

[part_2/word_boundary/word_boundary_ex5.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/word_boundary/word_boundary_ex5.js)

|   | **const** re = */**\b**green**\b**/*; |
| --- | --- |
|   |  |
|   | re.test(*"green-eyed"*); *// → true* |

同样的情况发生在撇号上：/\bcan\b/ 匹配 “I can’t do it”，即使“can’t”是缩写，并且在英语中是一个词：

[part_2/word_boundary/word_boundary_ex6.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/word_boundary/word_boundary_ex6.js)

|   | **const** re = */**\b**can**\b**/*; |
| --- | --- |
|   |  |
|   | re.test(*"I can't do it"*); *// → true* |

带有重音符号的字符也被视为单词边界（有关解决方法，请参见配方 53，[*匹配 Unicode 单词边界与 Unicode 属性转义*](f_0064.xhtml#rcp.unicode_property_escapes_p3)）：

[part_2/word_boundary/word_boundary_ex7.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/word_boundary/word_boundary_ex7.js)

|   | **const** re = */**\b**Fianc**\b**/*; |
| --- | --- |
|   |  |
|   | re.test(*"Fiancée"*); *// → true* |
|   | re.test(*"Fiancee"*); *// → false* |

你不需要将 \b 配对在单词的两边。你可以只使用一个 \b 来匹配单一的边界：

[part_2/word_boundary/word_boundary_ex8.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/word_boundary/word_boundary_ex8.js)

|   | **const** re1 = */**\b**green/*; |
| --- | --- |
|   | **const** re2 = */green**\b**/*; |
|   |  |
|   | re1.test(*"evergreen"*); *// → false* |
|   | re1.test(*"greenhouse"*); *// → true* |
|   |  |
|   | re2.test(*"evergreen"*); *// → true* |
|   | re2.test(*"greenhouse"*); *// → false* |

注意，当你将 \b 放在搜索字符串的开头（/\bgreen/）时，它只会找到以“green”开头的单词，而当放在结尾（/green\b/）时，它只会找到以“green”结尾的单词。

#### 使用 \B 来匹配非单词边界

\B 匹配任何 \b 不匹配的位置（任何非单词边界），因此我们说 \B 是 \b 的否定形式。在正则表达式中，这是一个常规约定：同一个字母的小写和大写版本互为对立/否定形式。

\B 匹配一个位置，在这个位置，一个字符后面或前面跟着相同类型的字符，比如两个空格字符或两个字母之间。以下是一个示例：

[part_2/word_boundary/word_boundary_ex9.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/word_boundary/word_boundary_ex9.js)

|   | **const** re = */green**\B**/*; |
| --- | --- |
|   |  |
|   | re.test(*"greenhouse"*); *// → true* |
|   | re.test(*"green bay"*); *// → false* |

在“greenhouse”中，“green”后面跟的是相同类型的字符：一个单词字符。因此，测试结果为真。然而，在“green bay”中，“green”后面跟的是一个空格（不同类型的字符），所以结果为假。

| \b 与 RegExp 构造函数 |
| --- |
| ![images/aside-icons/important.png](images/aside-icons/important.png) | 当使用 RegExp 构造函数时，你必须用反斜杠对 \b 元字符进行转义，因为你是在正常字符串中写模式，而不是斜杠包围的字面量。这里不应该使用代码标签。 |

#### 使用 Intl.Segmenter() 替代

还记得 Recipe 19 中的 Intl.Segmenter() 吗？[*使用 Intl.Segmenter() 统计字符串中的单词*](f_0029.xhtml#rcp.wordSegmenter)？如果你正在寻找一个纯 JavaScript 的解决方案，你可以使用 Intl.Segmenter() 来实现相同的效果：

[part_2/word_boundary/word_boundary_ex10.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/word_boundary/word_boundary_ex10.js)

|   | **function** includesWord(str, word) { |
| --- | --- |
|   | **let** s = [...**new** Intl.Segmenter(*"en"*, {granularity: *"word"*}).segment(str)]; |
|   | **return** s.some(value => { |
|   | **return** value.segment === word; |
|   | }); |
|   | } |
|   |  |
|   | includesWord(*"Her flashing green eyes."*, *"green"*); |
|   | *// → true* |
|   |  |
|   | includesWord(*"我们必须减少温室气体排放。 "*, *"绿"*); |
|   | *// → false* |
|   |  |
|   | includesWord(*"绿眼怪物"*, *"绿"*); |
|   | *// → true* |
|   |  |
|   | includesWord(*"我做不到"*, *"能"*); |
|   | *// → false* |

当您将粒度设置为“单词”时，Intl.Segmenter()会在单词边界处分割字符串。然后，您可以使用some()检查结果数组中的元素是否包含您要查找的单词，如果数组中至少有一个元素匹配该单词，some()会返回true。这种方法与正则表达式方法的一个区别是它处理撇号的方式：\b将撇号视为单词分隔符，而Intl.Segmenter()则不会。

另一个区别是，Intl.Segmenter()方法比正则表达式慢，尤其是在处理大量文本时。因此，除非您想避免匹配包含撇号的单词，否则应坚持使用正则表达式。

使用单词边界（\b）来查找字符串中的“完整单词”，但要小心重音字符、连字符和撇号，因为它们被视为单词分隔符。使用单词边界的否定形式（非单词边界 \B）来匹配\b无法匹配的位置。
