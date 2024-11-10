| 配方 51 | 使用 Unicode 属性转义匹配非 ASCII 数字 |
| --- | --- |

### 任务

假设你想匹配一个使用不同数字系统的语言中的数字，例如波斯语或越南语。还记得配方 29， [*使用量词重复正则表达式的一部分*](f_0040.xhtml#rcp.quantifiers)，当时你通过正则表达式验证了一个 PIN 码吗？

这次你想允许用户使用自己语言中的数字来创建 PIN 码。但问题是，匹配数字的字符类（\d）只匹配 ASCII 数字：

[part_2/unicode_property_escapes_p1/upe_p1_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/unicode_property_escapes_p1/upe_p1_ex1.js)

|   | **const** re = */^**\d{4,6}**$/*; |
| --- | --- |

![images/upe_p1_ex1.png](images/upe_p1_ex1.png)

即使设置 Unicode 标志也没有帮助：

[part_2/unicode_property_escapes_p1/upe_p1_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/unicode_property_escapes_p1/upe_p1_ex2.js)

|   | **const** re = */^**\d{4,6}**$/*u; |
| --- | --- |

![images/upe_p1_ex2.png](images/upe_p1_ex2.png)

你需要一个解决方案，允许你验证任何语言中的数字。

### 解决方案

使用 \p{Number} 形式的 Unicode 属性转义：

[part_2/unicode_property_escapes_p1/upe_p1_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/unicode_property_escapes_p1/upe_p1_ex3.js)

|   | **const** re = */^**\p**{Number}**{4,6}**$/*u; |
| --- | --- |

![images/upe_p1_ex3.png](images/upe_p1_ex3.png)

成功！你已经匹配了三种不同语言的数字。

### 讨论

Unicode 标准中的符号具有各种属性和值。通过 Unicode 属性转义，正则表达式可以根据字符的 Unicode 属性进行匹配。

在这个配方中，我们使用 \p{Number} 来匹配数字类别中的每个符号，包括罗马数字和被归类为兼容等价的数字：

[part_2/unicode_property_escapes_p1/upe_p1_ex4.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/unicode_property_escapes_p1/upe_p1_ex4.js)

|   | **const** re = */^**\p**{Number}**{4,6}**$/*u; |
| --- | --- |

![images/upe_p1_ex4.png](images/upe_p1_ex4.png)

如果你想排除非十进制数字，可以改用 \p{Decimal_Number}：

[part_2/unicode_property_escapes_p1/upe_p1_ex5.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/unicode_property_escapes_p1/upe_p1_ex5.js)

|   | **const** re = */**\p**{Decimal_Number}/*u; |
| --- | --- |

![images/upe_p1_ex5.png](images/upe_p1_ex5.png)

请记住，只有在设置了 u 标志时，才能使用 Unicode 属性转义。如果没有 u 标志，则模式 \p 是字母 p 的冗余转义序列。这是有意设计的，以便现有的模式（可能使用 \p{ ... }）在引入 Unicode 属性转义时不会破坏语言的兼容性。

| 否定的 Unicode 属性转义 |
| --- |
| ![images/aside-icons/note.png](images/aside-icons/note.png) | Unicode 属性转义也有一个否定版本，通过 \P{ ... } 来表示，它可以让你匹配与正常匹配结果相反的内容。例如，如果你想匹配不包含数字的字符串，可以写：/^\P{Number}+$/u |

在这个例子中，我们使用了 \p{Number} 来匹配数字类别中的符号，但你也可以匹配其他类型的符号。接下来的示例将展示如何利用 Unicode 属性转义来匹配单词字符。
