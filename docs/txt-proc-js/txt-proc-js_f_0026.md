| 食谱 16 | 使用 Intl.ListFormat() 创建语言敏感型列表 |
| --- | --- |

### 任务

假设你有一个游戏应用，想根据玩家的分数显示本周的前三名。由于你的应用支持多语言，你需要一个可以根据用户语言偏好自动格式化列表的函数。通常，这类项目会以数组形式存储，你需要根据不同的语言格式化成句子。

### 解决方案

使用 Intl.ListFormat() 构造函数：

[part_1/creating_lists/ListFormat_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/creating_lists/ListFormat_ex1.js)

| 1:  | **const** topPlayers = [*"Kraken"*, *"Boss99"*, *"Ninja"*]; |
| --- | --- |
| -  | **const** msg = *"恭喜本周的获胜者："*; |
| -  |  |
| -  | **function** getFormattedList(lang, arr) { |
| 5:  | **const** formatter = **new** Intl.ListFormat(lang, {type: *"conjunction"*}); |
| -  | **return** formatter.format(arr); |
| -  | } |
| -  |  |
| -  | console.log(msg + getFormattedList(*"en"*, topPlayers)); |
| 10:  |  |
| -  | *// 日志：* |
| -  | *// → 恭喜本周的获胜者：Kraken、Boss99 和 Ninja* |

这个函数会根据指定的语言返回数组项的格式化字符串表示。

| 浏览器兼容性 |
| --- |
| ![images/aside-icons/important.png](images/aside-icons/important.png) | ListFormat 支持已在 macOS 的 Safari 14.1 和 iOS 的 Safari 14.5 中添加。^([[14]](f_0032.xhtml#FOOTNOTE-14)) 因此，尽管所有现代浏览器都支持 ListFormat，但一些没有及时更新浏览器的用户将无法运行你的应用。为了最大程度兼容，使用该 API 时可以配合 polyfill，^([[15]](f_0032.xhtml#FOOTNOTE-15)) 或者在服务器端使用（自 Node 版本 13.0.0 起可用）。 |

### 讨论

ECMAScript国际化API使我们能够开发可以适应不同语言的应用程序。要访问这个API，我们使用Intl命名空间。在这个示例中，我们使用了API的Intl.ListFormat()构造函数，它提供了一种简单的方式来以文化上适当的方式格式化列表。

我们首先创建一个名为getFormattedList()的函数，接受两个参数：lang和arr。lang是一个BCP 47语言标签，表示用于格式化列表的语言代码，而arr是需要格式化的项数组。^([[16]](f_0032.xhtml#FOOTNOTE-16))

在函数内部，我们创建了一个Intl.ListFormat的实例，它接受两个参数：lang和options对象。在这个例子中，我们希望将列表格式化为英文，因此我们传入“en”作为语言标签。options对象指定了用于连接列表项的连接词类型。我们通过设置{type: "conjunction"}来指定使用“and”作为连接词。

最后，我们在Intl.ListFormat对象上调用formatter.format(arr)方法，并传入arr参数。这个方法会根据我们之前设置的语言和连接词类型返回一个格式化后的数组项字符串表示。

要在不同的语言中格式化列表，我们只需要将相关的语言标签传递给函数。例如，如果我们想要将列表格式化为西班牙语，我们可以传入“es”作为参数来调用函数。

这是当语言参数设置为“es”时，函数的输出示例：

[part_1/creating_lists/ListFormat_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/creating_lists/ListFormat_ex2.js)

|   | **const** topPlayers = [*"Kraken"*, *"Boss99"*, *"Ninja"*]; |
| --- | --- |
|   | **const** msg = *"恭喜本周的获胜者："*; |
|   |  |
|   | **function** getFormattedList(lang, arr) { |
|   | **const** formatter = **new** Intl.ListFormat(lang, {type: *"conjunction"*}); |
|   | **return** formatter.format(arr); |
|   | } |
|   |  |
|   | console.log(msg + getFormattedList(*"es"*, topPlayers)); |
|   |  |
|   | *// 输出日志:* |
|   | *// → 恭喜本周的获胜者：Kraken、Boss99 和 Ninja* |

即使我们只想在英文中格式化列表，Intl.ListFormat() 构造函数也非常有用，因为它避免了可能的语法错误。例如，如果数组中只有两个项，它不会在“and”前加上逗号：

[part_1/creating_lists/ListFormat_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/creating_lists/ListFormat_ex3.js)

|   | **const** topPlayers = [*"Kraken"*, *"Boss99"*]; |
| --- | --- |
|   | **const** msg = *"恭喜本周的获胜者： "*; |
|   | **function** getFormattedList(lang, arr) { |
|   | **const** formatter = **new** Intl.ListFormat(lang, {type: *"conjunction"*}); |
|   | **return** formatter.format(arr); |
|   | } |
|   |  |
|   | console.log(msg + getFormattedList(*"en"*, topPlayers)); |
|   |  |
|   | *// 输出日志:* |
|   | *// → 恭喜本周的获胜者：Kraken 和 Boss99* |

ListFormat 方法的第二个参数是可选的，允许我们设置诸如样式和分组类型等选项。默认的类型是连接词，但如果我们想对列表项进行基于“或”的分组，则可以使用析取。

比如，我们可能想询问玩家们更喜欢哪种荣誉称号：传奇、强大或勇敢。然后，应用程序会将该称号附加到他们的名字上，如“Faraz the Mighty”：

[part_1/creating_lists/ListFormat_ex4.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/creating_lists/ListFormat_ex4.js)

|   | **const** titles = [*"Legendary"*, *"Mighty"*, *"Bold"*]; |
| --- | --- |
|   | **const** formatter = **new** Intl.ListFormat(*"en"*, {type: *"disjunction"*}); |
|   |  |
|   | console.log(*"你更喜欢哪个荣誉称号？ "* + |
|   | formatter.format(titles)); |
|   |  |
|   | *// 输出日志:* |
|   | *// → 你更喜欢哪个荣誉称号？传奇的、强大的，还是大胆的* |

还有一个选项可以让我们将列表项作为一个整体分组：

[part_1/creating_lists/ListFormat_ex5.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/creating_lists/ListFormat_ex5.js)

|   | **const** titles = [*"Legendary"*, *"Mighty"*, *"Bold"*]; |
| --- | --- |
|   | **const** formatter = **new** Intl.ListFormat(*"en"*, {type: *"unit"*}); |
|   |  |
|   | console.log(formatter.format(titles)); |
|   |  |
|   | *// 输出日志:* |
|   | *// → 传奇的、强大的、大胆的* |

这个示例将类型的值设置为单元，因此它格式化列表时不使用“和”或“或”。

每当你想在句子中列举一系列项目时，可以考虑使用 ListFormat 构造函数，因为它能正确处理英语或其他语言中的标点符号。
