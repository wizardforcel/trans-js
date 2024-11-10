`第8章`

# `编码字符串和日期`

`在本章中`

![Bullet](images/check.png) `连接字符串`

![Bullet](images/check.png) `处理日期`

![Bullet](images/check.png) `调整时间`

尽管你的JavaScript代码在处理网页小玩意（如HTML标签和CSS属性）时会花费大量时间，但它还会执行许多后台工作，这些工作需要操作字符串以及处理日期和时间。为了帮助你完成这些任务，在本章中你将探讨JavaScript的两个内置对象：`String`对象和`Date`对象。你将研究每个对象最重要的属性并掌握最常用的方法。## `操作字符串`

到目前为止，我在这本书中使用了数十个字符串的示例。这些示例不仅包括字符串字面量（例如`"JavaScript Essentials For Dummies"`），还包括返回字符串的方法（例如`prompt()`方法）。因此，现在应该清楚，字符串在所有JavaScript编程中扮演着重要角色，几乎没有脚本不以某种方式处理字符串。

出于这个原因，掌握字符串的操作是值得的，包括在字符串中定位文本和从字符串中提取文本。你将在本节中了解到这些内容及更多信息。

你处理的任何字符串——无论是字符串字面量还是返回字符串的方法或函数的结果——都是一个`String`对象。因此，例如，以下两个语句是等效的：

`const bookName = new String("JavaScript Essentials For Dummies"); const bookName = "JavaScript Essentials For Dummies";`

这意味着在应用`String`对象的属性和方法时，你有相当大的灵活性。例如，`String`对象有一个`length`属性，我将在下一节中描述。以下都是使用该属性的合法JavaScript表达式：

`bookName.length; "JavaScript Essentials For Dummies".length; prompt("Enter the book name:").length; myFunction().length;`

最后一个示例假设`myFunction()`返回一个字符串值。

### `使用字符串模板`

在深入了解`String`对象的属性和方法之前，花点时间来审视一种特殊类型的字符串，它旨在解决你编程生涯中会反复遇到的三个与字符串相关的问题：

+   `处理内部引号：` 字符串字面量用引号括起来，但当你需要在字符串内部使用相同类型的引号时，该怎么办？

    一种解决方案是使用不同类型的引号来定界字符串。例如，这样是非法的：

    `'一定得有更好的方法来做这件事。'`

    但这样是可以的：

    `"一定得有更好的方法来做这件事。"`

    第二种解决方案是用斜杠转义内部引号，如下所示：

    `'一定得有更好的方法来做这件事。'`

    这些解决方案效果良好，但`remembering`使用它们比你想象的要困难！

+   `包含变量值：` 当你需要在字符串中使用变量的值时，通常会得到一些笨拙的表达式，例如：`const adjective = "better"; const lament = "There's got to be some " + adjective + " way to do this.";`

+   `多行字符串：` 它有时用于定义使用多行的字符串。然而，如果你尝试以下操作，你会得到一个 `string literal contains an unescaped line break` 错误：`const myHeader = '<nav class="banner"> <h3 class="nav-heading">Navigation</h3> <ul class="nav-links"> <li>Home</li> <li>Away</li> <li>In Between</li> </ul> </nav>'`

你可以通过使用一个`string template`（也称为`template literal`）来解决所有三个问题，这是一种字符串字面量，其中分隔的引号被反引号（`` ` ``）替换：

`` `*Your string goes here*` ``

![Remember](images/remember.png) 字符串模板是在 ECMAScript 2015 (ES6) 中引入的，因此仅在不需要支持古老的网页浏览器（如 Internet Explorer 11）时使用它们。

这是你如何使用字符串模板来解决刚刚描述的三个问题：

+   `处理内部引号：` 你可以在字符串模板中放置任意数量的单引号或双引号： `` `Ah, here's the better way to do this!` ``

+   `包含变量值：` 字符串模板支持一种叫做`variable interpolation`的技术，可以直接在字符串中引用变量值。以下是一个例子： ``const adjective = "better"; const paean = `Ah, here's the ${adjective} way to do this!`;``

    在任何字符串模板中，使用`${*variable*}`会插入`*variable*`的值，毫无疑问。实际上，你不必仅限于变量。字符串模板还可以插入任何JavaScript表达式，包括函数结果。

+   `多行字符串：` 字符串模板乐于与跨越多行的字符串无误地工作： `` const myHeader = `<nav class="banner"> <h3 class="nav-heading">Navigation</h3> <ul class="nav-links"> <li>Home</li> <li>Away</li> <li>In Between</li> </ul> </nav>` ``  ### 确定字符串的长度

`String`对象最基本的属性是它的`length`，它告诉你字符串中有多少个字符：

`` *string*.length ``

