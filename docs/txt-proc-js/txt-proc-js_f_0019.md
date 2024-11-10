| 配方 9 | 使用 filter() 交集 HTML 表格 |
| --- | --- |

### Task

假设你有一个显示统计数据和比分的体育应用。你有两个对象，并且想要找到同时存在于两个对象中的属性。第一个对象包含了赢得 FIFA 世界杯的国家队及其总冠军次数。第二个对象则包含了关于 UEFA 欧洲足球锦标赛的类似信息。

你想创建一个 HTML 表格，列出两个对象的交集，即列出在两个比赛中至少获得过一次冠军的队伍的表格。

### Solution

第一步是创建一个 HTML 表格。你可以将这项任务委托给 JavaScript，但让我们保持简单，先设置好 HTML 结构，再使用 JavaScript 向表格中插入信息：

[part_1/intersecting_tables/filter_ex1.xhtml](http://media.pragprog.com/titles/fkjavascript/code/part_1/intersecting_tables/filter_ex1.xhtml)

|   | <table id=*"national_teams"*> |
| --- | --- |
|   | <thead> |
|   | <tr> |
|   | <th>国家</th> |
|   | <th>UEFA 获胜次数</th> |
|   | <th>FIFA 获胜次数</th> |
|   | </tr> |
|   | </thead> |
|   | <tbody></tbody> |
|   | </table> |

现在创建两个对象：一个用于 FIFA 冠军，另一个用于 UEFA 冠军，如下所示：

[part_1/intersecting_tables/filter_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/intersecting_tables/filter_ex1.js)

|   | **const** FIFAChamps = { |
| --- | --- |
|   | *"巴西"*: 5, |
|   | *"德国"*: 4, |
|   | *"意大利"*: 4, |
|   | *"阿根廷"*: 2, |
|   | *"法国"*: 2, |
|   | *"乌拉圭"*: 2, |
|   | *"西班牙"*: 1, |
|   | *"英格兰"*: 1 |
|   | }; |
|   |  |
|   | **const** UEFAChamps = { |
|   | *"德国"*: 3, |
|   | *"西班牙"*: 3, |
|   | *"意大利"*: 2, |
|   | *"法国"*: 2, |
|   | *"俄罗斯"*: 1, |
|   | *"捷克共和国"*: 1, |
|   | *"葡萄牙"*: 1, |
|   | *"荷兰"*: 1, |
|   | *"丹麦"*: 1, |
|   | *"希腊"*: 1 |
|   | }; |

为了执行交集操作，使用 Object.keys() 获取第一个对象的键^([[8]](f_0032.xhtml#FOOTNOTE-8))，然后使用 filter() 检查哪些键在第二个对象中存在^([[9]](f_0032.xhtml#FOOTNOTE-9))。

[part_1/intersecting_tables/filter_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/intersecting_tables/filter_ex1.js)

|   | **function** getIntersection(obj1, obj2) { |
| --- | --- |
|   | **return** Object.keys(obj1).filter(key => { |
|   | **return** key **in** obj2; |
|   | }); |
|   | } |
|   |  |
|   | *// 这个常量将保存一个包含交集键的数组* |
|   | **const** intersection = getIntersection(FIFAChamps, UEFAChamps); |
|   |  |
|   | *// 获取表格主体的引用* |
|   | **const** tbody = document.querySelector(*"#national_teams tbody"*); |
|   |  |
|   | intersection.forEach(elem => { |
|   | **const** row = tbody.insertRow(); |
|   | **const** cell1 = row.insertCell(0); |
|   | **const** cell2 = row.insertCell(1); |
|   | **const** cell3 = row.insertCell(2); |
|   | cell1.textContent = elem; |
|   | cell2.textContent = UEFAChamps[elem]; |
|   | cell3.textContent = FIFAChamps[elem]; |
|   | }); |

一旦你得到两个对象的交集，遍历这些属性，每次遍历时将队伍、UEFA 胜利和 FIFA 胜利分别插入到第一、第二和第三个单元格中。在这里，我们使用了 JavaScript 的内置方法，包括 insertRow() 和 insertCell()，来创建表格行和单元格，但你也可以使用字符串字面量。这里是应用一些基本 CSS 样式后的结果：

![images/filter_ex1.png](images/filter_ex1.png)

表格只列出了同时存在于两个对象中的国家。

### 讨论

filter() 方法接受一个函数作为参数，并对数组的每个元素执行该函数——类似于 forEach() 和 map()。你提供的函数应该是一个谓词（即返回 true 或 false 的函数）。只有当谓词的返回值为 true 时，filter() 才会将元素添加到结果数组中。

在 JavaScript 中使用 filter() 方法时，重要的是要记住它会跳过数组中的任何缺失元素。例如，如果你有一个带有缺口的数组，比如 [0, 1, , , 4, , 6]，你可以利用 filter() 来去除这些缺失的元素，方法如下：

|   | **const** sparseArr = [0, 1, , , 4, , 6]; |
| --- | --- |
|   | sparseArr.filter(() => **true**); *// → [ 0, 1, 4, 6 ]* |

在这里我们使用了一个始终返回 true 的箭头函数。由于 filter() 会跳过缺口，新的数组就不会是稀疏的。

如果你的数组中还有 undefined 和 null 元素，你也可以通过 filter() 将它们移除：

|   | **const** sparseArr = [0, 1, , **null**, 4, **undefined**, 6]; |
| --- | --- |
|   | sparseArr.filter(x => x !== **undefined** && x !== **null**); *// → [ 0, 1, 4, 6 ]* |

在这段代码中，我们使用严格不等运算符（!==），只有当元素不是 null 或 undefined 时，才返回 true。

在进行性能优化时，你应该考虑对象的大小以及你需要获取交集的次数。如果你的第一个对象有 1000 个属性，第二个对象有 50 个属性，那么如果你先获取属性较少的对象的键，再应用 filter，代码的执行速度会更快，而不是反过来。

有了这个思路，让我们重写我们的交集函数：

[part_1/intersecting_tables/filter_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/intersecting_tables/filter_ex2.js)

| 1:  | **function** getIntersection(obj1, obj2) { |
| --- | --- |
| 2:  | **const** k1 = Object.keys(obj1); |
| 3:  | **const** k2 = Object.keys(obj2); |
| 4:  | **const** [first, next] = k1.length > k2.length ? [k2, obj1] : [k1, obj2]; |
| 5:  | **return** first.filter(key => key **in** next); |
| 6:  | } |

注意到我们在解构赋值的右侧使用了三元运算符来比较对象的长度，并将具有较少属性的那个赋值给 `first`（第4行）。解构赋值使我们能够使用类似数组字面量的语法提取值并将其赋给变量。在赋值的右侧是待解构的数据，左侧是将接收这些数据的变量。

我们的函数在处理大型数组时现在运行更快了。但请记住，这种微优化仅对性能关键的应用程序有帮助。在大多数情况下，使用这个食谱中的原始解决方案也完全可以。
