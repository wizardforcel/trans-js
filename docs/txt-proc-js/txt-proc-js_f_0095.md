## replace()

replace() 方法用给定的字符串替换匹配项。模式可以是一个字符串或正则表达式：

[appendix/methods/methods_ex11.js](http://media.pragprog.com/titles/fkjavascript/code/appendix/methods/methods_ex11.js)

|   | **const** str = *"fish and chips"*; |
| --- | --- |
|   |  |
|   | *// 使用字符串作为参数* |
|   | console.log(str.replace(*"and"*, *"&"*)); *// → fish & chips* |
|   |  |
|   | *// 使用正则表达式作为参数* |
|   | console.log(str.replace(*/and/*, *"&"*)); *// → fish & chips* |

如果设置了全局标志，该方法会替换字符串中找到的每一个匹配项：

[appendix/methods/methods_ex12.js](http://media.pragprog.com/titles/fkjavascript/code/appendix/methods/methods_ex12.js)

|   | **const** str = *"$5, $10, $20"*; |
| --- | --- |
|   | **const** re = */**\$**/g*; |
|   |  |
|   | console.log(str.replace(re, *"€"*)); *// → €5, €10, €20* |
