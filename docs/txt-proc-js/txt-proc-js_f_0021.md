| 食谱 11 | 从对象数组生成 HTML 表格 |
| --- | --- |

### 任务

假设你的任务是生成存储在对象数组中的数据报告，如下所示：

|   | const data = [ |
| --- | --- |
|   | {quarter: "Q1 FY22", revenue: 45962, netIncome: 20820, eps: 2.71}, |
|   | {quarter: "Q2 FY22", revenue: 44845, netIncome: 20610, eps: 2.71}, |
|   | {quarter: "Q3 FY22", revenue: 46151, netIncome: 16027, eps: 2.03}, |
|   | {quarter: "Q4 FY22", revenue: 46822, netIncome: 16244, eps: 2.11}, |
|   | {quarter: "Q1 FY23", revenue: 45215, netIncome: 20256, eps: 2.64} |
|   | ]; |

在前面的食谱中，你使用了一个数组的数组来创建表格。但是，在这个食谱中，数据是存储在一个对象数组中的。这意味着你需要使用稍微不同的方法来生成表格。

### 解决方案

使用以下函数：

[part_1/generating_html_table_v2/html_table_v2_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/generating_html_table_v2/html_table_v2_ex1.js)

|   | **const** data = [ |
| --- | --- |
|   | {quarter: *"Q1 FY22"*, revenue: 45962, netIncome: 20820, eps: 2.71}, |
|   | {quarter: *"Q2 FY22"*, revenue: 44845, netIncome: 20610, eps: 2.71}, |
|   | {quarter: *"Q3 FY22"*, revenue: 46151, netIncome: 16027, eps: 2.03}, |
|   | {quarter: *"Q4 FY22"*, revenue: 46822, netIncome: 16244, eps: 2.11}, |
|   | {quarter: *"Q1 FY23"*, revenue: 45215, netIncome: 20256, eps: 2.64} |
|   | ]; |
|   |  |
|   | **const** headers = [ |
|   | *"季度"*, |
|   | *"收入（以百万美元计）"*, |
|   | *"净收入（以百万美元计）"*, |
|   | *"每股收益（EPS）"* |
|   | ]; |
|   |  |
|   | **function** createTable(data, headers) { |
|   | **const** table = document.createElement(*"table"*); |
|   | **const** thead = table.createTHead(); |
|   | **const** tbody = table.createTBody(); |
|   | **const** headerRow = thead.insertRow(); |
|   |  |
|   | *// 创建表头* |
|   | headers.forEach(header => { |
|   | **const** th = document.createElement(*"th"*); |
|   | th.innerText = header; |
|   | headerRow.appendChild(th); |
|   | }); |
|   |  |
|   | *// 创建表格主体* |
|   | data.forEach(data => { |
|   | **const** row = tbody.insertRow(); |
|   | Object.values(data).forEach(value => { |
|   | **const** cell = row.insertCell(); |
|   | cell.innerText = value; |
|   | }); |
|   | }); |
|   |  |
|   | document.body.appendChild(table); |
|   | } |
|   |  |
|   | createTable(data, headers); |

当我们将数据数组作为参数调用此函数时，它会生成一个显示公司财务业绩数据的 HTML 表格。输出将类似于应用了一些基本样式后的[表格](#fig.part1.generating_html_table_v2)。

![images/generating_html_table_v2.png](images/generating_html_table_v2.png)

### 讨论

这个方法与之前的类似，只不过数组项是对象，每个对象都有如收入、净利润和每股收益等属性。在这个方法中，我们还定义了一个单独的数组，包含了我们将要创建的表格的列标题。

首先，我们为表格创建一个表头（thead）和一个表体（tbody）。然后，我们在表头中创建一个标题行（headerRow），并用 headers 数组中的标题填充它。

对于数组中的每个标题，我们使用 createElement() 方法创建一个 th 元素，将其内容设置为 header 字符串，并使用 appendChild() 方法将其添加到标题行中。

创建标题行后，我们遍历数据数组中的每个对象，并为每个对象在表格主体中创建一个新行。在每一行中，我们遍历对象的每个属性，并为每个属性值在该行中创建一个新单元格。

最后，我们将表格元素添加到 HTML 的 body 元素中。你应该修改这一行，将数据附加到你希望的元素中。
