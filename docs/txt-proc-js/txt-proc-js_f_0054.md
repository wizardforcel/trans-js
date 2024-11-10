| 配方 43 | 使用 u 标志启用 Unicode 特性 |
| --- | --- |

### 任务

假设你有一个在线论坛，想要限制用户帖子中的字符只能是单词、数字、下划线、连字符和表情符号。你可以通过字符类 `[-\w]+` 实现前四条规则。回想一下第27条配方，[*匹配多个字符中的一个（使用字符类）*](f_0038.xhtml#rcp.character_class)，`\w` 等价于 `[a-zA-Z0-9_]`，因此你只需要添加连字符和表情符号。

匹配表情符号稍微复杂一些。在 Unicode 中，表情符号是一个包含 80 个 Unicode 表情符号的代码点块。但将所有这些代码点添加到字符类中将非常繁琐。

你需要一种解决方案，能够像定义字符范围一样在字符类中定义表情符号范围。

### 解决方案

将表情符号 Unicode 块中的第一个和最后一个表情符号列出，并在它们之间放置一个连字符以定义一个范围。^([[27]](f_0064.xhtml#FOOTNOTE-27)) 然后，将 `u` 标志附加到模式中，以启用匹配表情符号范围：

[part_2/flag_unicode/unicode_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/flag_unicode/unicode_ex1.js)

|   | *// 匹配单词、数字、下划线、连字符和表情符号* |
| --- | --- |

![images/flags_u_ex1.png](images/flags_u_ex1.png)

你的模式现在能够成功匹配表情符号范围！

### 讨论

尽管这个正则表达式包含了两个连字符，但它们的作用不同。第一个连字符是字面上的匹配连字符，因为它位于字符类的开头，不可能定义一个范围。然而，第二个连字符则位于两个表情符号之间，这告诉正则表达式引擎匹配一个范围：

![images/flags_u_ex4.png](images/flags_u_ex4.png)

如果没有 `u` 标志，这段代码会抛出一个语法错误：

[part_2/flag_unicode/unicode_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/flag_unicode/unicode_ex2.js)

|   | *// 与没有 Unicode 标志的相同模式* |
| --- | --- |

![images/flags_u_ex2.png](images/flags_u_ex2.png)

Unicode 标志的另一个用途是告诉引擎将模式视为 Unicode 代码点的序列，这使得可以将代理对（surrogate pairs）解释为整个字符，而不是两个独立的字符。例如：

[part_2/flag_unicode/unicode_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/flag_unicode/unicode_ex3.js)

|   | **const** str = *"***\***ud846"*; |
| --- | --- |

![images/flags_u_ex3.png](images/flags_u_ex3.png)

这个例子中的汉字由两个代码点组成：\ud846\udf10。如果没有设置 u 标志，正则表达式引擎会错误地将第一个代码对当作匹配项。关于 Unicode 的更多细节，请参阅附录 1，[*什么是 Unicode？*](f_0088.xhtml#apx1)。

关于 u 标志需要记住的一点是，它对不必要使用反斜杠的情况更加严格。如果你转义一个在正则表达式中没有特殊意义的字符，并且启用了 Unicode 模式，系统会抛出错误：

[part_2/flag_unicode/unicode_ex4.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/flag_unicode/unicode_ex4.js)

|   | **const** str = *"cab"*; |
| --- | --- |
|   |  |
|   | */**\c**/*.test(str); |
|   | *// → false* |
|   |  |
|   | */**\c**/*u.test(str); |
|   | *// → SyntaxError: 无效的正则表达式：/\c/：无效的 Unicode 转义* |

该代码中的第二个正则表达式尝试转义“c”，但“c”不是保留字符，结果会导致 SyntaxError（语法错误）。

| Unicode 属性转义 |
| --- |
| ![images/aside-icons/note.png](images/aside-icons/note.png) | Unicode 标志的一个非常有用的功能是启用 Unicode 属性转义，你将在第 51 条食谱中学习到，[*使用 Unicode 属性转义匹配非 ASCII 数字*](f_0062.xhtml#rcp.unicode_property_escapes_p1)。 |
| Nitty-Gritty 细节 |
| --- |
| ![images/aside-icons/info.png](images/aside-icons/info.png) | 关于 u 标志还有更多细节，如果你在处理非 BMP 字符时可能会用到。查看 Mathias Bynens 关于 Unicode 感知正则表达式的详细文章，了解更多内容。^([[28]](f_0064.xhtml#FOOTNOTE-28)) |

Unicode 标志启用了各种 ES2015 Unicode 特性。你可以使用它来定义一系列天文字符（非 BMP 字符），如表情符号，解释代理对为完整字符，解释 Unicode 属性转义等。
