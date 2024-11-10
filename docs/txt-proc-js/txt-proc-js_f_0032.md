| 例子22 | 使用剪贴板API复制文本到剪贴板 |
| --- | --- |

### 任务

假设你有一个提供各种食谱的烹饪网站，你希望为读者提供一个复制食谱食材到剪贴板的选项，以便他们可以创建购物清单。为此，你需要创建一个按钮，点击时将食材列表复制到剪贴板。

### 解决方案

首先，设置你的HTML元素。你需要一个按钮来触发JavaScript代码。记住，程序在没有用户许可的情况下不应该尝试读取或写入剪贴板。因此，创建一个明确表示会将数据复制到剪贴板的按钮是第一步：

[part_1/copying_to_clipboard/clipboard_ex1.xhtml](http://media.pragprog.com/titles/fkjavascript/code/part_1/copying_to_clipboard/clipboard_ex1.xhtml)

|   | *<!doctype html>* |
| --- | --- |
|   | <html lang=*"zh-cn"*> |
|   | <head> |
|   | <meta charset=*"utf-8"*> |
|   | <meta name=*"viewport"* content=*"width=device-width, initial-scale=1"*> |
|   | <script src=*"clipboard_ex1.js"* defer></script> |
|   | </head> |
|   |  |
|   | <body> |
|   | <ul id=*"ingredients"*> |
|   | <li>1杯橄榄油</li> |
|   | <li>4瓣大蒜</li> |
|   | <li>1汤匙磨碎孜然</li> |
|   | <li>1汤匙辣椒粉</li> |
|   | <li>2罐豆类</li> |
|   | <li>1罐压碎的番茄</li> |
|   | </ul> |
|   | <button id=*"copyBtn"* type=*"button"*>复制食材到剪贴板</button> |
|   | </body> |
|   |  |
|   | </html> |

接下来，使用getElementById()或querySelector()定位按钮，并为其添加事件监听器。按钮点击后，你需要抓取食材列表并提取其文本：

[part_1/copying_to_clipboard/clipboard_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/copying_to_clipboard/clipboard_ex1.js)

|   | document.querySelector(*"#copyBtn"*).addEventListener(*"click"*, () => { |
| --- | --- |
|   |  |
|   | *// 选择列表元素* |
|   | **const** nodeList = document.querySelectorAll(*"#ingredients li"*); |
|   |  |
|   | *// 创建一个变量，用于保存将发送到剪贴板的文本* |
|   | **let** textList = *""*; |
|   |  |
|   | *// 将每个 li 元素的文本附加到 textList* |
|   | nodeList.forEach(li => { |
|   | textList += *`** ${li.textContent} *\n`*; |
|   | }); |
|   |  |
|   | *// 将当前 URL 附加到 textList* |
|   | textList += *"查看食谱： "* + window.location.href; |
|   | writeToClipboard(textList); |
|   | }); |

现在，定义一个负责将列表写入剪贴板的函数：

[part_1/copying_to_clipboard/clipboard_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/copying_to_clipboard/clipboard_ex1.js)

|   | **function** writeToClipboard(text){ |
| --- | --- |
|   | navigator.clipboard.writeText(text).then(() => { |
|   | console.log(*"复制到剪贴板成功！"*); |
|   | }, (err) => { |
|   | console.error(*"无法复制文本: "*, err); |
|   | }); |
|   | } |

该函数的主要部分是 Clipboard 接口的 writeText() 属性。该属性返回一个 promise，因此你需要使用 then() 来处理其结果（或者，你也可以使用 await）。

如果你的代码成功将字符串写入剪贴板，你将获得一个已完成的 promise，代码会在控制台输出一条信息。如果失败，则会出现错误。

### 讨论

除了 readText() 和 writeText() 外，剪贴板 API 还提供了其他两个方法，用于读取和写入非文本数据，如图像，至用户剪贴板：read() 和 write()。虽然 readText() 和 writeText() 在所有浏览器中均可使用，但 read() 和 write() 的支持情况不稳定。因此，在你的项目中使用这些方法之前，请务必检查浏览器的支持情况。^([[22]](#FOOTNOTE-22))

在使用 Clipboard API 时，你可能会遇到如下错误：

|   | DOMException: 由于缺乏**用户激活**，剪贴板写入被阻止。 |
| --- | --- |

这个错误来自Firefox控制台，表示你正试图通过编程方式写入剪贴板，但页面没有任何用户交互，比如点击按钮。像这样的错误对于限制开发者对剪贴板的访问非常重要。

使用剪贴板API时需要考虑的其他重要因素如下：

+   你可以在没有权限的情况下将文本写入剪贴板，但要从剪贴板读取内容时，始终需要获取用户的许可（浏览器通常会自动弹出许可对话框）

+   只有当页面是当前活动的浏览器标签时，才能访问剪贴板

+   剪贴板API仅在安全环境（HTTPS）中可用

以前，访问剪贴板的唯一方法是通过Web API的document.execCommand()方法。但由于此方法是同步的，并且在读取/写入大量数据时会阻塞浏览器，因此浏览器供应商已弃用该方法，转而支持剪贴板API。

使用剪贴板接口可以为用户提供更流畅的体验，尤其是在他们需要复制代码片段、激活密钥、令牌、验证码等时，但一定要明确说明何时以及存储何种内容到剪贴板。

### 总结

无论你想对文本做什么，JavaScript都能胜任。在本书的第一部分，你学习了如何使用JavaScript的内置方法处理复杂的文本。这包括筛选数据、提取相关信息、格式化不同的数据类型、处理Unicode字符等。

在第二部分，你将专注于JavaScript中正则表达式的实现。你将详细探索语法，并通过多个示例来理解它们的应用。

#### 脚注

[[2]](f_0013.xhtml#FNPTR-2)

[https://github.com/tc39/proposal-relative-indexing-method#polyfill](https://github.com/tc39/proposal-relative-indexing-method#polyfill)

[[3]](f_0013.xhtml#FNPTR-3)

[https://mzl.la/3FKyJMr](https://mzl.la/3FKyJMr)

[[4]](f_0013.xhtml#FNPTR-4)

[https://medium.com/pragmatic-programmers/at-method-in-javascript-54544ec93ccc](https://medium.com/pragmatic-programmers/at-method-in-javascript-54544ec93ccc)

[[5]](f_0014.xhtml#FNPTR-5)

[https://github.com/tc39/proposal-relative-indexing-method#polyfill](https://github.com/tc39/proposal-relative-indexing-method#polyfill)

[[6]](f_0014.xhtml#FNPTR-6)

[https://mzl.la/3FKyJMr](https://mzl.la/3FKyJMr)

[[7]](f_0015.xhtml#FNPTR-7)

[https://zh.wikipedia.org/wiki/%E7%BD%91%E9%A2%91%E9%A6%96%E5%85%89%E8%89%B2](https://zh.wikipedia.org/wiki/%E7%BD%91%E9%A2%91%E9%A6%96%E5%85%89%E8%89%B2)

[[8]](f_0019.xhtml#FNPTR-8)

[https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/keys](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)

[[9]](f_0019.xhtml#FNPTR-9)

[https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/filter](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

[[10]](f_0023.xhtml#FNPTR-10)

[https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry](https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry)

[[11]](f_0023.xhtml#FNPTR-11)

[https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/Date](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date/Date)

[[12]](f_0023.xhtml#FNPTR-12)

[https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat/DateTimeFormat](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat/DateTimeFormat)

[[13]](f_0024.xhtml#FNPTR-13)

[https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry](https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry)

[[14]](f_0026.xhtml#FNPTR-14)

[https://caniuse.com/mdn-javascript_builtins_intl_listformat_format](https://caniuse.com/mdn-javascript_builtins_intl_listformat_format)

[[15]](f_0026.xhtml#FNPTR-15)

[https://github.com/wessberg/intl-list-format](https://github.com/wessberg/intl-list-format)

[[16]](f_0026.xhtml#FNPTR-16)

[https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry](https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry)

[[17]](f_0028.xhtml#FNPTR-17)

[https://caniuse.com/mdn-javascript_builtins_intl_segmenter_segment](https://caniuse.com/mdn-javascript_builtins_intl_segmenter_segment)

[[18]](f_0028.xhtml#FNPTR-18)

[https://github.com/flmnt/graphemer](https://github.com/flmnt/graphemer)

[[19]](f_0029.xhtml#FNPTR-19)

[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/Segmenter#browser_compatibility](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/Segmenter#browser_compatibility)

[[20]](f_0029.xhtml#FNPTR-20)

[https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry](https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry)

[[21]](f_0031.xhtml#FNPTR-21)

[https://caniuse.com/mdn-javascript_builtins_string_normalize](https://caniuse.com/mdn-javascript_builtins_string_normalize)

[[22]](#FNPTR-22)

[https://caniuse.com/?search=Clipboard](https://caniuse.com/?search=Clipboard)

版权所有 © 2024, The Pragmatic Bookshelf.
