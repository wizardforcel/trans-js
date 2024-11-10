| 食谱 71 | 高亮显示包含特定单词的句子 |
| --- | --- |

### 任务

假设你想在程序中添加一个搜索功能，用于高亮显示文本中包含特定单词的所有句子。例如，你正在将一本翻译书与原文进行对比，原文中使用了一个多义词。你需要查看的不仅仅是这个单词本身，还有它所在的上下文，以帮助检查是否使用了正确的翻译。

虽然使用正则表达式查找单词相对简单，但识别包含该单词的句子要稍微复杂一些。要高亮显示包含指定单词的句子，你需要编写一个能够区分不同句子的模式。

### 解决方案

首先编写JavaScript组件，其中包括两个主要功能：highlight()和unhighlight()。highlight()函数获取HTML输入框中输入的搜索值，并应用一个正则表达式，识别包含搜索词的句子。通过将匹配的句子包裹在<mark></mark>标签中，你可以实现目标：

[part_3/highlighting_sentences/highlight_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_3/highlighting_sentences/highlight_ex1.js)

| 1:  | **const** el = document.querySelector(*"#string"*); |
| --- | --- |
| -  |  |
| -  | **function** highlight() { |
| -  |  |
| 5:  | *// 获取#input的值* |
| -  | **const** keyword = document.querySelector(*"#input"*).value; |
| -  |  |
| -  | *// 如果输入为空，不执行函数的其余部分* |
| -  | **如果**(keyword === *""*) { |
| 10:  | **return**; |
| -  | } |
| -  |  |
| -  | *// 从文本中移除任何现有的高亮显示* |
| -  | unhighlight(); |
| 15:  |  |
| -  | *// 构造一个正则表达式* |
| -  | **const** re = **new** RegExp(*`([^.!?]*\\b*${keyword}*\\b[^.!?]*.?)`*, *"gi"*); |
| -  |  |
| -  | *// 将每个句子用一对<mark></mark>标签包裹* |
| 20:  | el.innerHTML = el.innerHTML.replace(re,*"<mark>$1</mark>"*); |
| -  | } |
| -  |  |
| -  | **function** unhighlight() { |
| -  |  |
| 25:  | *// 构建一个正则表达式，用于匹配 <mark> 和 </mark> 标签* |
| -  | **const** re = */<**\/?**mark>/g*; |
| -  |  |
| -  | *// 通过将每个标签替换为空字符串来移除标签* |
| -  | el.innerHTML = el.innerHTML.replace(re, *""*); |
| 30:  | } |
| -  |  |
| -  | document.querySelector(*"#highlight"*).addEventListener(*"click"*, highlight); |
| -  | document.querySelector(*"#unhighlight"*).addEventListener(*"click"*, unhighlight); |

现在，创建两个 HTML 按钮：一个用于启动高亮显示，另一个用于反转效果。你还需要一个输入字段来输入搜索关键词：

|   | <button id=*"highlight"*>高亮显示全部<*/button***>** |
| --- | --- |
|   | <button id=*"unhighlight"*>取消高亮<*/button***>** |
|   | <input id=*"input"* type=*"text"* value=*"crocodiles"*> |

输入元素的默认值是“鳄鱼”。如果你不希望页面加载时输入框中显示任何文本，可以删除值属性。为了简单起见，我们将要搜索的文本限制为几句话：

