| 配方 36 | 使用函数作为替换模式 |
| --- | --- |

### 任务

假设你的任务是改进一个在线房地产市场，该市场以平方英尺列出物业规格。你需要编写一段代码，查找平方英尺的数值，并提供一个括号中的平方米版本，以便国际买家能轻松理解。

### 解决方案

从创建一个将平方英尺值转换为平方米（m2）的函数开始：

|   | function convertToM2(sqft) { |
| --- | --- |
|   |  |
|   | // 移除非数字字符 |
|   | sqft = sqft.replace(/\D/g, ""); |
|   |  |
|   | // 将平方英尺转换为平方米 |
|   | const m2 = sqft * 0.0929; |
|   |  |
|   | // 四舍五入到两位小数并返回 |
|   | return m2.toFixed(2); |
|   | } |

现在，你需要一个接收字符串作为输入并扫描其中包含数字和单位（如“sqft”，“sq. ft.”或“sq ft.”）的函数。一旦找到匹配项，你希望调用 convertToM2() 函数将值转换为平方米，然后将转换后的结果附加到原始匹配项后面。

这时，使用函数作为替换参数就派上用场了：

|   | function appendM2ToSqft(str) { |
| --- | --- |
|   | return str.replace(/\d+,?\d+\s(sqft&#124;sq\.?\sft)/ig, (match) => { |
|   | return `${match} (${convertToM2(match)} m2)`; |
|   | }); |
|   | } |

下面是最终代码的样子：

[part_2/replacement_fn/replacement_fn_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/replacement_fn/replacement_fn_ex1.js)

|   | **const** str = *"3 Beds, 2.5 baths, 1,850 Sq. Ft"*; |
| --- | --- |
|   |  |
|   | *// 将平方英尺转换为平方米* |
|   | **function** convertToM2(sqft) { |
|   |  |
|   | *// 移除非数字字符* |
|   | sqft = sqft.replace(*/**\D**/g*, *""*); |
|   |  |
|   | *// 将平方英尺转换为平方米* |
|   | **const** m2 = sqft * 0.0929; |
|   |  |
|   | *// 四舍五入到两位小数并返回结果* |
|   | **return** m2.toFixed(2); |
|   | } |
|   |  |
|   | *// 匹配字符串中的平方英尺，并将其转换为平方米，* |
|   | *// 将结果括在括号中，并将其附加到sqft* |
|   | **function** appendM2ToSqft(str) { |
|   | **return** str.replace(*/**\d**+,**?\d**+**\s(**sqft&#124;sq**\.?\s**ft**)**/ig*, (match) => { |
|   | **return** *`*${match} *(*${convertToM2(match)} *m2)`*; |
|   | }); |
|   | } |
|   |  |
|   | appendM2ToSqft(str); |
|   | *// → "3 Beds, 2.5 baths, 1,850 Sq. Ft (171.86 m2)"* |

使用这段代码，你可以列出房产的面积，既包括平方英尺，也包括平方米。

### 讨论

让我们从检查正则表达式模式开始：

|   | /\d+,?\d+\s(sqft&#124;sq\.?\sft)/ig |
| --- | --- |
|   |  |
|   | ● \d 匹配数字 |
|   | ○ + 匹配前一个符号，匹配次数为一次或无限次 |
|   | ● , 字面匹配字符"," |
|   | ○ ? 匹配前一个符号零次或一次 |
|   | ● \d 匹配数字 |
|   | ○ + 匹配前一个符号，匹配次数为一次或无限次 |
|   | ● \s 匹配任意空白字符 |
|   | ● (sqft&#124;sq.? ft) 第一个捕获组 |
|   | ○ sqft 第一个备选项 |
|   | ○ sqft 字面匹配字符"sqft" |
|   | ○ sq\.?\sft 第二个备选项 |
|   | ○ sq 字面匹配字符"sq" |
|   | ○ \. 字面匹配句号 |
|   | ○ ? 匹配前一个符号零次或一次 |
|   | ○ \s 匹配任意空白字符 |
|   | ○ ft 字面匹配字符"ft" |
|   | ● 标志 |
|   | ○ i 启用不区分大小写的匹配 |
|   | ○ g 启用全局匹配，表示我们要查找所有匹配项 |
|   | 匹配，而不是在第一次匹配后停止 |

replace() 方法接受字符串或函数作为替换参数。如果使用函数，它将在每次匹配时执行，并且其输出将成为替换文本。

替换函数具有以下语法：

[part_2/replacement_fn/replacement_fn_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/replacement_fn/replacement_fn_ex2.js)

|   | **function** replacer(match, p1, p2, */* …, */* pN, offset, string, groups) { |
| --- | --- |
|   | **return** replacement; |
|   | } |

第一个参数包含匹配的字符串（类似于$&）。如果存在捕获组，它们将在第一个参数后面提供（p1, p2, /* …, */ pN）。

下一个参数提供匹配字符串的偏移量。例如，如果你有字符串“Hello”和搜索模式“ll”，偏移量将是3。还有一个字符串参数，包含整个提供的字符串。

最后，如果你的模式中至少有一个命名捕获组，则groups参数将可用。在这个示例中，我们只使用第一个参数，因此省略了其他参数。

在replacer函数内部，我们使用模板字面量来获取匹配项的值，并将其传递给convertToM2()函数。convertToM2()首先通过用空字符串替换非数字字符来去除字符串中的非数字字符。然后，它执行转换并返回结果。最终的输出是一个包含平方米值的字符串，值被括号括起来并附加到原始匹配字符串后面。

当你需要在替换字符串中执行计算或处理匹配值时，可以利用替换函数。
