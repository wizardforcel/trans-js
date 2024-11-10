| 食谱 38 | 使用问号创建懒量词 |
| --- | --- |

### 任务

假设你的任务是编写一个脚本，通过移除所有注释来减小 HTML 文件的大小。HTML 注释的语法是 `<!-- 注释内容 -->`。所以，为了完成这个任务，你可能会认为只需要移除注释语法中的开头和结尾的标记，以及它们之间的字符：

[part_2/lazy_quantifiers/lazy_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/lazy_quantifiers/lazy_ex1.js)

|   | **const** re = */<!--.*-->/*; |
| --- | --- |
|   | **const** str = *"HTML 注释: <!-- 我是注释 -->"*; |
|   |  |
|   | str.replace(re, *""*); *// → "HTML 注释: "* |

在这里，句点（.）匹配任何字符（除了换行符），量词 * 告诉引擎此操作可以执行零次或多次。这个模式适用于单行注释。那么跨越多行的注释该如何处理呢？

由于句点（.）无法匹配换行符，正则表达式会失败。一个常见的解决方法是使用字符类，例如 [\d\D]，代替句点。`\d` 匹配任何数字字符，`\D` 匹配其他所有字符。将它们结合在一起，可以匹配任何字符：

[part_2/lazy_quantifiers/lazy_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/lazy_quantifiers/lazy_ex2.js)

|   | **const** re = */<!--**[\d\D]***-->/*; |
| --- | --- |
|   | **const** str = *`HTML 注释: <!--* |
|   | *我是注释* |
|   | *-->`*; |
|   |  |
|   | str.replace(re, *""*); *// → "HTML 注释: "* |

但是你的代码应该能够删除所有注释，而不仅仅是一个。所以，在正则表达式的末尾添加一个 g 标志：

[part_2/lazy_quantifiers/lazy_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/lazy_quantifiers/lazy_ex3.js)

|   | **const** re = */<!--**[\d\D]***-->/g*; |
| --- | --- |
|   | **const** str = *`HTML 注释: <!-- 我是注释 -->* |
|   | *另一个注释: <!--* |
|   | *我是注释* |
|   | *-->`*; |
|   |  |
|   | str.replace(re, *""*); *// → "HTML 注释: "* |

g 标志告诉正则表达式引擎在整个字符串中查找所有匹配项，而不是在找到第一个匹配项后停止。

现在你有了另一个问题！这个模式匹配的是第一个注释的开括号以及其后所有内容，直到最后一个注释的闭括号。原因是量词——在这种情况下是*贪婪的*！它们尽可能多地匹配前面的标记，这正是你在完成这个任务时不想要的行为。

你需要找到一种方法来改变量词的行为。

### 解决方案

通过在量词后面加上问号，使*量词变得惰性*：

[part_2/lazy_quantifiers/lazy_ex4.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/lazy_quantifiers/lazy_ex4.js)

|   | **const** re = */<!--**[\d\D]*****?**-->/g*; |
| --- | --- |
|   | **const** str = *`HTML 注释: <!-- 我是一个注释 -->* |
|   | *另一个注释: <!--* |
|   | *我是一个注释* |
|   | *-->`*; |
|   |  |
|   | str.replace(re, *""*); |
|   | *// → "HTML 注释: "* |
|   | *// 另一个注释: "* |

现在你的正则表达式已经能够准确匹配每个注释。

### 讨论

正如你在第29个食谱中学到的，[*使用量词重复正则表达式的一部分*](f_0040.xhtml#rcp.quantifiers)，+ 量词允许你匹配前面的标记一次或多次。因此，模式 \w+ 匹配一个或多个单词字符。

但是在像“str”这样的字符串中，\w+ 应该匹配“s”还是“str”？正则引擎如何决定匹配“一个”字符还是“多个”字符？量词默认是贪婪的，会尽可能多地匹配前面的标记。问号强制量词采取相反的方式（惰性匹配），尽可能少地匹配。对比一下：

[part_2/lazy_quantifiers/lazy_ex5.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/lazy_quantifiers/lazy_ex5.js)

|   | **const** str = *"str"*; |
| --- | --- |
|   |  |
|   | str.match(*/**\w**+**?**/*)[0]; *// → "s"* |
|   | str.match(*/**\w**+/*)[0]; *// → "str"* |

这个模式 [\d\D]*? 在这个例子中匹配零次或多次任何字符（包括数字和非数字字符），并尽量匹配最少的字符。结果是匹配到第一个 --> 而不是最后一个。

| 懒惰的别名 |
| --- |
| ![images/aside-icons/tip.png](images/aside-icons/tip.png) | 懒惰量词也称为非贪婪量词或不情愿量词。 |
| 所有权量词 |
| --- |
| ![images/aside-icons/info.png](images/aside-icons/info.png) | JavaScript 不支持所有权量词。所有权量词类似于贪婪量词，但在某些情况下提供更好的性能。 |

请记住，在量词后面立即使用问号（包括 *、+、? 或 {}）会使该量词变为懒惰量词。
