| 配方4 | 使用slice()从文本中提取列表 |
| --- | --- |

### 任务

假设你经营一家在线商店，销售成千上万种不同的衣物。你的任务是通过颜色让商品可以搜索。问题是每个产品的可用颜色都以一句话形式列出在产品描述中。你需要一种方法来编程提取这些颜色，以便建立一个可搜索的数据库。

所以如果你有这样的产品描述：

|   | 这些防水越野跑鞋帮助你在最不可预见的天气条件下保持干爽。 |
| --- | --- |
|   | 防水越野跑鞋帮助你保持干爽。提供四种新颜色。 |
|   | 颜色：天鹅绒棕色，黑色，金色苔藓，中蓝色。 |

你想提取这些颜色并将其存储在像这样的数组中：

|   | [*"天鹅绒棕色"*, *"黑色"*, *"金色苔藓"*, *"中蓝色"*] |
| --- | --- |

你想提取的列表可能还有不同的变化。它可能在项之间使用斜杠(/)而不是逗号。或者它可能包含一些额外的词汇，如“和”、“或”、“等等”，这些词你不希望出现在数组中。

在这个方法中，我们首先构建一个提取简单列表的函数，然后增强该函数以处理更复杂的列表。

### 解决方案

这个方法包含两个步骤：首先，找到包含颜色列表的句子，其次，提取每个颜色并将其存储在一个数组中。你可以使用indexOf()方法执行第一步。颜色列表出现在冒号(:)后面。通过indexOf()定位它，并将结果索引存储在一个常量中。接下来，找到紧随冒号后的第一个句号，并将其索引存储在另一个常量中：

|   | **const** str = *`即使在最不可预见的天气条件下，也能让你信心满满` |
| --- | --- |
|   | *使用这些防水越野跑鞋帮助你保持干爽。可用的* |
|   | *以四种新颜色提供：天鹅绒棕色，黑色，金色苔藓，中蓝色。`*; |
|   |  |
|   | **const** start = str.indexOf(*":"*); |
|   | **const** end = str.indexOf(*"."*, start); |

现在，你有两个索引，分别标记了列表在字符串中的开始和结束位置。将它们传递给slice()方法来提取列表：

|   | **const** list = str.slice(start + 2, end); |
| --- | --- |
|   | *// "Velvet Brown, Black, Golden Moss, Medium Blue"* |

你传递给slice()的方法参数指定了字符串的起始和结束索引。为了偏移字符串开头的冒号和空格，将起始索引增加2。结束索引告诉slice()提取到该索引位置，但不包括该位置，因此不需要从结束索引中减去任何值。

接下来是第二步，你需要将逗号分隔的列表转换为一个数组。JavaScript中有几种方法可以实现这一点。较长的方式是通过循环查找逗号，并将每个项添加到数组中。更直接的方法是使用split()方法。通过split()，你可以定义字符串中每个分隔的位置，并迅速得到一个项的数组：

|   | **const** colors = list.split(*", "*); |
| --- | --- |
|   |  |
|   | console.log(colors); |
|   | *// → [ "Velvet Brown", "Black", "Golden Moss", "Medium Blue" ]* |

在这段代码中，你告诉split()使用逗号后跟空格作为分隔符。结果是一个没有额外空格或逗号的颜色数组，避免了不必要的麻烦。

这是将代码组织成一个函数的最终版本，这样你就可以重用它：

[part_1/extracting_lists/slice_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/extracting_lists/slice_ex1.js)

|   | **const** str = *`即使在最无法预见的天气条件下也能保持信心`* |
| --- | --- |
|   | *这款防水越野跑鞋帮助你保持干爽。提供* |
|   | *以四种新颜色：Velvet Brown, Black, Golden Moss, Medium Blue.`*; |
|   |  |
|   | **function** extractList(str) { |
|   | **const** start = str.indexOf(*":"*); |
|   | **const** end = str.indexOf(*"."*, start); |
|   | **const** list = str.slice(start + 2, end); |
|   |  |
|   | **return** list.split(*", "*); |
|   | } |
|   |  |
|   | extractList(str); |
|   | *// → [ "天鹅绒棕", "黑色", "金色苔藓", "中蓝色" ]* |

### 讨论

如果你想提取的列表中有额外的词语，如“和”，“或”，“等等”，或者使用斜杠（/）而不是逗号，那么你需要一个更高级的功能。你可能不会在某个产品的可选颜色列表中看到“等等”，但我们在这里包括它，以便在其他类型的列表中需要时可以将其移除。

请看这个例子：

[part_1/extracting_lists/slice_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/extracting_lists/slice_ex2.js)

