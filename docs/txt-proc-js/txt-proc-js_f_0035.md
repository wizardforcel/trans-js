| 配方 24 | 使用 ^ 和 $ 断言字符串的开始或结束 |
| --- | --- |

### 任务

假设你在应用程序中有一个输入字段，允许客户输入他们的订单号并跟踪包裹。你想确保用户输入的是数字，然后再在数据库中查询。如果你对正则表达式稍微熟悉，你会知道，要匹配数字，可以使用 \d。而要匹配一个或多个数字，可以在其后加上加号，像这样：

[part_2/caret_and_dollar/cnd_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/caret_and_dollar/cnd_ex1.js)

|   | **常量** input = *"8751409"*; |
| --- | --- |
|   |  |
|   | **函数** verifyDigits(input) { |
|   | **常量** re = */**\d**+/*; |
|   | **返回** re.test(input); |
|   | } |
|   |  |
|   | verifyDigits(input); *// → true* |

这个正则表达式会像你预期的那样匹配“8751409”。但是它也会匹配像“123abc”或“abc123abc”这样的字符串：

[part_2/caret_and_dollar/cnd_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/caret_and_dollar/cnd_ex2.js)

|   | **常量** input = *"abc123abc"*; |
| --- | --- |
|   |  |
|   | **函数** verifyDigits(input) { |
|   | **常量** re = */**\d**+/*; |
|   | **返回** re.test(input); |
|   | } |
|   |  |
|   | verifyDigits(input); *// → true* |

那么发生了什么呢？你的模式告诉正则表达式引擎匹配一个或多个数字，但它没有告诉它在哪个位置匹配。所以，它成功地匹配了字符串中间的数字，并返回true，即使字符串中还有其他不匹配的字符。

你需要的是一种方法，来指定正则表达式中字符串的开始和结束位置，以便它不会匹配其他字符。

### 解决方案

在模式的开头加上插入符号（^），在结尾加上美元符号（$），像这样：

[part_2/caret_and_dollar/cnd_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/caret_and_dollar/cnd_ex3.js)

|   | **常量** digits = *"8757409"*; |
| --- | --- |
|   | **常量** digits_and_letters = *"875abc"*; |
|   |  |
|   | **函数** verifyDigits(input) { |
|   | **const** re = */^**\d**+$/*; |
|   | **return** re.test(input); |
|   | } |
|   |  |
|   | console.log(verifyDigits(digits)); *// → true* |
|   | console.log(verifyDigits(digits_and_letters)); *// → false* |

正则表达式现在可以精确匹配你所寻找的短语！插入符号（`^`）断言字符串的开始位置，美元符号（`$`）断言字符串的结束位置。

### 讨论

不要将 `^` 和 `$` 与 startsWith() 和 endsWith() 混淆。`^` 和 `$` 被称为零宽度断言，这意味着它们不匹配实际字符，而是匹配文本中的位置。因此，`/^Hello$/` 中的插入符号并不会匹配输入中的 "H"，而是断言在文字 "Hello" 之前没有其他字符。

同样，美元符号（`$`）并不匹配任何字符，它只是确保位置是在字符串的末尾。如果你想匹配字符串开头或结尾的特定字符，你应该使用 JavaScript 的 startsWith() 和 endsWith() 方法（参见配方 3，[*使用 startsWith() 和 endsWith() 匹配字符串的开始或结束*](f_0013.xhtml#rcp.start_end)）。

| 多行标志改变规则 |
| --- |
| ![images/aside-icons/warning.png](images/aside-icons/warning.png) | 如果你使用多行标志，`$` 还会匹配换行符前的位置，而 `^` 也会匹配换行符后的位置。我们将在配方 41 中讲解多行标志，[*强制 `^` 和 `$` 匹配行的开始和结束位置，使用 m 标志*](f_0052.xhtml#rcp.flag_m)。 |

使用 `^` 和 `$` 来断言字符串的开始或结束位置，但在使用多行标志时要小心，因为它会改变这些符号的工作方式。

正则表达式还提供了一种语法用于匹配整个单词：`\b`。这种语法与 `^` 和 `$` 一起被称为边界。接下来的配方会告诉你有关单词边界（`\b`）的所有信息。
