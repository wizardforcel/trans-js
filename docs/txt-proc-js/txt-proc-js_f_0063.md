| 食谱 52 | 使用 Unicode 属性转义匹配非 ASCII 单词 |
| --- | --- |

### 任务

假设你想要搜索一个具有特定扩展名的文件并提取文件名。这个任务类似于食谱 31，[*使用捕获组提取匹配值*](f_0042.xhtml#rcp.capturing_group_p2)，你在那里匹配了一个扩展名为 .pdf 的文件。

现在你想要匹配一个包含非 ASCII 字符的文件名。人们保存文件时使用自己语言的文件名并不罕见，但你当前的脚本无法匹配非 ASCII 字母：

[part_2/unicode_property_escapes_p2/upe_p2_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/unicode_property_escapes_p2/upe_p2_ex1.js)

|   | **const** re = */**\b(\w**+**)\.**pdf**\b**/*; |
| --- | --- |

![images/upe_p2_ex1.png](images/upe_p2_ex1.png)

你需要一个能够匹配非 ASCII 单词的解决方案。

### 解决方案

使用 Unicode 属性转义的组合来匹配 Unicode 字符，可以像 \w 匹配 ASCII 字符一样匹配 Unicode 字符：

[part_2/unicode_property_escapes_p2/upe_p2_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/unicode_property_escapes_p2/upe_p2_ex2.js)

|   | **const** re = */**([\p**{Alpha}**\p**{Pc}**\p**{Mark}**\p**{Nd}**\p**{Join_Control}**]**+**)\.**pdf**\b**/*u; |
| --- | --- |

![images/upe_p2_ex2.png](images/upe_p2_ex2.png)

现在你可以匹配任何语言的文件名了！

### 讨论

\w 字符类匹配任何来自基本拉丁字母表的字母数字字符，包括下划线。为了匹配类似范围的 Unicode 字符，我们需要使用多个属性转义：

+   \p{Alpha} 是字母（Alphabetic）的缩写，用于匹配任何具有字母属性的字符

+   \p{Pc} 是连接标点符号（Connector_Punctuation）的缩写，用于匹配连接标点符号，如下划线

+   \p{Mark} 匹配组合符号

+   \p{Nd} 是十进制数字（Decimal_Number）的缩写，用于匹配一个十进制数字

+   \p{Join_Control} 匹配具有控制草书连接和连字功能的格式控制字符

在 Unicode 标准中，每个字符都会分配一组属性和属性值。Unicode 属性转义符使我们能够基于特定属性匹配字符。例如，字母“A”具有一个值为“是”的字母属性，这意味着我们可以使用 \p{Alpha} 或 \p{Alphabetic} 来匹配它。

要查看特定字符的属性，请访问 Unicode 字符数据库，并在搜索栏中输入该字符。^([[30]](f_0064.xhtml#FOOTNOTE-30)) 若要查看支持的属性转义符列表，请参考 Unicode 规范。^([[31]](f_0064.xhtml#FOOTNOTE-31))