字符串中的所有字符——包括空格和标点符号——都算作长度。唯一的例外是转义序列（如`\n`），它们始终算作一个字符。以下代码获取各种 `String` 对象类型的长度属性值。

`function myFunction() { return "filename.htm"; } const bookName = "JavaScript Essentials For Dummies"; length1 = myFunction().length; // 返回 12 length2 = bookName.length; // 返回 37 length3 = "123\n5678".length; // 返回 8`

`String` 对象虽然在属性上有所欠缺，但在方法上却弥补了这一点。它有数十种方法，可以帮助你的代码执行许多有用的任务，从大小写字母转换，到在字符串中查找文本，再到提取字符串的部分内容。 ### 查找子字符串

`substring` 是一个现有字符串的部分。例如，字符串 `"JavaScript"` 的一些子字符串可能是 `"Java"`、`"Script"`、`"vaSc"` 和 `"v"`。在脚本中处理字符串时，你经常需要确定一个字符串是否包含另一个子字符串。例如，如果你在验证用户的电子邮件地址时，你应该检查其中是否包含 `@` 符号。

[表 8-1](#c08-tbl-0001) 列出了几种用于在较大字符串中查找子字符串的 `String` 对象方法。

[表 8-1](#rc08-tbl-0001) `String` 对象查找子字符串的方法

| **方法** | **功能** |
| --- | --- |
| `string.endsWith(substring, start)` | 检测 `substring` 是否出现在 `string` 的结尾 |
| `string.includes(substring, start)` | 检测 `substring` 是否出现在 `string` 中 |
| `string.indexOf(substring, start)` | 在 `string` 中搜索第一个出现的 `substring` |
| `string.lastIndexOf(substring, start)` | 在 `string` 中搜索最后一个出现的 `substring` |

| `string.startsWith(substring, start)` | 检测 `substring` 是否出现在 `string` 的开头 |  ### 学习提取子字符串的方法

查找子字符串是一回事，但你经常需要提取子字符串。例如，如果用户输入了一个电子邮件地址，你可能需要提取用户名（`@` 左边的部分）或域名（`@` 右边的部分）。对于这些操作，JavaScript 提供了六种方法，详见 [表 8-2](#c08-tbl-0002)。

[表 8-2](#rc08-tbl-0002) `String` 对象提取子字符串的方法

| **方法** | **功能** |
| --- | --- |
| `string.charAt(index)` | 返回 `string` 中指定 `index` 位置的字符 |
| `string.charCodeAt(index)` | 返回 `string` 中指定 `index` 位置字符的编码 |
| `string.slice(start, end)` | 返回 `string` 中从 `start` 索引位置开始、到 `end` 索引位置之前的子字符串 |
| `string.split(separator, limit)` | 返回一个数组，每个元素是 `string` 中的一个子字符串，这些子字符串由 `separator` 字符分隔 |
| `string.substr(start, length)` | 返回 `string` 中从 `start` 指定的索引位置开始，长度为 `length` 的子字符串 |

| `string.substring(start, end)` | 返回 `string` 中从 `start` 指定的索引位置开始，并在 `end` 指定的索引位置前结束的子字符串 | ## 处理日期和时间

日期和时间看起来应该是直截了当的编程命题。毕竟，一年只有 12 个月，一个月有 28 到 31 天，一周有 7 天，一天有 24 小时，一小时有 60 分钟，一分钟有 60 秒。难道如此固定的东西竟然会变得有些奇怪吗？

你可能会感到惊讶。日期和时间`可以`变得很奇怪，但如果你始终记住三个关键点，它们会变得更容易处理：

+   JavaScript 时间以毫秒为单位，或者说是千分之一秒。更具体地说，JavaScript 通过计算从 1970 年 1 月 1 日到当前日期和时间之间经过的毫秒数来衡量时间。所以，举个例子，`你` 可能会遇到 2001 年 1 月 1 日，并且想，“啊，是的，新千年的开始。”然而，`JavaScript` 看到这个日期时，它看到的是 `978220800000`。

+   在 JavaScript 的世界里，时间从 1970 年 1 月 1 日格林威治标准时间午夜开始。那之前的日期在毫秒数上是 `负` 值。

+   因为你的 JavaScript 程序运行在用户的浏览器中，所以日期和时间几乎总是用户的 `本地` 日期和时间。也就是说，你的脚本处理的日期和时间`不是`托管页面的服务器上的日期和时间。这意味着你永远无法知道用户在何时查看你的页面。

### 学习 Date 对象的参数

在深入了解 `Date` 对象及其相关方法之前，我会先简单讲解 JavaScript 在许多与日期相关的功能中所需的各个参数。这样可以避免之后重复冗长地提到这些参数。[表 8-3](#c08-tbl-0003) 提供了详细信息。

[表 8-3](#rc08-tbl-0003) 与 Date 对象相关的参数

| **参数** | **表示的内容** | **可能的值** |
| --- | --- | --- |
| `date` | 变量名 | `Date` 对象 |
| `yyyy` | 年份 | 四位数的整数 |
| `yy` | 年份 | 两位数的整数 |
| `month` | 月份 | 从 `"January"` 到 `"December"` 的完整月份名称 |
| `mth` | 月份 | 从 0（1 月）到 11（12 月）的整数 |
| `dd` | 月中的天数 | 从 1 到 31 的整数 |
| `hh` | 一天中的小时 | 从 0（午夜）到 23（23:00）的整数 |
| `mm` | 小时中的分钟 | 从 0 到 59 的整数 |
| `ss` | 分钟中的秒数 | 从 0 到 59 的整数 |

| `ms` | 秒的毫秒数 | 从 0 到 999 的整数 | ### 了解 Date 对象

每当你在JavaScript中处理日期和时间时，你都在处理一个`Date`对象的实例。更准确地说，当你在JavaScript中处理`Date`对象时，你是在处理一个特定的时间点，精确到毫秒。`Date`对象绝不会是一个时间段，也不是一个在脚本运行时一直走的时钟。相反，`Date`对象是一个时间的快照，你可以用来提取它所记录的时间的具体信息：年份、月份、日期、小时等等。

#### 指定当前的日期和时间

`Date`对象最常见的用途是存储当前的日期和时间。你可以通过调用`Date()`函数来实现，这个函数是创建新的`Date`对象的构造函数。以下是一般格式：

`const dateToday = new Date();`  #### 指定任何日期和时间

如果你需要处理特定的日期或时间，需要使用`Date()`函数的参数。`Date()`函数语法有五种版本（请参考本章开头的参数列表）：

`const date = new Date("month dd, yyyy hh:mm:ss"); const date = new Date("month dd, yyyy"); const date = new Date(yyyy, mth, dd, hh, mm, ss); const date = new Date(yyyy, mth, dd); const date = new Date(ms);`

以下语句为每种语法提供了一个示例：

`const myDate = new Date("August 23, 2024 3:02:01"); const myDate = new Date("August 23, 2024"); const myDate = new Date(2024, 8, 23, 3, 2, 1); const myDate = new Date(2024, 8, 23); const myDate = new Date(1692763200000);`  ### 获取日期信息

当你的脚本简单地输出你存储在变量中的`Date`对象值时，结果并不是特别美观。如果你想以更吸引人的格式显示日期，或者想对日期进行算术运算，你需要深入挖掘`Date`对象，以提取特定信息，比如月份、年份、小时等。你可以使用在[表8-4](#c08-tbl-0004)中列出的`Date`对象方法来实现这一点。

[TABLE 8-4](#rc08-tbl-0004) `Date`对象方法，用于提取日期值

| `**方法语法**` | `**返回值**` |
| --- | --- |
| `date.getFullYear()` | 四位数的年份（1999，2000，等等） |
| `date.getMonth()` | 这一年的月份；从0（1月）到11（12月） |
| `date.getDate()` | 月份中的日期；从1到31 |
| `date.getDay()` | 一周中的天；从0（星期天）到6（星期六） |
| `date.getHours()` | 一天中的小时；从0（午夜）到23（11:00 PM） |
| `date.getMinutes()` | 这一小时的分钟；从0到59 |
| `date.getSeconds()` | 这一分钟的秒；从0到59 |
| `date.getMilliseconds()` | 这一秒的毫秒；从0到999 |

| `date.getTime()` | 自1970年1月1日格林威治时间以来的毫秒数 |  ### 设置日期

当你执行日期运算时，你通常需要更改现有``Date``对象的值。例如，一个电子商务脚本可能需要计算一个距离销售发生日期90天的日期。通常最简单的方法是创建一个``Date``对象，然后使用表达式或字面量值来更改年份、月份或日期的其他组成部分。你可以通过使用在[表8-5](#c08-tbl-0005)中列出的``Date``对象方法来实现这一点。

[TABLE 8-5](#rc08-tbl-0005) `Date`对象方法，设置日期值

| **方法语法** | **设置值** |
| --- | --- |
| ``date``.setFullYear(`yyyy`) | 四位数的年份（1999，2000，等等） |
| ``date``.setMonth(`mth`) | 这一年的月份；从0（1月）到11（12月） |
| ``date``.setDate(`dd`) | 月份中的日期；从1到31 |
| ``date``.setHours(`hh`) | 一天中的小时；从0（午夜）到23（11:00 PM） |
| ``date``.setMinutes(`mm`) | 小时中的分钟；从0到59 |
| ``date``.setSeconds(`ss`) | 分钟中的秒；从0到59 |
| ``date``.setMilliseconds(`ms`) | 秒中的毫秒；从0到999 |
| ``date``.setTime(`ms`) | 自1970年1月1日格林威治时间以来的毫秒数 |
