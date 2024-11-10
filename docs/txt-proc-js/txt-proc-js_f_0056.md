| 食谱 45 | 修改现有的正则表达式字面量 |
| --- | --- |

### 任务

假设你想要修改你队友的正则表达式字面量，以便在代码的其他部分使用。你不想改变原始的正则表达式，因为它已经通过了所有的测试，适用于它最初的用途。

你需要一个解决方案，能够修改现有正则表达式字面量的副本。

### 解决方案

使用 `source` 和 `flags` 属性来获取原始正则表达式的部分。然后使用这些部分构造一个新的 `RegExp` 对象：

[part_2/modifying_regex/modifying_regex_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/modifying_regex/modifying_regex_ex1.js)

|   | *// 匹配带有 .png 扩展名的文件名的模式* |
| --- | --- |
|   | **const** origRegex = */**\b(\w**+**)\.**png**\b**/*; |
|   |  |
|   | *// 匹配带有 .png 或 .PNG 扩展名的文件名的模式* |
|   | **const** newRegex = **new** RegExp(origRegex.source, origRegex.flags + *"i"*); |

太棒了！你已经成功将 `i` 标志添加到正则表达式模式中。

### 讨论

JavaScript 提供了 `flags` 属性，用于读取正则表达式中使用的所有标志：

[part_2/modifying_regex/modifying_regex_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/modifying_regex/modifying_regex_ex2.js)

|   | **const** re1 = */**\b(\w**+**)\.**png**\b**/ig*u; |
| --- | --- |
|   | **const** re2 = */**\b(\w**+**)\.**png**\b**/*; |
|   |  |
|   | console.log(re1.flags); *// → giu* |
|   | console.log(re2.flags); *// → ""* |

注意当读取标志时，标志的顺序是如何变化的。`flags` 属性总是忽略原始模式的顺序，并以固定顺序列出它们：“gimuy”。如果模式没有标志，返回值将是一个空字符串。

同样，`source` 属性获取我们被正斜杠包围的模式：

[part_2/modifying_regex/modifying_regex_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/modifying_regex/modifying_regex_ex3.js)

|   | **const** re = */**\b(\w**+**)\.**png**\b**/ig*u; |
| --- | --- |
|   |  |
|   | console.log(re.source); *// → \b(\w+)\.png\b* |

我们还可以检查特定的标志是否应用于正则表达式。例如，要查看 `global` 标志 `g` 是否设置，我们可以读取 `global` 属性：

[part_2/modifying_regex/modifying_regex_ex4.js](http://media.pragprog.com/titles/fkjavascript/code/part_2/modifying_regex/modifying_regex_ex4.js)

|   | **const** re1 = */**\b(\w**+**)\.**png**\b**/ig*; |
| --- | --- |
|   | **const** re2 = */**\b(\w**+**)\.**png**\b**/*u; |
|   |  |
|   | console.log(re1.global); *// → true* |
|   | console.log(re2.global); *// → false* |

下表列出了所有支持的标志及其对应的属性。请注意，这些属性都是只读的：

| 标志 | 对应的属性 |
| --- | --- |
| d | hasIndices |
| g | global |
| i | ignoreCase |
| m | multiline |
| s | dotAll |
| u | unicode |
| y | sticky |

使用 `flags` 属性来获取正则表达式对象的标志。使用 `source` 属性来获取正则表达式对象的源文本。记住，`source` 返回的值不包括两侧的正斜杠或标志。这个属性在你想从现有模式构建新模式时非常有用。
