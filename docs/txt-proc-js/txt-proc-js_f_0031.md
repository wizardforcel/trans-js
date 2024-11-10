| 食谱 21 | 使用normalize()方法使不兼容字符统一 |
| --- | --- |

### 任务

假设你有一个烹饪应用程序，并且想要添加一个功能来根据烹饪方法对食谱进行排序。你开发的代码在排序蒸煮和烤制等方法的食谱时表现良好。然而，当涉及到煎炒时，代码无法识别某些食谱。

在调查问题后，你会发现代码有时无法匹配“sautéing”这个词，尽管字符看起来是相同的：

[part_1/equalizing_characters/normalize_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/equalizing_characters/normalize_ex1.js)

|   | *// 请注意字符串的长度* |
| --- | --- |

![images/normalize_ex1.png](images/normalize_ex1.png)

方法中的“é”字符的代码点是U+00E9，而关键字中的“é”由两个代码点组成：U+0065和U+0301。因此，严格相等运算符（===）认为它们不相等。

代码点数量的差异并不是代码可能失败的唯一原因。某些字符虽然长度相同，但使用了两个不同的代码点进行编码，这也可能导致代码出现问题。

例如，字符“Å”可以被编码为U+212B ANGSTROM SIGN或U+00C5 LATIN CAPITAL LETTER A WITH RING ABOVE。这两个字符在JavaScript中不相等，除非你将它们规范化。

### 解决方案

使用normalize()方法在比较字符串之前将它们转换为规范化形式：

[part_1/equalizing_characters/normalize_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/equalizing_characters/normalize_ex2.js)

|   | *// 解决方案* |
| --- | --- |

![images/normalize_ex2.png](images/normalize_ex2.png)

这个函数可以让我们确定两个字符串是否相等，考虑到它们的Unicode表示之间的任何差异。

### 讨论

可以用多种方式表示的字符使文本处理变得更加困难。幸运的是，Unicode标准提供了一种文本规范化程序，将字符串转换为可以直接比较身份的形式。

在areEqual()函数内部，我们使用normalize()方法将两个字符串转换为规范化形式，采用规范化形式规范合成（NFC）算法。该算法确保任何具有多个代码点的Unicode字符都以其组合形式表示。

我们可以传递三个其他参数给normalize()，稍后我们将详细讨论。使用的格式取决于你的程序需求，但NFC通常是处理普通文本的更好选择，因为它与从旧版编码转换过来的字符更兼容。

