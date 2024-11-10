| 配方 17 | 使用 charAt() 确定字母大小写 |
| --- | --- |

### 任务

假设你有一个表单，要求用户输入他们的昵称。有些用户可能会选择用小写字母输入昵称，所以你的应用程序不应该自动将昵称首字母大写。但也有一些用户可能在输入时比较随意，打算让他们的名字首字母大写。

在这种情况下，你需要通知用户他们的昵称将按原样存储和显示。因此，您的应用需要能够识别昵称第一个字符的字母大小写。

### 解决方案

使用严格不等于运算符（!==）将字符串的第一个字符（索引 0）与其小写形式进行比较。如果它们不相等，说明字符串以大写字母开头：

[part_1/determining_letter_case/charAt_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/determining_letter_case/charAt_ex1.js)

|   | **function** isCapital(str) { |
| --- | --- |
|   | **return** str.charAt(0) !== str.charAt(0).toLowerCase(); |
|   | } |
|   |  |
|   | isCapital(*"Dave"*); *// → true* |
|   | isCapital(*"dave"*); *// → false* |

成功！现在你能够确定一个单词第一个字符的字母大小写了。

### 讨论

这个配方中的函数会在输入字符串的第一个字符是大写字母时返回 true，否则返回 false。为了获取输入字符串的第一个字母，我们使用 charAt() 方法。该方法接受一个索引数字作为参数，并返回字符串中该位置的字符。例如，"Hello".charAt(1) 返回 "Hello" 中的第二个字符 "e"。

你可能会想，为什么不使用严格相等运算符（===）来将字符与其大写形式进行比较呢？

为了理解原因，让我们用 === 重写这个例子：

[part_1/determining_letter_case/charAt_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/determining_letter_case/charAt_ex2.js)

|   | *// 不要使用此代码* |
| --- | --- |

![images/charAt_ex2.png](images/charAt_ex2.png)

这个版本的函数即使输入字符串以数字开头（例如“1990Dave”），也会返回 `true`。`toUpperCase()` 对于输入字符串中没有大写版本的字符没有影响。因此，在这个示例中，我们将“1”和将其转换为大写后的“1”进行比较。结果，比较返回 `true`。

这个函数对于像希伯来语和阿拉伯语这样的语言也会返回 `true`，因为这些语言没有大写和小写字母。

在使用 `charAt()` 处理具有补充字符的特定语言（如中文）时，需要注意一些问题。为了能够表示这些字符，JavaScript 必须在字符串中分配更多的“空间”，这会导致 `charAt()` 失败：

[part_1/determining_letter_case/charAt_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/determining_letter_case/charAt_ex3.js)

|   | *// 注意 charAt() 的返回值并不是* |
| --- | --- |
|   | *// 在索引 0 和索引 1 处可识别* |

![images/charAt_ex3.png](images/charAt_ex3.png)

JavaScript 使用 UTF-16 编码点来表示字符，大多数字符需要一个编码点。例如，字符“F”被分配了 U+0046 的编码点。

然而，有时一个字符是由多个编码点组成的。在这种情况下，中文字符由两个 Unicode 编码点组成。第一个编码点的值是 U+d846，第二个编码点的值是 U+df10。你可以通过在每个编码前加上 `\u` 并将两个编码对放在一个字符串中来确认这一点：

![images/charAt_ex4.png](images/charAt_ex4.png)

这对中的任何一对都不能单独对应一个可打印字符，因此 `charAt()` 方法无法在索引 0 或索引 1 处返回有效字符。第四个 `console.log()` 方法尝试获取索引 2 处的字符，但由于该位置没有字符，它返回了一个空字符串。

当你需要获取特定索引处的字符时，使用`charAt()`方法，但要小心包含补充字符的语言，因为它们可能会导致代码出错。幸运的是，JavaScript还有另一种方法可以帮助你处理补充字符，你将在下一个例子中学习到。要了解更多关于Unicode的信息，请参阅附录1，[*什么是Unicode？*](f_0088.xhtml#apx1)。
