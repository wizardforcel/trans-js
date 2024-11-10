## search()

search() 方法对字符串执行搜索，并返回一个整数，表示第一个匹配项的索引。如果未找到匹配项，返回值将是 -1：

[appendix/methods/methods_ex10.js](http://media.pragprog.com/titles/fkjavascript/code/appendix/methods/methods_ex10.js)

|   | **const** str = *"Eat well, stay fit, die anyway."*; |
| --- | --- |
|   |  |
|   | *// 使用字符串作为模式* |
|   | console.log(str.search(*"fit"*)); *// → 15* |
|   |  |
|   | *// 使用正则表达式作为模式* |
|   | console.log(str.search(*/fit/*)); *// → 15* |

与 exec() 或 test() 不同，search() 方法不支持全局标志，并且忽略 lastIndex 属性。这意味着它总是从字符串的开头开始执行搜索，并返回第一个匹配项的索引。
