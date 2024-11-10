## split()

split() 方法将一个字符串拆分成子字符串并将它们作为数组返回。第一个参数可以是字符串或正则表达式，用于指定拆分的位置。第二个参数限制了返回数组中元素的数量。以下是一个示例：

[appendix/methods/methods_ex16.js](http://media.pragprog.com/titles/fkjavascript/code/appendix/methods/methods_ex16.js)

|   | **const** str = *"a b c"*; |
| --- | --- |
|   |  |
|   | console.log(str.split(*" "*)); *// → ["a", "b", "c"]* |
|   | console.log(str.split(*/**\s**/*, 2)); *// → ["a", "b"]* |
| 索引 |
| --- |
| ![images/aside-icons/info.png](images/aside-icons/info.png) | 如果在正则表达式中设置 d 标志，你将在 exec()、match() 和 matchAll() 的结果中访问到 indices 属性。有关 indices 的更多信息，请参见第 40 章，[*使用 d 标志生成匹配的索引*](f_0051.xhtml#rcp.flag_d)。 |
