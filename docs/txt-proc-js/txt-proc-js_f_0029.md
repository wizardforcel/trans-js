| 配方 19 | 使用 Intl.Segmenter() 统计字符串中的单词 |
| --- | --- |

### 任务

假设您有一个博客，允许用户提交文章。您要求每篇文章的字数必须至少为 500 字。您希望创建一个函数，向用户反馈其文章的字数。为此，您的应用需要确定给定文本字符串中的单词数。

解决这个问题的一种粗略方法是通过空格分割文本字符串并计算得到的段落。然而，当单词之间有多个连续空格，或文章使用不以空格分隔单词的语言（如韩语或日语）时，这种方法可能无法正确工作。

您需要一个能够准确计算文本中单词数的解决方案，不论所使用的语言是什么。

### 解决方案

使用 `Intl.Segmenter()` 构造函数，并将粒度选项设置为单词：

[part_1/counting_words/word_segmenter_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/counting_words/word_segmenter_ex1.js)

|   | **const** str = *"White, red, and blue."*; |
| --- | --- |
|   |  |
|   | **function** countWords(str, lang) { |
|   | **const** segments = [...**new** Intl.Segmenter(lang, {granularity: *"word"*}) |
|   | .segment(str)]; |
|   | **return** segments.filter(item => item.isWordLike === **true**).length; |
|   | } |
|   |  |
|   | countWords(str, *"en"*); *// → 4* |

成功！countWords() 函数根据指定的语言（lang）统计 str 中的单词数。

| 浏览器兼容性 |
| --- |
| ![images/aside-icons/warning.png](images/aside-icons/warning.png) | 截至本文撰写时，Firefox 尚未实现 Intl.Segmenter()。^([[19]](f_0032.xhtml#FOOTNOTE-19)) 在浏览器支持更加稳定之前，您可以在服务器端（Node 16 或更高版本）运行 Intl.Segmenter()。 |

### 讨论

在之前的示例中，我们使用了`Intl.Segmenter()`的默认实现，它在字素集群（用户感知字符）边界处拆分字符串。这次，我们将粒度设置为单词，以便在单词边界处进行拆分。

`Intl.Segmenter()`的第一个参数决定了地区设置，它必须是一个BCP 47语言标签。^([[20]](f_0032.xhtml#FOOTNOTE-20)) 在这种情况下，我们想要拆分英文单词，所以我们传递“en”。一旦获得字符串的片段，我们应该过滤掉那些不是单词的片段。幸运的是，API通过提供`isWordLike`属性使这变得非常简单。该过滤器有效地移除了所有非单词片段（如标点符号或数字）。

最后，我们返回过滤后的片段数组的长度，它表示原始字符串中单词片段的总数。现在，如果我们想要统计另一种语言的单词，我们只需将相应的语言标签传递给`countWords()`函数。例如，下面的例子统计了日语中的单词数：

[part_1/counting_words/word_segmenter_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/counting_words/word_segmenter_ex2.js)

|   | **const** str = *"アジア・東アジアの中でも東方にあります"*; |
| --- | --- |
|   |  |
|   | **function** countWords(str, lang) { |
|   | **const** segments = [...**new** Intl.Segmenter(lang, {granularity: *"word"*}) |
|   | .segment(str)]; |
|   | **return** segments.filter(item => item.isWordLike === **true**).length; |
|   | } |
|   |  |
|   | countWords(str, *"jp"*); *// → 8* |

尽管日语中单词之间没有空格，函数仍然能够区分单词边界。

如果你在线搜索一个JavaScript解决方案来统计单词，你肯定会看到类似这样的代码：

|   | **return** str.split(*" "*).length; |
| --- | --- |

这段代码返回一个由单个空格字符拆分的单词数组，并计算其长度。但是，如果你的字符串中有双空格或尾随空格，结果会是错误的：

|   | **常量** str = *"白色，红色，和蓝色。 "*; |
| --- | --- |
|   | str.split(*" "*).length; *// → 5* |

当然，你可以通过如下方式过滤数组来解决这个问题：

|   | **常量** str = *"白色，红色，和蓝色。 "*; |
| --- | --- |
|   |  |
|   | **函数** countWords(str) { |
|   | **返回** str |
|   | .split(*" "*) |
|   | .filter(a => {**返回** a != *""*}) |
|   | .length; |
|   | } |
|   |  |
|   | countWords(str); *// → 4* |

但这个解决方案仅适用于在单词之间使用空格的语言。使用 `Intl.Segmenter()` 的优点在于它能够在不同语言中检测单词边界。
