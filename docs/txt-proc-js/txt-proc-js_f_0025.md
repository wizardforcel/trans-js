| 配方 15 | 使用 Intl.NumberFormat() 为数字添加千位分隔符 |
| --- | --- |

### 任务

假设你希望为四位或更多位的数字添加千位分隔符。也许你正在从数据库中提取财务数据，以便在一个多语言出版的财经杂志中使用。

千位分隔符在许多不同的语言和国家中使用，以使大数字更易读。然而，作为千位分隔符使用的字符在不同的语言和文化中可能会有所不同。

举个例子，假设你有以下字符串：

|   | 1000000000 |
| --- | --- |

你希望将其格式化为：

|   | 1,000,000,000 |
| --- | --- |

你需要编写代码以编程方式为数字添加千位分隔符。

### 解决方案

使用 Intl.NumberFormat() 构造函数：

[part_1/adding_thousand_separators/adding_thousand_separators_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/adding_thousand_separators/adding_thousand_separators_ex1.js)

|   | **function** addThousandSeparator(num, locale) { |
| --- | --- |
|   | **const** numFormat = **new** Intl.NumberFormat(locale); |
|   | **return** numFormat.format(num); |
|   | } |
|   |  |
|   | addThousandSeparator(1000000000, *"en"*); |
|   | *// → "1,000,000,000"* |

在这段代码中，new Intl.NumberFormat() 创建了一个 NumberFormat 对象。然后，在该对象上调用 format() 方法，并传入“en”参数来指定使用英语。该函数返回一个格式化后的字符串，添加了千位分隔符，依据地区设置。

### 讨论

在数值中包含千位分隔符是一种简单的方式，可以增强数据的清晰度和视觉吸引力。但在继续之前，必须验证内容的类型。

逗号（,）在英语国家和许多其他国家通常用作千位分隔符。例如，10,000,000表示一千万。然而，在许多欧洲国家，如德国、希腊和意大利，使用句点（.）作为千位分隔符，而逗号（,）用作小数点分隔符。因此，要表示一千万，他们使用10.000.000。

在一些国家，使用其他符号或字符作为千位分隔符。例如，印度的数字系统使用类似逗号的符号，称为“分隔符”，来分隔数字组。而中文和日文的数字系统使用不同的字符来表示千、万、百万等大数。

通常，小于1000的数字不需要分隔符。另外，科学计数法表示的数字、邮政编码和电话号码通常不需要分隔符以保持清晰。因此，由这些数字组成的文档和数据可能不适合自动插入逗号。

本示例中的解决方案可以适应不同数字系统的千位分隔符。例如，为了按照德国语言习惯添加千位分隔符，你可以将“de-DE”（一个BCP-47语言标签）传递给NumberFormat()构造函数，如下所示：

[part_1/adding_thousand_separators/adding_thousand_separators_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/adding_thousand_separators/adding_thousand_separators_ex2.js)

|   | **function** addThousandSeparator(num, locale) { |
| --- | --- |
|   | **const** numFormat = **new** Intl.NumberFormat(locale); |
|   | **return** numFormat.format(num); |
|   | } |
|   |  |
|   | addThousandSeparator(1000000000, *"de-DE"*); |
|   | *// → "1.000.000.000"* |

请记住，千位分隔符并不是通用的，不同国家和书写语言中可能有所不同。同时，具体的格式化约定也可能根据上下文有所变化，例如在科学记数法中，通常不使用逗号。要从字符串中提取带有千位分隔符的数字，请参见配方69，[ *匹配带有千位分隔符的数字*](f_0081.xhtml#rcp.matching_thousand_separators)。