除非你是那些不得不支持IE11的可怜人之一，否则在这里你不需要polyfill。幸运的是，所有现代浏览器都支持normalize()。^([[21]](f_0032.xhtml#FOOTNOTE-21)) 规范化后，我们使用===运算符来比较这两个字符串，如果它们相等则返回true。

我们可以根据规范等价性或兼容性来规范化字符串。传递给normalize()的参数决定了Unicode规范化的形式：

+   规范化形式D（NFD）：规范分解

+   规范化形式C（NFC）：规范分解，随后是规范合成

+   规范化形式KD（NFKD）：兼容性分解

+   规范化形式KC（NFKC）：兼容性分解，随后是规范合成

当两个字符具有不同的代码点但以相同方式呈现时，它们是规范等价的，就像我们示例中的“é”一样。当我们说NFC执行规范合成时，意味着它将字符的代码点合并成一个单一的代码点，因此由U+0065和U+0301组成的“é”变成了由U+00E9组成的“é”。规范分解则是相反的过程。

现在，如果两个字符具有不同的外观和代码点，但具有相同的含义，它们被归类为兼容等价。请看下面的表格，了解两种等价序列的形式：

![images/Compatibly_table.png](images/Compatibly_table.png)

当我们规范化一个字符串时，我们告诉程序选择这些等效编码之一，以便字符要么全部组合，要么全部分解。注意有些单元格中的箭头只指向右边。这意味着我们可以将一个字符转换为其兼容分解形式，但不能反向转换。因此，在使用这种转换时我们应该小心：如果我们失去对源文本的访问，字符的原始形式将永远丢失，因为没有函数可以将文本恢复为组合形式。

请看以下代码：

[part_1/equalizing_characters/normalize_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/equalizing_characters/normalize_ex3.js)

|   | **const** str1 = *"***\***u00E9"*; *// é* |
| --- | --- |
|   | **const** str2 = *"***\***u0065***\***u0301"*; *// é* |
|   |  |
|   | console.log(str1 === str2); *// → false* |
|   |  |
|   | *// normalize str1* |
|   | **const** str1norm = str1.normalize(*"NFD"*); *// \u0065\u0301* |
|   |  |
|   | console.log(str1norm === str2); *// → true* |

在这段代码中，我们正在将 str1 中的任何规范组合替换为其分解形式。如果我们将 NFC 传递给 normalize()，该方法则执行相反的操作：

[part_1/equalizing_characters/normalize_ex4.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/equalizing_characters/normalize_ex4.js)

|   | **const** str1 = *"***\***u00E9"*; *// é* |
| --- | --- |
|   | **const** str2 = *"***\***u0065***\***u0301"*; *// é* |
|   |  |
|   | *// normalize str2* |
|   | **const** str2norm = str2.normalize(*"NFC"*); *// \u00E9* |
|   |  |
|   | console.log(str2norm === str1); *// → true* |
| 默认参数 |
| --- |
| ![images/aside-icons/tip.png](images/aside-icons/tip.png) | 如果你没有传递任何参数给 normalize()，它将使用 NFC。 |

兼容规范化有两种形式：NFKD 和 NFKC。转换为 NFKD 的工作原理类似于 NFD。它将字符串中的规范组合替换为其分解形式。此外，它还将任何兼容组合替换为其分解形式。

如果字形只是另一个字形的兼容组合，那么使用 NFD 或 NFC 进行规范化不会改变它。另一方面，NFKD 和 NFKC 都会将字形替换为其兼容的分解形式：

[part_1/equalizing_characters/normalize_ex6.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/equalizing_characters/normalize_ex6.js)

|   | **const** str1 = *"⑥"*; *// \u2465* |
| --- | --- |
|   |  |
|   | console.log(str1.normalize(*"NFD"*)); *// → ⑥ (\u2465)* |
|   | console.log(str1.normalize(*"NFC"*)); *// → ⑥ (\u2465)* |
|   | console.log(str1.normalize(*"NFKD"*)); *// → 6 (\u0036)* |
|   | console.log(str1.normalize(*"NFKC"*)); *// → 6 (\u0036)* |
|   |  |
|   | **const** str2 = *"⁶"*; *// \u2076* |
|   |  |
|   | console.log(str2.normalize(*"NFD"*)); *// → ⁶ (\u2076)* |
|   | console.log(str2.normalize(*"NFC"*)); *// → ⁶ (\u2076)* |
|   | console.log(str2.normalize(*"NFKD"*)); *// → 6 (\u0036)* |
|   | console.log(str2.normalize(*"NFKC"*)); *// → 6 (\u0036)* |

在这段代码中，转换为 NFD 或 NFC 不会影响 str1 和 str2，因为这些字符串是兼容组合，而不是规范组合。有趣的是，转换为 NFKD 和 NFKC 会产生相同的结果，因为 NFKC 使用兼容分解作为规范组合的基础。在这种情况下，字符没有规范的组合形式，因此它只是转换为兼容分解。

当字形是规范组合，且与另一个字形兼容时，NFKC 和 NFKD 之间的差异更加明显。考虑以下代码：

[part_1/equalizing_characters/normalize_ex7.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/equalizing_characters/normalize_ex7.js)

|   | **const** str = *"ẛ"*; *// \u1E9B* |
| --- | --- |
|   |  |
|   | console.log(str.normalize(*"NFD"*)); *// → ẛ (\u017F\u0307)* |
|   | console.log(str.normalize(*"NFC"*)); *// → ẛ (\u1E9B)* |
|   |  |
|   | console.log(str.normalize(*"NFKD"*)); *// → ṡ (\u0073\u0307)* |
|   | console.log(str.normalize(*"NFKC"*)); *// → ṡ (\u1E61)* |

正如我们所说，NFKC 使用兼容性分解作为规范组合的基础。\u1E9B 的兼容性分解是 \u0073\u0307，而 \u0073\u0307 的规范组合是 \u1E61。

请记住，在存储或处理文本之前，务必进行文本规范化，以避免可能的陷阱。但在使用规范化形式 KD 和 KC 时要小心，因为它们会丢失可能对文本语义至关重要的格式区分。因此，您不应该盲目地将它们应用于任意文本。对于一般文本来说，NFC 通常是更好的选择。
