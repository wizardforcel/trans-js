| 配方 67 | 从文件名中剥离无效字符 |
| --- | --- |

### 任务

假设你经营一个文件托管服务。为了确保顺畅的下载过程，应该避免在提供下载的文件名中使用某些字符。在iOS和macOS中，文件名不能包含冒号（:），而Android和Windows操作系统则有更严格的限制，不允许在文件名中使用<, >, :, ", /, \, |, ?, 和*。

原因是操作系统使用这些字符来将路径括起来，用引号标记驱动器和目录，表示通配符和命令行重定向等。此外，Windows有一些特定的保留名称，用于内部目的，因此不能将它们用作文件名。

这些保留名称如下：

|   | LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, |
| --- | --- |
|   | COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, |
|   | CON, PRN, AUX, NUL |

当尝试下载文件时，如果文件名中包含无效字符，Windows会自动将这些字符替换为下划线，而不会向用户发出任何警告。为避免此类问题，你可以创建一个脚本，检测文件名中存在的问题字符，并在继续下载之前通知用户解决这些问题。

### 解决方案

为了提高可读性和可维护性，最好分别测试每个字符和单词的列表，而不是将它们合并并使用单一的正则表达式。创建一个接受文件名作为输入的函数，逐一测试每个正则表达式，并在测试通过时返回true：

[part_3/striping_invalid_characters/striping_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_3/striping_invalid_characters/striping_ex1.js)

|   | **let** reservedNames = |
| --- | --- |
|   | *`LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9,* |
|   | *COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9,* |
|   | *CON, PRN, AUX, NUL`*; |
|   |  |
|   | *// 从reservedNames字符串创建一个数组* |
|   | reservedNames = reservedNames.split(*/,**\s**/*); |
|   |  |
|   | **function** isValidFilename(name) { |
|   | **const** re1 = **new** RegExp(*`^(*${reservedNames.join(*"&#124;"*)}*)$`*, *"i"*); |
|   | **const** re2 = */**[**<>:"**/\\**&#124;?***]**/*; |
|   | **return** !(re1.test(name) &#124;&#124; re2.test(name)); |
|   | } |
|   |  |
|   | isValidFilename(*"COM1"*); *// → false* |
|   | isValidFilename(*"com1"*); *// → false* |
|   | isValidFilename(*"com1_"*); *// → true* |
|   | isValidFilename(*"@com1"*); *// → true* |
|   | isValidFilename(*"]-:"*); *// → false* |
|   | isValidFilename(*"<myfile>"*); *// → false* |

成功！

### 讨论

首先，准备一个包含无效字符/名称的数组。如果你像我一样不想通过键入来创建数组，可以使用split()方法将保留名称分开并存储到数组中。结果如下：

|   | let reservedNames = |
| --- | --- |
|   | `LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, |
|   | COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, |
|   | CON, PRN, AUX, NUL`; |
|   |  |
|   | reservedNames.split(/,\s/); |
|   | // → ["LPT1", "LPT2", "LPT3", "LPT4", "LPT5", "LPT6", "LPT7", "LPT8", "LPT9", |
|   | // "COM1", "COM2", "COM3", "COM4", "COM5", "COM6", "COM7", "COM8", "COM9", |
|   | // "CON", "PRN", "AUX", "NUL"] |

在isValidFilename()函数内部，我们使用RegExp构造函数将结果数组中的项与管道符连接，形成类似LPT1|LPT2|LPT3...的交替表达式：

如果你不想动态创建模式，可以避免逐个输入每个名称。相反，利用字符类定义一个范围：

|   | /^(LPT[1-9]&#124;COM[1-9]&#124;CON&#124;PRN&#124;AUX&#124;NUL)$/i |
| --- | --- |

只有当文件名包含这些词语且没有额外字符时，才是无效的。例如，“LPT1”是一个无效的文件名，但“LPT1z”或“ALPT1”则不是。模式开头的插入符号（^）表示字符串的开始，并确保没有其他字符出现在目标字符串匹配之前。类似地，美元符号（$）表示字符串的结束。

第二个模式列出了保留字符，包含的只有九个字符。因此，使用方括号[]将它们包含在字符类中就足够了。字符类匹配方括号中出现的任何单个字符，因此我们可以检查给定字符串中是否包含这些字符。

在字符类内部，反斜杠被视为元字符，因此需要用另一个反斜杠进行转义。但所有其他字符都被视为字面字符。

文件名可能包含操作系统或文件系统不允许的字符。通过使用正则表达式模式，我们可以检测这些字符，并提供一个无问题的下载过程。
