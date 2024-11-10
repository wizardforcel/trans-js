| 配方 12 | 使用 console.table() 在控制台显示表格数据 |
| --- | --- |

### 任务

假设你一直在对一个数组进行加法和减法运算，但遇到了一些问题。你想检查脚本中特定行的数组内容，以便定位问题。

你需要一种快速将数组内容打印到控制台的方法。

### 解决方案

使用 console.table() 方法：

[part_1/displaying_tabular_data/displaying_tabular_data_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/displaying_tabular_data/displaying_tabular_data_ex1.js)

|   | **const** data = [ |
| --- | --- |
|   | {quarter: *"Q1 FY22"*, revenue: 45962, netIncome: 20820, eps: 2.71}, |
|   | {quarter: *"Q2 FY22"*, revenue: 44845, netIncome: 20610, eps: 2.71}, |
|   | {quarter: *"Q3 FY22"*, revenue: 46151, netIncome: 16027, eps: 2.03}, |
|   | {quarter: *"Q4 FY22"*, revenue: 46822, netIncome: 16244, eps: 2.11}, |
|   | {quarter: *"Q1 FY23"*, revenue: 45215, netIncome: 20256, eps: 2.64} |
|   | ]; |
|   |  |
|   | console.table(data); |

console.table() 方法以便于人类理解的格式在控制台输出一个数组：

![images/tabular_data_ex1.png](images/tabular_data_ex1.png)

### 讨论

console.table() 方法应当获得更多 JavaScript 开发者的认可。虽然许多开发者使用 for 循环将数组项记录到控制台，JavaScript 已经提供了 console.table() 方法，能更直接地实现相同的效果。

表格的初始列将被指定为（index）。如果数据是数组形式，其值将对应数组索引；另一方面，如果数据是对象形式，则其值将与属性名对齐，如[表格](#fig.part1.tabular_data_ex2)所示。

[part_1/displaying_tabular_data/displaying_tabular_data_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/displaying_tabular_data/displaying_tabular_data_ex2.js)

|   | **const** data = { |
| --- | --- |
|   | *"Q1 FY22"*: {revenue: 45962, netIncome: 20820, eps: 2.71}, |
|   | *"Q2 FY22"*: {revenue: 44845, netIncome: 20610, eps: 2.71}, |
|   | *"Q3 FY22"*: {revenue: 46151, netIncome: 16027, eps: 2.03}, |
|   | *"Q4 FY22"*: {revenue: 46822, netIncome: 16244, eps: 2.11}, |
|   | *"Q1 FY23"*: {revenue: 45215, netIncome: 20256, eps: 2.64} |
|   | }; |
|   |  |
|   | console.table(data); |

![images/tabular_data_ex2.png](images/tabular_data_ex2.png)

在这里，季度值用作表头，而包含 revenue、netIncome 和 eps 属性的对象用作行值。

console.table() 方法还接受一个额外的可选参数，允许你限制显示的列。例如，如果你只想显示 netIncome 列，可以使用如下代码：

[part_1/displaying_tabular_data/displaying_tabular_data_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/displaying_tabular_data/displaying_tabular_data_ex3.js)

|   | **const** data = { |
| --- | --- |
|   | *"Q1 FY22"*: {revenue: 45962, netIncome: 20820, eps: 2.71}, |
|   | *"Q2 FY22"*: {revenue: 44845, netIncome: 20610, eps: 2.71}, |
|   | *"Q3 FY22"*: {revenue: 46151, netIncome: 16027, eps: 2.03}, |
|   | *"Q4 FY22"*: {revenue: 46822, netIncome: 16244, eps: 2.11}, |
|   | *"Q1 FY23"*: {revenue: 45215, netIncome: 20256, eps: 2.64} |
|   | }; |
|   |  |
|   | console.table(data, *"netIncome"*); |

![images/tabular_data_ex3.png](images/tabular_data_ex3.png)

console.table() 方法可以生成清晰简洁的表格数据的纯文本表示。当处理多维数组（即包含其他数组的数组）时，使用 console.table() 的好处尤其明显。在调试数组和对象时，记得充分利用它。
