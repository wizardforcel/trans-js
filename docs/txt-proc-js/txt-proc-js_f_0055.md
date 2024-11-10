| 配方 44 | 使用 y 标志从特定索引进行搜索 |
| --- | --- |

### 任务

假设你的任务是将会议记录整理成像文章一样的格式。假设记录如下：

|   | <p>下午2:05：我们还提高了耐用性，这是我们产品的另一个重要方面。 |
| --- | --- |
|   | 我们产品的一个方面。</p> |
|   |  |
|   | <p>下午2:10：得益于更强的几何设计，它拥有我们最抗裂的前玻璃。</p> |
|   | 更坚固且更具抗裂性的几何结构。</p> |
|   |  |
|   | <p>下午2:15：这也是我们首个拥有IP6X认证的产品，因此你 |
|   | 你不必担心在多尘环境中佩戴它。</p> |

你需要去除时间戳和多余的 <p></p> 标签，并像这样连接句子：

|   | <p>我们还提高了耐用性，这是我们产品的另一个重要方面。 |
| --- | --- |
|   | 产品。它拥有我们最抗裂的前玻璃，得益于更强的 |
|   | 以及更坚固的几何结构。这也是我们首个拥有IP6X认证的产品。 |
|   | 认证，因此你不必担心在多尘环境中佩戴它。 |
|   | 环境。</p> |

你想提取的数据具有固定结构：一个成对的HTML标签字符串和一个总是8个字符长的时间戳。因此，你只需要从索引9开始提取字符。

### 解决方案

使用 sticky 标志（y）仅从你指定的索引（通过 lastIndex 属性）匹配目标字符串：

[part_2/flag_sticky/sticky_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/flag_sticky/sticky_ex1.js)

|   | **const** re = */.+/*ys; |
| --- | --- |
|   |  |
|   | re.lastIndex = 9; |
|   |  |
|   | **const** str = *`下午2:05：我们还提高了耐用性，这是我们产品的另一个重要方面* |
|   | *我们产品的一个方面。`*; |
|   |  |
|   |  |
|   | console.log(str.match(re)[0]); |
|   | *// → 我们还提高了耐用性，这是我们产品的另一个重要方面。* |
|   | *// 产品。* |

现在你知道你的正则表达式有效，可以用它从实际的HTML文档中提取文本：

[part_2/flag_sticky/sticky.xhtml](http://media.pragprog.com/titles/fkjavascript/code/part_2/flag_sticky/sticky.xhtml)

|   | *<!doctype html>* |
| --- | --- |
|   | <html lang=*“en-us”*> |
|   | <head> |
|   | <meta charset=*“utf-8”*> |
|   | <meta name=*“viewport”* content=*“width=device-width, initial-scale=1”*> |
|   | <script src=*“sticky_ex2.js”* defer></script> |
|   | </head> |
|   | <body> |
|   | <p>下午2:05：我们还提高了耐用性，这是另一个至关重要的方面</p> |
|   | 我们的产品之一。</p> |
|   | <p>下午2:10：得益于 |
|   | 更强大且更加坚固的几何结构。</p> |
|   | <p>下午2:15：这是我们的首个获得 IP6X 认证的产品，因此你 |
|   | 无需担心在灰尘环境中佩戴。</p> |
|   | </body> |
|   | </html> |

调用 querySelectorAll() 方法获取所有段落元素，并将每个元素传递给应用正则表达式的函数，如下所示：

[part_2/flag_sticky/sticky_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/flag_sticky/sticky_ex2.js)

|   | **let** result = *“”*; |
| --- | --- |
|   |  |
|   | *// 从每个元素中提取信息并附加到结果中* |
|   | **function** extractData(str) { |
|   | **const** re = */.+/*ys; |
|   | re.lastIndex = 9; |
|   | **const** match = str.match(re); |
|   | **if** (match) { |
|   | result = result + match[0] + *“ ”*; |
|   | } **else** { |
|   | **throw** **new** Error(*“没有找到匹配项。”*); |
|   | } |
|   | } |
|   |  |
|   | *// 执行 extractData() 函数，处理每个 <p> 元素的内容* |
|   | document.querySelectorAll(*“p”*).forEach(el => { |
|   | extractData(el.textContent); |
|   | }); |
|   |  |
|   | *// 从结果字符串中移除换行符,* |
|   | *// 去除字符串两端的空白字符,* |
|   | *// 并将其包含在一对 <p> 标签中.* |
|   | console.log(*`<p>*${result.trim().replaceAll(*“***\***n”*, *“”*)}*</p>`*); |

现在你有了可以像故事一样阅读的连续句子。

### 讨论

sticky 标志仅在 lastIndex 属性指示的位置执行搜索。考虑以下代码：

[part_2/flag_sticky/sticky_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/flag_sticky/sticky_ex3.js)

| 1:  | **const** str = *"crack resistant"*; |
| --- | --- |
| -  | **const** re = */resistant/*y; |
| -  |  |
| -  | re.lastIndex = 0; |
| 5:  | console.log(str.match(re)); |
| -  | *// → null (在索引 0 处没有匹配项)* |
| -  |  |
| -  | re.lastIndex = 2; |
| -  | console.log(str.match(re)); |
| 10:  | *// → null (在索引 2 处没有匹配项)* |
| -  |  |
| -  | re.lastIndex = 6; |
| -  | console.log(str.match(re)); |
| -  | *// → ["resistant", index: 6, input: "crack resistant", groups: undefined]* |
| 15:  |  |
| -  | console.log(re.lastIndex); |
| -  | *// → 15* |

sticky 搜索不会匹配除 lastIndex 属性所指示的索引之外的字符。另请注意，当操作成功时，标志如何更新 lastIndex 属性（第 16 行）。

| 标志的顺序 |
| --- |
| ![images/aside-icons/tip.png](images/aside-icons/tip.png) | JavaScript 标志可以按任何顺序或组合指定。正则表达式 /abc/img 的行为与 /abc/mgi 相同。 |

当我们要匹配的字符串具有固定结构时，sticky 标志非常有用。在这个示例中，我们事先知道输入字符串的结构：一个时间戳后跟一个句子。因此，我们通过告诉引擎仅在我们需要的数据所在的位置进行搜索来简化了模式。没有 sticky 标志，模式可能会变得不必要地更复杂。
