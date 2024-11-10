## replaceAll()

replaceAll() 方法在设置了全局标志时输出与 replace() 相同的结果。对比：

[appendix/methods/methods_ex13.js](http://media.pragprog.com/titles/fkjavascript/code/appendix/methods/methods_ex13.js)

|   | **const** str = *"$5, $10, $20"*; |
| --- | --- |
|   | **const** re = */**\$**/g*; |
|   |  |
|   | console.log(str.replace(re, *"€"*)); *// → €5, €10, €20* |
|   | console.log(str.replaceAll(re, *"€"*)); *// → €5, €10, €20* |

结果是，调用 replaceAll() 方法似乎并不会比调用 replace() 方法带来更多好处。这两者之间的主要区别在于，当模式是字符串而不是正则表达式时，replaceAll() 如何处理替换：

[appendix/methods/methods_ex14.js](http://media.pragprog.com/titles/fkjavascript/code/appendix/methods/methods_ex14.js)

|   | **const** str = *"$5, $10, $20"*; |
| --- | --- |
|   | **const** searchStr = *"$"*; |
|   |  |
|   | console.log(str.replace(searchStr, *"€"*)); *// → €5, $10, $20* |
|   | console.log(str.replaceAll(searchStr, *"€"*)); *// → €5, €10, €20* |

replaceAll() 方法会替换所有子字符串的实例，而 replace() 方法在替换第一个子字符串后就停止搜索。请记住，replaceAll() 总是期望正则表达式模式中包含全局标志；否则，它会抛出错误：

[appendix/methods/methods_ex15.js](http://media.pragprog.com/titles/fkjavascript/code/appendix/methods/methods_ex15.js)

|   | **const** str = *"$5, $10, $20"*; |
| --- | --- |
|   | **const** re = */**\$**/*; |
|   |  |
|   | str.replaceAll(re, *"€"*); |
|   | *// → TypeError: String.prototype.replaceAll called with a non-global RegExp* |
|   | *// 参数* |
| 特殊替换模式 |
| --- |
| ![images/aside-icons/note.png](images/aside-icons/note.png) | replace() 和 replaceAll() 的第二个参数支持一组特殊模式，可以让你引用匹配的子字符串的不同部分。请参见第 34 条，[*使用特殊替换模式*](f_0045.xhtml#rcp.replacement_patterns)。 |
