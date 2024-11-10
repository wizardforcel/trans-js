| 配方 8 | 使用 replaceAll() 将 HTML 标记转换为 HTML 实体 |
| --- | --- |

### 任务

假设你想在你的网站上发布包含 HTML 标记的编程教程。但你遇到一个问题，浏览器会解释你示例中的 HTML 标签，而不是显示它们。这是因为浏览器认为你使用这些标签来构建网页。

你需要以一种方式表示这些标记，以防止浏览器对其进行解析。

### 解决方案

使用 replaceAll() 方法将 HTML 标签的组件替换为实体：

[part_1/converting_html_to_entities/entities_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/converting_html_to_entities/entities_ex1.js)

|   | **function** escapeHTML(str) { |
| --- | --- |
|   | **return** str |
|   | .replaceAll(*'&'*, *'&amp;'*) |
|   | .replaceAll(*'<'*, *'&lt;'*) |
|   | .replaceAll(*'>'*, *'&gt;'*) |
|   | .replaceAll(*'"'*, *'&quot;'*) |
|   | .replaceAll(*"'"*, *'&apos;'*); |
|   | } |
|   |  |
|   | escapeHTML(*'<a href="test.htm">foo</a>'*); |
|   | *// → "&lt;a href=&quot;test.htm&quot;&gt;foo&lt;/a&gt;"* |

replaceAll() 方法允许你替换字符串中所有匹配的模式。每次调用时，它都会返回一个新的字符串，因此你可以链式调用多个 replaceAll() 方法，在一个语句中替换多个模式。

### 讨论

通过使用 HTML 实体，我们可以显示某些字符，否则这些字符会被浏览器解析为 HTML 代码。下表显示了字符及其对应的 HTML 实体：

| 字符 | 实体 |
| --- | --- |
| & | &amp; |
| < | &lt; |
| > | &gt; |
| " | &quot; |
| ’ | &apos; |

请记住，HTML 实体是区分大小写的，所以 &amp; 和 &AMP; 不是同一个实体。

HTML 实体有两种类型：命名实体和数字实体。命名实体由一串字母组成，字母之间用与符号（&）和分号（;）包围。而数字实体则由与符号（&）开头，后跟井号（#），再接十进制或十六进制代码，并以分号（;）结束。

这是上面的表格，将命名实体转换为相应的数字实体：

| 字符 | 实体 |
| --- | --- |
| & | &#38; |
| < | &#60; |
| > | &#62; |
| " | &#34; |
| ’ | &#39; |

你可以使用命名实体和数字实体在 HTML 文档中显示特殊字符。但通常优先使用命名实体，因为它们更具可读性，也更容易记住。

除了显示具有特殊意义的字符，HTML 实体还可以用于显示那些在标准键盘上难以输入的字符，例如外语字符、数学符号或表情符号。通过使用 HTML 实体，我们可以确保这些字符在网页上正确显示。
