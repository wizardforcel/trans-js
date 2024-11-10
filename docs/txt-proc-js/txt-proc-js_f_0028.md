| 配方 18 | 使用 Intl.Segmenter() 计算 Unicode 字符数 |
| --- | --- |

### 任务

假设你有一个需要用户注册的应用，其中包含一个文本输入框用于填写用户的个人简介。这个简介可以是任何语言，并且可能包含表情符号。你希望将简介的长度精确限制为 120 个字符。因此，你需要计算字符串的长度。很简单！使用 length() 方法来获取字符的数量：

![images/char_segmenter_ex1.png](images/char_segmenter_ex1.png)

这可能不是你期望的结果。JavaScript 中的字符串是基于 UTF-16 的，它使用一个或两个 16 位的整数来表示字符。有些字符，比如“口才”中的“口”和猫咪表情符号，需要两个 16 位的单元（代理对）来编码。length() 方法给出的是字符串中 UTF-16 代码单元的数量，而不是字符的数量。

| 补充字符 |
| --- |
| ![images/aside-icons/info.png](images/aside-icons/info.png) | 由一对 16 位代理代码单元组成的字符被称为补充字符。 |

### 解决方案

使用 Intl.Segmenter() 构造函数：

[part_1/counting_characters/char_segmenter_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/counting_characters/char_segmenter_ex2.js)

|   | **函数** getLength(str) { |
| --- | --- |
|   | **返回** [...**new** Intl.Segmenter().segment(str)].length; |
|   | } |

![images/char_segmenter_ex2.png](images/char_segmenter_ex2.png)

此函数返回输入字符串中的 Unicode 段数。换句话说，它根据 Unicode 字符的数量而非代码单元的数量来确定给定字符串的长度。

| 浏览器兼容性 |
| --- |
| ![images/aside-icons/warning.png](images/aside-icons/warning.png) | Segmenter() 是国际化 API 的一部分。虽然大多数浏览器已经支持国际化 API 的特性多年，但 Segmenter() 是一个相对较新的特性，目前在 Firefox 中不受支持（截至本文撰写时）。^([[17]](f_0032.xhtml#FOOTNOTE-17))有一些 Unicode 感知库，比如 Graphemer，可以让你将 JavaScript 字符串拆分成单独的字母，^([[18]](f_0032.xhtml#FOOTNOTE-18))但它们的结果与 Segmenter 的结果并不完全一致。目前没有完美的方法来模拟 Segmenter() 在浏览器中的行为，因为这需要大量语言特定的规则。在浏览器的支持更加稳固之前，你可以在服务器端运行 Intl.Segmenter()（从 Node 16 开始支持）。 |

### 讨论

Intl.Segmenter() 构造函数允许我们根据指定的语言环境和粒度对字符串进行分段。在这个例子中，我们使用默认实现，因此我们调用该方法时不传递任何参数。由于 Intl.Segmenter() 是一个构造函数，我们需要使用 new 关键字来调用它。

返回的对象有一个 segment() 方法，该方法接受一个单一的字符串参数。正如其名字所示，该方法将字符串分段，意味着它将字符串拆分为用户感知的字符边界。由于返回值是一个迭代器，我们可以使用展开语法 (...) 将对象展开为其元素。展开语法由三个连续的点组成，可以让我们迅速从迭代器中创建一个数组。

最后，我们计算数组的长度，以获得字符串中 Unicode 字符的数量。如果你觉得代码过于晦涩，可以使用这个版本代替：

[part_1/counting_characters/char_segmenter_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/counting_characters/char_segmenter_ex3.js)

|   | **function** getLength(str) { |
| --- | --- |
|   | *// 创建一个 segmenter 实例* |
|   | **const** Segmenter = **new** Intl.Segmenter(); |
|   |  |
|   | *// 对字符串进行分段* |
|   | **const** segment = Segmenter.segment(str); |
|   |  |
|   | *// 将其转换为数组* |
|   | **const** arr = Array.**from**(segment); |
|   |  |
|   | *// 返回字符的数量* |
|   | **return** arr.length; |
|   | } |

![images/char_segmenter_ex3.png](images/char_segmenter_ex3.png)

这段代码与第一段代码执行相同的操作。你可能会遇到使用其他技巧来计算字符串中字符数的代码。一种方法是将字符串转换为字符数组，然后计算数组中元素的数量：

![images/char_segmenter_ex4.png](images/char_segmenter_ex4.png)

这个技巧有效是因为自 ES2015 起，字符串内置了 Unicode 感知的迭代器，并自动将补充字符当作单一值处理。然而，计算字符串中的字符数并不总是那么简单。在某些情况下，这种方法可能会给出不准确的结果。例如：

![images/char_segmenter_ex5.png](images/char_segmenter_ex5.png)

上面的家庭表情符号是一个 Emoji ZWJ 序列，由三个独立的表情符号组成：

![images/char_segmenter_ex6.png](images/char_segmenter_ex6.png)

当在它们之间放置一个零宽连接符（ZWJ）时，这些表情符号会以连接的形式显示。ZWJ 是一个不可打印字符，它会导致字符或表情符号在支持的平台上以连接的形式显示。

在上面的例子中，表情符号的长度为 5，因为我们计算了每个零宽连接符（ZWJ）。以下代码片段可以让这一点更清楚：

![images/char_segmenter_ex7.png](images/char_segmenter_ex7.png)

结果中的空字符串表示 ZWJ 字符。由于 ZWJ 是不可打印的，它们会显示为空字符串。

另一个问题是，一些字符看起来相同，但它们的代码点不同，因此它们不相等。请看以下代码：

![images/char_segmenter_ex8.png](images/char_segmenter_ex8.png)

分配给 str1 的字符可能与分配给 str2 的字符看起来完全相同，但实际上它们是不同的字符。第一个字符串中的字符的代码点是 U+00E9（拉丁小写字母 E 带有重音符号），而第二个字符由两个独立的代码点组成，包括 U+0065（拉丁小写字母 E）和 U+0301（组合重音符号）：

|   | console.log(*"***\***u00E9"*); *// → é* |
| --- | --- |
|   | console.log(*"***\***u0065***\***u0301"*); *// → é* |

这解释了为什么第二个字符串的长度是 2。幸运的是，国际化 API 足够智能，可以将这种字符视为单个字符来计算。对比一下：

![images/char_segmenter_ex9.png](images/char_segmenter_ex9.png)

回顾前一个食谱，我们知道 charAt() 不能处理补充字符。让我们利用 Intl.Segmenter() 编写一个函数来解决这个问题：

[part_1/counting_characters/char_segmenter_ex4.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/counting_characters/char_segmenter_ex4.js)

|   | *// charAt() 替代方法* |
| --- | --- |

![images/char_segmenter_ex10.png](images/char_segmenter_ex10.png)

这个函数与我们在本食谱中看到的第一个函数非常相似，不同之处在于它使用了[index]["segment"]，而不是.length。表达式[index]可以让我们获取被对象包装的字符，["segment"]则是指对象中包含字符的属性。

每当你需要获取包含 Unicode 字符的字符串长度时，可以使用Intl.Segmenter()构造函数。但字符计数并不是Intl.Segmenter()唯一的功能。在下一个食谱中，我们将学习如何使用这个 API 来计算字符串中的单词数。
