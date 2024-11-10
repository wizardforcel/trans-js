| 食谱 61 | 移除重复空格 |
| --- | --- |

### 任务

假设你有一个带有博客部分的网站，允许游客发布文章。作为审阅者，你注意到提交的文章中常常有一个常见错误：单词之间有双空格。为了解决这个问题，你希望创建一个函数，自动识别并纠正这个错误，将双空格替换为单空格。

一种简单直接的方法，将双空格转换为单空格，是使用 replaceAll() 方法，如下所示：

[part_3/removing_dup_spaces/removing_dup_spaces_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_3/removing_dup_spaces/removing_dup_spaces_ex1.js)

|   | **const** str = *"没有阳光的一天就像你知道的，夜晚。"*; |
| --- | --- |
|   |  |
|   | str.replaceAll(*" "*, *" "*); |
|   | *// → "没有阳光的一天就像你知道的，夜晚。"* |

你传递给 replaceAll() 的第一个参数是要被第二个参数替换的模式。虽然 replaceAll() 方法能有效地将双空格转换为单空格，但当单词之间有超过两个空格时，它会失效：

[part_3/removing_dup_spaces/removing_dup_spaces_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_3/removing_dup_spaces/removing_dup_spaces_ex2.js)

|   | **const** str = *"没有阳光的一天就像你知道的，夜晚。"*; |
| --- | --- |
|   |  |
|   | str.replaceAll(*" "*, *" "*); |
|   | *// → "没有阳光的一天就像你知道的，夜晚。"* |

你需要一个解决方案，可以替换重复的空格，而不仅仅是替换双空格。

### 解决方案

将输入字符串按空格分割，将结果子字符串存入数组，移除空数组项，然后使用单个空格将剩余元素组合起来：

[part_3/removing_dup_spaces/removing_dup_spaces_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_3/removing_dup_spaces/removing_dup_spaces_ex3.js)

|   | **function** replaceRepeatedSpaces(str) { |
| --- | --- |
|   | **return** str.split(*" "*).filter(i=>i).join(*" "*); |
|   | } |
|   |  |
|   | **const** str = *"没有阳光的一天就像，你知道的，夜晚。"*; |
|   |  |
|   | replaceRepeatedSpaces(str); |
|   | *// → "没有阳光的一天就像，你知道的，夜晚。"* |

这段代码接受一个字符串并移除连续空格，然后返回修改后的字符串，单词之间用一个空格分隔。

### 讨论

在这个函数中，我们将字符串拆分成单独单词的数组，使用 split(" ") 方法。然后我们使用 filter(i => i) 方法从结果数组中移除任何空的或伪值（falsy）的元素。filter() 方法创建一个新数组，包含所有通过回调函数定义的条件的原始数组元素。

记住，回调函数需要返回 true 或 false。在这种情况下，我们使用箭头函数直接返回数组中的值。由于空字符串是伪值（falsy），它会被隐式转换为 false 并从数组中移除。

| 什么是真值和伪值？ |
| --- |

| ![images/aside-icons/info.png](images/aside-icons/info.png) | 伪值（falsy）是当作为布尔值进行评估时被认为是 false 的值，而真值（truthy）是被认为是 true 的值。以下是 JavaScript 中被认为是伪值的值：

+   0 - 数字零

+   0n - BigInt 类型的零

+   "" - 空字符串

+   null - 表示没有任何值

+   undefined - 表示未定义的值

+   NaN - 代表 "不是一个数字"，表示无效或无法表示的值

所有其他值，包括非空字符串、非零数字、数组、对象和函数，都被认为是真值（truthy）。

经过过滤后，我们得到一个单词数组，可以使用单个空格将它们连接起来。如果需要处理大量文本，使用正则表达式可能比使用 JavaScript 方法稍微快一些。不过，对于大多数其他情况，性能差异可以忽略不计。

这是一个使用正则表达式实现解决方案的示例：

[part_3/removing_dup_spaces/removing_dup_spaces_ex4.js](http://media.pragprog.com/titles/fkjavascript/code/part_3/removing_dup_spaces/removing_dup_spaces_ex4.js)

|   | **function** replaceRepeatedSpaces(str) { |
| --- | --- |
|   | **return** str.replace(*/ +/g*,*" "*); |
|   | } |
|   |  |
|   | **const** str = *"没有阳光的一天就像，你知道的，夜晚。"*; |
|   |  |
|   | replaceRepeatedSpaces(str); |
|   | *// → "没有阳光的一天就像，你知道的，夜晚。"* |

需要记住的是，这个方法只替换空格字符，而不是所有空白字符。空格字符是你按下键盘空格键时产生的字符，而空白字符可以是空格、制表符、换行符、换页符、回车符或其他类似的字符。所以，虽然空格字符是空白字符的一种类型，但还有许多其他类型的空白字符。

当涉及到替换空白字符时，使用正则表达式可能是一个更好的选择，因为它更加简洁。你将在下一个方法中学习更多关于空白字符的内容。
