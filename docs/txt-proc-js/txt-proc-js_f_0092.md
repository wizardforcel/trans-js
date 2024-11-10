## match()

match() 方法返回一个类似于 exec() 的数组。你可能已经注意到这两个方法之间的相似性。考虑以下示例：

[appendix/methods/methods_ex4.js](http://media.pragprog.com/titles/fkjavascript/code/appendix/methods/methods_ex4.js)

|   | **const** str = *"大约100英尺"*; |
| --- | --- |
|   | **const** re = */**(\d**+**)**英尺/*; |
|   |  |
|   | console.log(str.match(re)); |
|   | *// → ["100英尺", "100", index: 6, input: "大约100英尺", groups: undefined]* |
|   |  |
|   | console.log(re.exec(str)); |
|   | *// → ["100英尺", "100", index: 6, input: "大约100英尺", groups: undefined]* |

exec() 和 match() 返回相同的结果。只有在设置全局标志（g）时，输出才会有所不同：

[appendix/methods/methods_ex5.js](http://media.pragprog.com/titles/fkjavascript/code/appendix/methods/methods_ex5.js)

|   | **const** str = *"9英尺, 10英尺, 11英尺"*; |
| --- | --- |
|   | **const** re = */**(\d\d)**英尺/g*; |
|   |  |
|   | console.log(str.match(re)); |
|   | *// → ["10英尺", "11英尺"]* |
|   |  |
|   | console.log(re.exec(str)); |
|   | *// → ["10英尺", "10", index: 5, input: "9英尺, 10英尺, 11英尺", groups: undefined]* |

设置全局标志时，match() 返回一个仅包含匹配子串的数组，并不会包括捕获组、索引和其他属性。

请记住，默认情况下，match() 会忽略你为 lastIndex 设置的值。要指定搜索的起始位置，必须使用粘性标志（参见配方44，[*使用 y 标志从特定索引开始搜索*](f_0055.xhtml#rcp.flag_y)）。
