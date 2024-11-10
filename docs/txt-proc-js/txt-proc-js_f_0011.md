| 食谱 1 | 使用 `typeof` 操作符确定一个值是否是字符串 |
| --- | --- |

### 任务

在 JavaScript 中，你经常需要验证一个值是否为字符串。例如，在下一个食谱中，我们将构建一个函数，用来搜索字符串中的多个单词。在将值传递给函数之前，你需要检查它是否是字符串。任何其他数据类型，如数字或布尔值，都会导致函数抛出错误。

在本书中，你会多次看到类似的函数，因此这是一个很好的起点。

### 解决方案

使用 `typeof` 操作符：

[part_1/determining_valid_strings/typeof_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/determining_valid_strings/typeof_ex1.js)

|   | **function** isString(value) { |
| --- | --- |
|   | **return** **typeof** value === *"string"*; |
|   | } |
|   |  |
|   | isString(123); *// → false* |
|   | isString(*"abc"*); *// → true* |

`typeof` 操作符返回一个字符串，表示值的类型。

### 讨论

在 JavaScript 中，你可以使用单引号、双引号或反引号来创建字符串字面量：

[part_1/determining_valid_strings/typeof_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/determining_valid_strings/typeof_ex2.js)

|   | **let** str1 = *"string"*; |
| --- | --- |
|   | **let** str2 = *'string'*; |
|   | **let** str3 = *`string`*; |

所以，用引号或反引号括起来的数字不再是数字，而是字符串。如果你不使用 `new` 关键字，还可以使用 `String()` 构造函数来创建字符串：

[part_1/determining_valid_strings/typeof_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/determining_valid_strings/typeof_ex3.js)

|   | String(123); *// → "123"* |
| --- | --- |

在字符串中，每个字符占据一个位置。索引 0 对应第一个字符，索引 1 对应第二个字符，依此类推。所以，要获取字符串中的第二个字符，可以输入 `str[1]`：

[part_1/determining_valid_strings/typeof_ex4.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/determining_valid_strings/typeof_ex4.js)

|   | **let** str = *"string"*; |
| --- | --- |
|   |  |
|   | console.log(str[1]); *// → t* |

接下来，我们将通过构建一个函数，开始探索 JavaScript 文本处理方法的领域，该函数检查一个字符串是否包含一组单词。
