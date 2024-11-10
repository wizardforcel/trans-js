## exec()

exec() 方法在字符串上执行搜索。如果找到匹配项，它将返回一个包含搜索结果的数组。如果没有找到，它将返回 null。以下是一个例子：

[appendix/methods/methods_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/appendix/methods/methods_ex1.js)

|   | **const** str = *"About 100ft"*; |
| --- | --- |
|   | **const** re = */**(\d**+**)**ft/*; |
|   |  |
|   | console.log(re.exec(str)); |
|   | *// → ["100ft", "100", index: 6, input: "About 100ft", groups: undefined]* |

生成的数组将匹配的字符串作为第一个元素。如果匹配中有捕获组，它们将按从索引1开始的顺序列出。该数组还具有三个属性：

+   index 提供匹配项的索引

+   input 返回原始字符串

+   groups 列出命名的捕获组（如果有的话）

如果使用全局标志，exec() 将使用 lastIndex 的值作为起始位置来开始搜索字符串。每次调用 exec() 时，lastIndex 属性会更改，以反映匹配项中最后一个字符后的位置。让我们来看一个例子：

[appendix/methods/methods_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/appendix/methods/methods_ex2.js)

|   | **const** str = *"8, 9, 10, 11"*; |
| --- | --- |
|   | **const** re = */**\d\d**/g*; |
|   |  |
|   | console.log(re.lastIndex); |
|   | *// → 0* |
|   |  |
|   | console.log(re.exec(str)); |
|   | *// → ["10", index: 6, input: "8, 9, 10, 11", groups: undefined]* |
|   | console.log(re.lastIndex); |
|   | *// → 8* |
|   |  |
|   | console.log(re.exec(str)); |
|   | *// → ["11", index: 10, input: "8, 9, 10, 11", groups: undefined]* |
|   |  |
|   | console.log(re.lastIndex); |
|   | *// → 12* |
|   |  |
|   | console.log(re.exec(str)); |
|   | *// → null* |
|   |  |
|   | console.log(re.lastIndex); |
|   | *// → 0* |

在这段代码中，我们多次调用exec()来查找同一字符串中的连续匹配项。当方法无法找到更多匹配项时，它会返回null，并将lastIndex的值重置为0。

我们还可以手动修改lastIndex的值，以改变exec()的起始位置。例如，假设我们有一个这样的编号列表：

|   | 1\. 123 |
| --- | --- |
|   | 2\. 4355 |
|   | 3\. 764989 |

我们希望编写一个正则表达式来检索每个项目的值。使用lastIndex，我们可以仅在目标数据所在的位置进行搜索，从而大大简化正则表达式模式：

[appendix/methods/methods_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/appendix/methods/methods_ex3.js)

|   | **const** str = |
| --- | --- |
|   | *`1\. 123* |
|   | *2\. 4355* |
|   | *3\. 764989`*; |
|   |  |
|   | **const** re = */**\d**+/g*; |
|   |  |
|   | *// 将字符串拆分为多行* |
|   | **const** arr = str.split(*"***\***n"*); |
|   |  |
|   | *// 遍历每一行并应用正则表达式* |
|   | arr.forEach(line => { |
|   | re.lastIndex = 2; |
|   | console.log(re.exec(line)[0]); |
|   | }); |
|   |  |
|   | *// → 123* |
|   | *// → 4355* |
|   | *// → 764989* |
| 两个独立的家庭 |
| --- |
| ![images/aside-icons/info.png](images/aside-icons/info.png) | test()和exec()是RegEx对象的属性，因此你应该将它们作为正则表达式的方法来调用。相反，match()、matchAll()、replace()、replaceAll()、split()和search()是String对象的属性，应该在字符串上调用。 |