[part_3/highlighting_sentences/highlight_ex1.xhtml](http://media.pragprog.com/titles/fkjavascript/code/part_3/highlighting_sentences/highlight_ex1.xhtml)

|   | *<!doctype html>* |
| --- | --- |
|   | <html lang=*"en-us"*> |
|   | <head> |
|   | <meta charset=*"utf-8"*> |
|   | <meta name=*"viewport"* content=*"width=device-width, initial-scale=1"*> |
|   | <script src=*"highlight_ex1.js"* defer></script> |
|   | </head> |
|   | <body> |
|   | <p id=*"string"*> |
|   | 鳄鱼就像巨大的蜥蜴，有着严重的态度问题。它们是 |
|   | 就像动物王国中的暴躁老头，永远皱着眉头和 |
|   | 发出类似胃部不适的咕噜声。但尽管它们看起来 |
|   | 尽管鳄鱼给人一种威严的印象，但它们也有柔软的一面。只要试着和它们玩玩 |
|   | 给它们放一些平滑的爵士乐，或者给它们端上一盘新鲜出炉的饼干 |
|   | —它们会变得听从你指挥。总的来说，鳄鱼其实就是 |
|   | 被误解的生物，需要一点爱和一个好的脊椎按摩师。 |
|   | </p> |
|   |  |
|   | <button id=*"highlight"*>高亮全部</button> |
|   | <button id=*"unhighlight"*>取消高亮</button> |
|   | <input id=*"input"* type=*"text"* value=*"crocodiles"*> |
|   | </body> |
|   |  |
|   | </html> |

太棒了！现在代码能够高亮显示文本中包含特定词汇的每个句子。

### 讨论

在JavaScript代码中，我们定义了两个函数和两个事件监听器。第一个函数`highlight()`会在用户点击“highlight”按钮时执行。在函数内部，我们首先获取用户输入的值，并将其存储在一个名为`keyword`的变量中。如果输入为空，我们会终止函数并不做任何操作。如果输入不为空，我们调用`unhighlight()`来移除HTML元素中现有的高亮。

接下来，我们创建一个正则表达式模式，用于匹配包含关键字的句子。我们使用否定字符类[^.!?]来匹配一个不是句点、感叹号或问号的单个字符。这使我们能够区分一个句子与另一个句子。如果你希望该模式识别以其他标点符号结尾的句子，例如冒号，你可以将它们包括在字符类中。

请注意第17行，我们在这里创建了一个RegExp对象实例，而不是使用正则表达式字面量。这一点至关重要，因为我们希望动态地将HTML输入框中的文本插入到正则表达式模式中。我们还需要使用反引号来限定模式，而不是双引号或单引号。如果没有反引号，${keyword}占位符将无法按预期工作。

请注意单词边界（\b）前面有一个反斜杠。因为我们在正则表达式对象中使用了单词边界，所以需要用反斜杠对其进行转义。

以下是正则表达式引擎如何理解该模式：

|   | ([^.!?]*\\b${keyword}\\b[^.!?]*.?) |
| --- | --- |
|   |  |
|   | ● ([^.!?]*\\b${keyword}\\b[^.!?]*.?) 第一个捕获组 |
|   | ○ [^.!?] 匹配不是.、! 或 ? 的任何字符 |
|   | ○ * 匹配前面项的零个或多个序列 |
|   | ○ \\b 表示一个单词边界 |
|   | ○ ${keyword} 将关键字常量的值插入到模式中 |
|   | ○ \\b 表示一个单词边界 |
|   | ○ [^.!?] 匹配不是.、! 或 ? 的任何字符 |
|   | ○ * 匹配前面项的零个或多个序列 |
|   | ○ . 匹配任何非换行符的字符 |
|   | ○ ? 匹配前面项的零次或一次出现 |
|   | ● 标志 |
|   | ○ g 告诉正则表达式引擎匹配所有出现的项，而不是停止 |
|   | 在第一次匹配之后 |
|   | ○ i 使搜索不区分大小写 |

在函数的末尾，我们使用replace()方法将所有匹配模式的结果替换为被<mark></mark>标签包围的匹配字符串。在HTML中，有多种方式来标示具有重要意义的文本。在这个例子中，我们选择了<mark>元素，它指示网页浏览器通过将文本高亮显示为黄色来强调包围其中的文本。

第二个函数`unhighlight()`是在用户点击“取消高亮”按钮时调用的。它仅仅创建一个正则表达式模式，用来匹配 HTML 中的任何<mark>或</mark>标签，然后使用replace()方法移除这些标签。代码的最后两行为“高亮”和“取消高亮”按钮添加了相应的事件监听器。当每个按钮被点击时，相应的函数将被执行。

在使用用户提交的输入进行正则表达式处理时，保持谨慎非常重要。如果你没有验证输入，程序可能会受到一种叫做ReDoS的潜在攻击。要了解如何保护你的应用免受此类攻击，请参阅配方66，[*在正则表达式中使用字符串的转义*](f_0078.xhtml#rcp.escaping_metacharacters)。
