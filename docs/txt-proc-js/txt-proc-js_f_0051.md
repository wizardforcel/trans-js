| 食谱 40 | 使用 d 标志生成匹配的索引 |
| --- | --- |

### 任务

假设你正在构建一个工具，帮助检测 JavaScript 代码中的错误和潜在问题。你需要确保你的工具能够检测到变量和函数中使用了保留字，并警告用户。

理想情况下，你希望将工具编程为准确地定位到代码中保留字被误用的具体部分，而不仅仅是输出行号。因此，如果代码中有类似这样的变量赋值：

|   | **let** **default** = 7; |
| --- | --- |

你希望像这样指示错误：

|   | **let** **default** = 7; |
| --- | --- |
|   | **↑**------ 无效的变量名 |

为了完成这个任务，你需要一个正则表达式，能够提供匹配的起始和结束索引。

### 解决方案

将提供的代码逐行传递给一个查找无效变量/函数名称的函数。使用 `d` 标志来获取名称的起始和结束索引：

[part_2/flag_indices/indices_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/flag_indices/indices_ex1.js)

|   | *// 你想要检查的 JS 代码。* |
| --- | --- |
|   | *// 在生产环境中，你可能会使用 FileReader API* |
|   | *// 或者一个文本框来获取代码。* |
|   | **const** code = *`* |
|   | *let a = 123;* |
|   | *let b = 456;* |
|   | *let default = 7;* |
|   | *`*; |
|   |  |
|   | *// 一小部分 JS 保留字列表。* |
|   | *// 完整的保留字列表可以在这里找到：* |
|   | *// https://mzl.la/3XG92DO* |
|   | **const** reserved = [*"class"*, *"default"*, *"this"*, *"case"*, *"if"*]; |
|   | *// 使用保留字构建正则表达式模式* |
|   | **const** re = **new** RegExp(*`(?:var&#124;let&#124;const&#124;function)\\s+(*${reserved.join(*"&#124;"*)}*)`*, |
|   | *"d"*); |
|   |  |
|   | *// 查找并显示保留字的位置* |
|   | **function** locateReservedWord(line) { |
|   | **const** match = line.match(re); |
|   |  |
|   | *// 如果没有匹配，返回* |
|   | **if** (match === **null**) {**return**;} |
|   |  |
|   | *// 使用解构赋值赋值起始和结束索引。* |
|   | *// indices[0] 保存匹配字符串的索引。* |
|   | *// indices[1] 保存第一个捕获组的索引。* |
|   | **const** [start, end] = match.indices[1]; |
|   |  |
|   | *// 构建错误消息* |
|   | **const** error = |
|   | *" "*.repeat(start) + *// 在箭头前添加空格* |
|   | *"↑"* + |
|   | *"-"*.repeat(end - start - 1) + |
|   | *" 无效的名称（保留字）"*; |
|   |  |
|   | console.log(line); |
|   | console.log(error); |
|   | } |
|   |  |
|   | *// 将代码分割成单独的行，* |
|   | *// 然后发送每一行到 locateReservedWord()* |
|   | code.split(*/**\n**&#124;**\r**&#124;**\r\n**/*).forEach(line => { |
|   | locateReservedWord(line); |
|   | }); |
|   |  |
|   | *// 日志：* |
|   | *// → let default = 7;* |
|   | *// → ↑------ 无效的名称（保留字）* |

现在，您的代码可以准确地指示保留字在变量或函数名中的位置。

| 浏览器兼容性 |
| --- |
| ![images/aside-icons/info.png](images/aside-icons/info.png) | 尽管 d 标志是正则表达式家族中的新成员，但所有现代浏览器都支持它。^([[23]](f_0064.xhtml#FOOTNOTE-23)) 在 Node 环境中，您需要至少版本 16.0.0（发布于 2021-04-20）。为了支持旧版浏览器，您可以使用 NPM 上 regexp-match-indices 包中的 polyfill。^([[24]](f_0064.xhtml#FOOTNOTE-24)) |

### 讨论

hasIndices 标志（d）表示匹配结果应提供关于每个匹配子串的起始和结束位置的附加信息。该信息将存储在一个名为 indices 的属性中。请考虑以下示例：

[part_2/flag_indices/indices_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/flag_indices/indices_ex2.js)

|   | **const** str = *"word1 word2"*; |
| --- | --- |
|   | **const** re = */word/*dg; |
|   |  |
|   | console.log(re.exec(str).indices[0]); *// → [ 0, 4 ]* |
|   | console.log(re.exec(str).indices[0]); *// → [ 6, 10 ]* |

当我们在正则表达式中设置 d 标志时，exec()、match() 和 matchAll() 的结果中将包含一个 indices 属性。在这里，我们使用 exec() 方法，它与 match() 类似，不同之处在于它也在全局模式下提供 indices（请参见附录 2，[*在 JavaScript 中实现正则表达式*](f_0089.xhtml#apx2)）。

这个正则表达式的写法需要使用 RegExp() 构造函数，因为我们正在通过一个保留字数组动态构建模式。在 RegExp() 中的任何反斜杠都必须用另一个反斜杠进行转义。因此，我们以 \\s 的形式编写简写字符类来匹配空白字符，而不是 \s。记住，如果你动态创建的列表中包含反斜杠，你也必须进行转义。

此外，请注意 RegExp() 的第二个参数。RegExp() 构造函数使用不同的方式设置标志：它接受一个可选的第二个参数，包含要设置的标志字母。在这里，我们希望设置 hasIndices 标志，因此传入 d。与第一个参数一样，第二个参数必须是字符串，不要将其包裹在斜杠中。

让我们更详细地分析这个正则表达式：

|   | (?:var&#124;let&#124;const&#124;function)\\s+(${reserved.join("&#124;")}) |
| --- | --- |
|   |  |
|   | ● (?:var&#124;let&#124;const&#124;function) 非捕获组 |
|   | ○ 第一个替代方案：字面匹配字符“var” |
|   | ○ 第二个替代方案：字面匹配字符“let” |
|   | ○ 第三个替代方案：字面匹配字符“const” |
|   | ○ 第四个替代方案：字面匹配字符“function” |
|   | ● \\s 匹配任何空白字符 |
|   | ○ + 匹配前一个标记一次或多次 |
|   | ● (${reserved.join("&#124;")}) 第一个捕获组 |
|   | ○ ${reserved.join("&#124;")} 获取保留字数组并将其连接 |
|   | 带有竖线的项目，结果为 class&#124;default&#124;this&#124;case&#124;if |
|   | ● 标志 |
|   | ○ d 提供关于起始和结束索引的信息 |

利用 hasIndices 标志获取匹配项的起始和结束位置的信息。请记住，在使用 RegExp() 构造函数时，你不能像通常使用正则表达式字面量那样将标志附加到正则表达式模式上。相反，你应该将包含标志的字符串作为构造函数的第二个参数传递。