|   | **function** extractList(str) { |
| --- | --- |
|   | **const** start = str.indexOf(*":"*); |
|   | **const** end = str.indexOf(*"."*, start); |
|   | **const** list = str.slice(start + 2, end); |
|   |  |
|   | **return** list.split(*", "*); |
|   | } |
|   |  |
|   | extractList(*"可提供三种颜色：红色，黑色和蓝色。"*); |
|   | *// → [ "红色", "黑色", "和 蓝色" ]* |
|   |  |
|   | extractList(*"可用颜色：红色/黑色/蓝色。"*); |
|   | *// → "红色/黑色/蓝色"* |
|   |  |
|   | extractList(*"可用颜色：红色，黑色，蓝色，等等。"*); |
|   | *// → [ "红色", "黑色", "蓝色", "等等" ]* |

这个函数没有正确处理这类列表的能力。我们来修改它！你首先需要检查列表中是否有逗号或斜杠：

|   | list.includes(*","*) ? list.split(*", "*) : list.split(*'/'*); |
| --- | --- |

includes() 方法检查列表中是否包含逗号。如果是，它返回 true，三元操作符执行 list.split(", ")。如果不是，则操作符执行 list.split("/")。

接下来，从结果数组中移除“等等”：

|   | arr.at(-1) === *"等等"* ? arr.pop() : **null**; |
| --- | --- |

at(-1) 获取数组中的最后一个项。如果它的值是“等等”，pop() 会将其移除。你也可以在这里使用 filter()，但是因为“等等”通常是数组中的最后一个项，所以只检查最后一项的值更加高效。

| 浏览器兼容性 |
| --- |
| ![images/aside-icons/important.png](images/aside-icons/important.png) | 老版本的浏览器不支持 at() 方法。为了确保你的应用能够被老旧浏览器用户访问，你应该使用补丁程序。^([[5]](f_0032.xhtml#FOOTNOTE-5)) 在 Node 环境中，最低需要 Node 版本 16.6.0。^([[6]](f_0032.xhtml#FOOTNOTE-6)) |

为了移除“and”/“or”，你可以使用 map()，如下所示：

|   | **return** arr.map(word => { |
| --- | --- |
|   | **if** (word.startsWith(*"and "*)) { |
|   | **return** word.slice(4); |
|   | } **else** **if** (word.startsWith(*"or "*)) { |
|   | **return** word.slice(3); |
|   | } **else** { |
|   | **return** word; |
|   | } |
|   | }); |

当你调用 map() 时，它会对数组中的每个元素执行一个函数。使用 startsWith() 方法检查项目开头是否有多余的“and”或“or”，并使用 slice() 方法将其移除。

你的修订函数应该如下所示：

[part_1/extracting_lists/slice_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/extracting_lists/slice_ex3.js)

|   | **function** extractList(str) { |
| --- | --- |
|   | **const** start = str.indexOf(*":"*); |
|   | **const** end = str.indexOf(*"."*, start); |
|   | **const** list = str.slice(start + 2, end); |
|   |  |
|   | *// 按逗号或斜杠分割字符串* |
|   | **const** arr = list.includes(*","*) ? list.split(*", "*) : list.split(*"/"*); |
|   |  |
|   | *// 移除 "etc"* |
|   | arr.at(-1) === *"etc"* ? arr.pop() : **null**; |
|   |  |
|   | *// 移除 and/or* |
|   | **return** arr.map(word => { |
|   | **if** (word.startsWith(*"and "*)) { |
|   | **return** word.slice(4); |
|   | } **else** **if** (word.startsWith(*"or "*)) { |
|   | **return** word.slice(3); |
|   | } **else** { |
|   | **return** word; |
|   | } |
|   | }); |
|   | } |
|   |  |
|   | extractList(*"Available in three colors: red, black, and blue."*); |
|   | *// → [ "Red", "Black", "Blue" ]* |
|   |  |
|   | extractList(*"Available colors: Red/Black/Blue."*); |
|   | *// → [ "红色", "黑色", "蓝色" ]* |
|   |  |
|   | extractList(*"可用颜色：红色，黑色，蓝色，等等。"*); |
|   | *// → [ "红色", "黑色", "蓝色" ]* |

你可能会想，为什么不使用 `replaceAll()` 方法先将文本中的“and”，“or”，“etc.”等删除，再将其分割成数组？这是因为可能会有包含这些字母的颜色名称，例如“Macaroni and Cheese”（是的，这是一个颜色名称）。

利用 `slice()` 方法提取字符串或数组的某个部分。第二个参数是可选的：如果省略它，将返回字符串的其余部分。使用 `split()` 方法将字符串分割成子字符串数组，最后，使用 `map()` 方法剔除数组中任何不需要的部分。
