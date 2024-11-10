| 配方 13 | 使用 Intl.DateTimeFormat() 格式化日期 |
| --- | --- |

### 任务

假设你在一家在线商店工作，商店在购买日期后两天交付产品。你的任务是编写一段 JavaScript 代码，通知用户他们可以在具体的星期几收到所订购的商品。

例如，如果客户在周六购买了商品，你的代码应当通知他们，交货将在下周一进行。

### 解决方案

这项任务包括三个步骤：

+   获取当前日期

+   将当前日期加上两天

+   将该日期转换为星期几

我们可以通过以下函数完成前两步：

|   | **function** addDaysToToday(days) { |
| --- | --- |
|   | **const** d = **new** Date(); |
|   | d.setDate(d.getDate() + days); |
|   | **return** d; |
|   | } |
|   |  |
|   | **const** dayAfterTomorrow = addDaysToToday(2); |
|   |  |
|   | console.log(dayAfterTomorrow); |
|   | *// → Wed Apr 12 2023 11:41:09 GMT+0400* |

首先，使用 Date() 构造函数获取当前日期。接下来，通过调用日期对象的 getDate() 方法获取今天的日期。将此值加上二得到后天的日期。然后，使用 setDate() 方法更新日期，日期对象会自动调整月份和年份（如有需要）。

执行前面的步骤后，你将获得一个包含后天日期的字符串，其中包括时间戳和时区。但你只需要日期和月份，并且不希望包含时间戳或时区。因此，使用 Intl.DateTimeFormat() 构造函数来格式化日期：

|   | **function** getFormattedDate(locale, date) { |
| --- | --- |
|   | **const** formatter = **new** Intl.DateTimeFormat(locale, {dateStyle: *"full"*}); |
|   | **return** formatter.format(date); |
|   | } |
|   |  |
|   | **const** formattedDate = getFormattedDate(*"en-US"*, dayAfterTomorrow) |
|   |  |
|   | console.log(formattedDate); |
|   | *// → 2023年4月12日，星期三* |

`Intl.DateTimeFormat()` 接受一个对象作为第二个参数，用于指定日期的格式。在这种情况下，你希望在日期中包含星期几，所以需要将 `dateStyle` 设置为 `full`。

以下是最终代码的样子：

[part_1/formatting_dates/adding_days_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/formatting_dates/adding_days_ex1.js)

|   | **function** addDaysToToday(days) { |
| --- | --- |
|   | **const** d = **new** Date(); |
|   | d.setDate(d.getDate() + days); |
|   | **return** d; |
|   | } |
|   |  |
|   | **function** getFormattedDate(locale, date) { |
|   | **const** formatter = **new** Intl.DateTimeFormat(locale, {dateStyle: *"full"*}); |
|   | **return** formatter.format(date); |
|   | } |
|   |  |
|   | **const** dayAfterTomorrow = addDaysToToday(2); |
|   | **const** msg = *"我们将在 "*; |
|   |  |
|   | console.log(msg + getFormattedDate(*"en-US"*, dayAfterTomorrow)); |
|   | *// → 我们将在2023年4月12日，星期三交付您的购买商品* |

这段代码根据当前日期和指定的区域生成一条消息，内容为预计的购买商品交付日期。

### 讨论

为确保应用程序中的日期格式适用于商品发货所在国家/地区，你应该将适当的 BCP 47 语言标签传递给 `Intl.DateTimeFormat()`。^([[10]](f_0032.xhtml#FOOTNOTE-10))

语言标签由一个或多个子标签组成，用于标识语言、脚本、区域和其他与语言相关的信息。例如，"en-GB" 是表示英国英语的语言标签，其中 "en" 表示语言，"GB" 表示区域。BCP-47 标准广泛应用于软件开发中，以确保在不同平台上提供一致的语言支持。

在这个解决方案中，我们使用了“en-US”语言来表示美式英语。但如果你要将产品交付到法国，例如，应该使用“fr-FR”标签来表示法语：

[part_1/formatting_dates/adding_days_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/formatting_dates/adding_days_ex2.js)

|   | **function** addDaysToToday(days) { |
| --- | --- |
|   | **const** d = **new** Date(); |
|   | d.setDate(d.getDate() + days); |
|   | **return** d; |
|   | } |
|   |  |
|   | **function** getFormattedDate(locale, date) { |
|   | **const** formatter = **new** Intl.DateTimeFormat(locale, {dateStyle: *"full"*}); |
|   | **return** formatter.format(date); |
|   | } |
|   |  |
|   | **const** dayAfterTomorrow = addDaysToToday(2); |
|   | **const** msg = *"我们将在您的购买交付 "*; |
|   |  |
|   | console.log(msg + getFormattedDate(*"fr-FR"*, dayAfterTomorrow)); |
|   | *// → 我们将在2023年4月12日星期三交付您的购买* |
| 转换字符串为日期对象 |
| --- |
| ![images/aside-icons/tip.png](images/aside-icons/tip.png) | 如果你想从文本中提取日期并将其转换为日期对象，可以使用Date()构造函数。^([[11]](f_0032.xhtml#FOOTNOTE-11)) |

在处理日期和时间时，考虑使用Intl.DateTimeFormat()构造函数。Intl.DateTimeFormat()允许你获取不同语言的日期格式，设置日期和时间的样式，定义诸如泰语和阿拉伯语等语言的数字系统，等等。要查看完整的可用选项列表，请访问MDN Web文档。^([[12]](f_0032.xhtml#FOOTNOTE-12))
