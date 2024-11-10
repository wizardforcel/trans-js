## test()

test()方法返回一个布尔值，指示给定字符串中是否存在某个模式。例如，以下模式检查字符串是否包含子串“day”：

[appendix/methods/methods_ex8.js](http://media.pragprog.com/titles/fkjavascript/code/appendix/methods/methods_ex8.js)

|   | **const** str = *"12天"*; |
| --- | --- |
|   | **const** re = */day/*; |
|   |  |
|   | console.log(re.test(str)); *// → true* |

一些正则表达式方法，如test()和exec()，使用lastIndex的值作为开始位置来搜索字符串。如果匹配成功，test()返回true，并更新正则表达式对象的lastIndex属性。以下是一个示例：

[appendix/methods/methods_ex9.js](http://media.pragprog.com/titles/fkjavascript/code/appendix/methods/methods_ex9.js)

| 1:  | **const** str = *"10, 20, 30"*; |
| --- | --- |
| -  | **const** re = */**\d\d**/g*; *// 匹配两个连续的数字* |
| -  |  |
| -  | console.log(re.test(str)); *// → true* |
| 5:  | console.log(re.lastIndex); *// → 2* |
| -  |  |
| -  | console.log(re.test(str)); *// → true* |
| -  | console.log(re.lastIndex); *// → 6* |
| -  |  |
| 10:  | *// lastIndex 可写* |
| -  | *// 所以你可以手动设置它* |
| -  | re.lastIndex = 11; |
| -  | console.log(re.test(str)); *// → false* |
| -  | console.log(re.lastIndex); *// → 0* |

注意第13行，当test()在索引11找不到匹配项时返回false。发生这种情况时，方法会将lastIndex重置为0。请记住，必须设置全局标志（g）才能使其生效。
