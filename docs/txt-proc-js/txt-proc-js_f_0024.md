|   食谱 14 | 使用Intl.NumberFormat()格式化货币 |
| --- | --- |

### 任务

假设你经营一家在线商店，向多个国家/地区提供商品。你希望以用户所在位置的货币显示商品价格。例如，如果一位来自加拿大的访客选择查看一款价格为499美元的显示器，你希望自动 1) 将价格从美元（USD）转换为加元（CAD），并 2) 按照加元格式化货币。

### 解决方案

首先，你需要获得美元（USD）和加元（CAD）之间的汇率。由于汇率可能会不断变化，你应该使用一个提供实时数据的在线API来获取你想要转换的货币。这些服务通常需要付费订阅。

在本示例中，我们将使用exchangerate.host提供的免费服务，该服务每天只更新一次汇率。你可以通过指定你想要转换的货币作为参数，向API发送请求。

一旦获取数据成功，使用json()方法读取并解析数据，如下所示：

|   | **async** **function** getExchangeRate(**from**, to) { |
| --- | --- |
|   | **const** api = *`https://api.exchangerate.host/convert?from=*${**from**}*&to=*${to}*`*; |
|   | **let** response = **await** fetch(api); |
|   | response = **await** response.json(); |
|   | **return** response.info.rate; |
|   | } |
|   |  |
|   | **const** exchangeRate = getExchangeRate(*"USD"*, *"CAD"*); |

现在你已经获得了目标货币的汇率，你需要一种方法来格式化它。将你想要转换的货币的ISO代码作为选项传递给`Intl.NumberFormat()`构造函数。这样将返回一个包含`format()`方法的对象，你可以使用它来格式化任意金额：

|   | **function** getFormattedCurrency(currency, amount) { |
| --- | --- |
|   | **return** **new** Intl.NumberFormat(*"en-US"*, { |
|   | style: *"currency"*, |
|   | currency: currency, |
|   | }).format(amount); |
|   | } |
|   |  |
|   | getFormattedCurrency(*"CAD"*, exchangeRate * 499) |

清理后，你的最终代码应该如下所示：

[part_1/formatting_currencies/NumberFormat_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/formatting_currencies/NumberFormat_ex1.js)

|   | **const** USDprice = 499; |
| --- | --- |
|   |  |
|   | **异步** **函数** getExchangeRate(**from**, to) { |
|   | **const** api = *`https://api.exchangerate.host/convert?from=*${**from**}*&to=*${to}*`*; |
|   | **let** response = **await** fetch(api); |
|   | response = **await** response.json(); |
|   | **返回** response.info.rate; |
|   | } |
|   |  |
|   | **函数** getFormattedCurrency(currency, amount) { |
|   | **返回** **new** Intl.NumberFormat(*"en-CA"*, { |
|   | style: *"currency"*, |
|   | currency: currency, |
|   | }).format(amount); |
|   | } |
|   |  |
|   | getExchangeRate(*"USD"*, *"CAD"*).then(exchangeRate => { |
|   | console.log(getFormattedCurrency(*"CAD"*, exchangeRate * USDprice)); |
|   | }); |
|   |  |
|   | *// 输出类似以下内容:* |
|   | *// → CA$679.31* |
| 类型错误 |
| --- |
| ![images/aside-icons/error.png](images/aside-icons/error.png) | 如果你遇到类似“TypeError: Failed to fetch”的错误，很可能是因为你在浏览器控制台中运行代码。除非你在 https://exchangerate.host/ 上，否则浏览器的安全机制会阻止请求。尝试在 HTML 文档中或 Node 环境中执行代码（需要 Node v18）。 |

### 讨论

和国际化 API 中的其他方法一样，Intl.NumberFormat() 接受一个 BCP 47 语言标签作为它的第一个参数。^([[13]](f_0032.xhtml#FOOTNOTE-13)) 在这里，语言标签告诉方法在格式化货币时使用哪种区域设置，这在你想要为你的网站提供多语言支持时非常有用。

如果你传递“ar”作为语言标签，返回的数字将使用阿拉伯字母：

[part_1/formatting_currencies/NumberFormat_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/formatting_currencies/NumberFormat_ex2.js)

|   | **函数** getFormattedCurrency(currency, amount) { |
| --- | --- |
|   | **返回** **new** Intl.NumberFormat(*"ar"*, { |
|   | style: *"货币"*, |
|   | currency: currency, |
|   | }).format(amount); |
|   | } |

![images/NumberFormat_ex2.png](images/NumberFormat_ex2.png)

你可以通过设置第二个参数中的选项，进一步调整货币的显示方式。一项有用的选项是 signDisplay，它让你可以设置何时显示数字的符号。

默认情况下，函数仅在负数（包括负零，即四舍五入为零的负数）时显示符号。如果你希望始终显示符号，比如表示余额变动时，应该使用“始终”：

[part_1/formatting_currencies/NumberFormat_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/formatting_currencies/NumberFormat_ex3.js)

|   | **函数** getFormattedCurrency(currency, amount) { |
| --- | --- |
|   | **返回** **new** Intl.NumberFormat(*"en"*, { |
|   | style: *"货币"*, |
|   | currency: currency, |
|   | signDisplay: *"始终"* |
|   | }).format(amount); |
|   | } |
|   |  |
|   | getFormattedCurrency(*"USD"*, 499); *// → "+$499.00"* |

Intl.NumberFormat() 构造函数使得在 JavaScript 中处理数字变得简单。记得在需要格式化货币时充分利用它。
