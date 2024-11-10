| 配方 53 | 使用 Unicode 属性转义匹配 Unicode 单词边界 |
| --- | --- |

### 任务

假设你要在文档中查找葡萄牙语单词“vã”，它的意思是“去”，而不想匹配包含“vã”的其他单词，如“vão”。为了实现这一目标，你尝试使用单词边界将单词“vã”与其他包含相似字符的单词隔离开来：

[part_2/unicode_property_escapes_p3/upe_p3_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/unicode_property_escapes_p3/upe_p3_ex1.js)

|   | **const** re = */**\b**vã**\b**/*; |
| --- | --- |
|   |  |
|   | *"vão"*.match(re); |
|   | *// → ["vã", index: 0, input: "vão bem", groups: undefined]* |
|   |  |
|   | *"vã bem"*.match(re); |
|   | *// → null* |

但是，你的正则表达式匹配到的结果与预期相反。问题在于，单词边界（\b）将带有重音符号的字符（如“ã”）视为非单词字符。因此，你需要一个不受此限制的替代方案。

### 解决方案

使用 Unicode 属性转义的组合来匹配 Unicode 字符中的单词边界：

[part_2/unicode_property_escapes_p3/upe_p3_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/unicode_property_escapes_p3/upe_p3_ex2.js)

|   | **let** re = */**(?<**=**[^\p**{L}**\p**{M}**\p**{Nd}**\p**{Pc}**]**&#124;^**)**vã**(?=[^\p**{L}**\p**{M}**\p**{Nd}**\p**{Pc}**]**&#124;$**)**/*u; |
| --- | --- |
|   |  |
|   | *"vão"*.match(re); |
|   | *// → null* |
|   |  |
|   | *"vã bem"*.match(re); |
|   | *// → ["vã", index: 0, input: 'vã bem', groups: undefined]* |

成功的结果！现在正则表达式能够正确地匹配葡萄牙语以及其他语言中的单词边界。

### 讨论

在 JavaScript 中处理非英语文本时，一个缺点是正则表达式引擎中的单词边界仅识别 ASCII 表中的字符。结果是，当文本中包含带有重音符号的字符或使用非拉丁字母书写的单词时，\b 无法正确匹配“完整单词”。

在这个例子中，问题的出现是因为字符“ã”被分类为非单词字符，导致“ã”和“o”之间被检测为单词边界。相反，“ã”后跟一个空格字符会形成一个连续的非单词字符字符串，因此没有检测到单词边界。

为了解决这个问题，我们可以在环视中使用一组 Unicode 属性转义：

+   \p{L} 字母类别：匹配任何类型的字母，无论其语言是什么

+   \p{M} 标记类别：匹配一个组合字符，这种字符通常与另一个字符结合使用，例如重音符号、变音符号、包围框等

+   \p{Nd} 十进制数字：匹配任何数字（0 到 9）在任何脚本中，排除表意文字脚本

+   \p{Pc} 连接标点符号：匹配一个标点符号字符，例如下划线

在 JavaScript 中处理非英语文本需要特别注意，以确保准确地搜索和匹配单词。使用标准的单词边界可能会导致带重音符号或非拉丁字母脚本的单词无法完全匹配。幸运的是，通过使用 Unicode 属性转义，我们可以解决这个问题，进行更可靠的非英语文本搜索。

### 总结

文本处理是任何现代应用程序的核心部分。无论你是在开发一个内容密集型网站，还是在构建一个复杂的数据分析工具，使用正则表达式都能显著提升你的开发能力。

在本书的这一部分，你学会了如何在 JavaScript 中使用正则表达式，并利用各种正则表达式方法。你了解了正则表达式的基本构件，如字符类、量词和元字符，以及如何将它们组合起来形成更复杂的模式。

接下来，您将通过解决一系列文本处理问题来加深对正则表达式的理解，这些问题需要使用本部分讨论的标记。正则表达式一开始可能让人感到艰难，但通过实践和耐心，掌握这个工具能够显著提高您的文本处理能力。

#### 脚注

[[23]](f_0051.xhtml#FNPTR-23)

[https://mzl.la/3u78Y6w](https://mzl.la/3u78Y6w)

[[24]](f_0051.xhtml#FNPTR-24)

[https://www.npmjs.com/package/regexp-match-indices](https://www.npmjs.com/package/regexp-match-indices)

[[25]](f_0052.xhtml#FNPTR-25)

[https://developer.mozilla.org/en-US/docs/Web/API/fetch](https://developer.mozilla.org/en-US/docs/Web/API/fetch)

[[26]](f_0053.xhtml#FNPTR-26)

[https://github.com/acornjs/acorn](https://github.com/acornjs/acorn)

[[27]](f_0054.xhtml#FNPTR-27)

[https://en.wikipedia.org/wiki/Emoticons_(Unicode_block)](https://en.wikipedia.org/wiki/Emoticons_(Unicode_block))

[[28]](f_0054.xhtml#FNPTR-28)

[https://mathiasbynens.be/notes/es6-unicode-regex](https://mathiasbynens.be/notes/es6-unicode-regex)

[[29]](f_0060.xhtml#FNPTR-29)

[https://caniuse.com/?search=lookbehind](https://caniuse.com/?search=lookbehind)

[[30]](f_0063.xhtml#FNPTR-30)

[https://util.unicode.org/UnicodeJsps/character.jsp?a=A&B1=Show](https://util.unicode.org/UnicodeJsps/character.jsp?a=A&B1=Show)

[[31]](f_0063.xhtml#FNPTR-31)

[https://unicode.org/reports/tr18/](https://unicode.org/reports/tr18/)

版权 © 2024，The Pragmatic Bookshelf.
