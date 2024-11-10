© 作者，专有许可授予 Springer Fachmedien Wiesbaden GmbH，Springer Nature 旗下公司 2024J. L. Zuckarelli《学习 Python 和 JavaScript 编程》[https://doi.org/10.1007/978-3-658-42912-6_35](https://doi.org/10.1007/978-3-658-42912-6_35)

# 35. 循环：如何高效地重复程序指令？

Joachim L. Zuckarelli^([1](#Aff2) )(1)德国慕尼黑概述

与大多数其他编程语言一样，JavaScript 提供了循环结构，可以重复相似的语句。实际上，这种循环非常流行且经常使用，因为它们可以清晰而优雅地表达重复的过程。在本章中，我们将详细了解 JavaScript 中主要的循环类型，并通过一个较大的示例来演示它们的实际应用。

在本章中，你将学习：

+   如何使用带有数字运行变量的计数**for**循环，来执行语句或语句块，重复指定的次数

+   如何通过**for-of**循环轻松遍历一组对象（例如数组的内容）

+   如何开发由头部控制（**while**）和由尾部控制（**do-while**）的条件循环，其执行取决于一个可以自由定义的运行条件

## 35.1 计数循环（for 和 for-of）

### 35.1.1 带有数值运行变量的**for**循环

**for**循环的结构与功能

在 JavaScript 中，标准的**for**循环用于重复代码块，形式如下：

**for**(初始化; 检查; 增量) {*// 被重复的代码块*}

假设我们有一个名字数组，想通过**for**循环遍历它：

**>** friends = ['Peter', 'Sophie', 'Helen', 'Mike', 'Ben']

像大多数计数循环一样，我们需要一个（数值型）运行变量，假设它是**i**，并且首先使用起始值对其进行初始化。正如我们现在已经知道的，JavaScript 中数组的索引是从 0 开始的，因此建议在开始时将运行变量**i**设置为 0：**i = 0**。接下来，我们需要在循环头部设置一个检查条件，只有满足此条件，循环才会继续。在我们的示例中，假设我们想要循环遍历从 0 到最后一个元素的数组，这个条件必须是：**i <= friends.length-1**（请注意，最后一个元素的索引是**length-1**，因为我们已经从 0 开始计数！）。最后，我们需要告诉循环在每一步中，运行变量应该增加多少。在我们的示例中，运行变量增加 1。因此，循环通过数组的元素并将它们输出到控制台的代码如下所示：

**for**(i = 0; i <= friends.length-1; i = i+1) {console.log('Friend no. ', i+1, ': ', friends[i])}

循环现在从运行变量的值 0 开始，首先检查运行条件是否满足。因为 0 小于数组长度减一（即四），所以循环开始执行循环体中的代码。在第一次执行时，运行变量的值为 0。实际执行的代码是：

console.log('朋友编号 ', 1, ': ', friends[0])

当循环体执行完毕后，执行将跳回循环头，并根据增量语句增加运行变量，在我们的示例中为1。然后再次检查运行条件，如果满足条件，则循环体中的代码将再次执行。循环将继续进行这些回合，直到运行变量的下一个增量后，运行条件不再满足。在我们的示例中，如果**i**等于5，运行变量现在大于数组长度减一，循环体中的代码将不再执行。相反，程序的执行将继续在**for**循环之后。运行变量保持其旧值，不再递增。

我们可以使用增量操作符**++**（它是单目运算符，因为它只作用于一个操作数），而不是使用增量指令**i = i+1**，只需写**i++**。运行变量的值也可以递减（这样我们就可以从数组的末尾向前遍历）。当然，初始化运行变量的起始值也必须进行调整，否则循环将根本不会执行。最好的减少运行变量1的方法是使用递减操作符**--**。

顺便说一下：所有的JavaScript循环都可以通过**break**语句退出，并通过**continue**语句进入下一个循环。这不仅适用于**for**循环，也适用于**for-of**、**while**和**do-while**循环，我们将在接下来的章节中进行讲解。

一个实际的例子

以下示例展示了一个**for**循环，准确来说是两个嵌套的循环，在实际应用中的使用。这次的目标是开发一个简单的电子表格，可以在表格单元格中输入数字，并计算行和列的总和。在第一步中，用户输入电子表格的大小。

根据用户的规格生成的电子表格可以在◘ 图 [35.1](#Fig1) 中看到。![](../images/474412_1_En_35_Chapter/474412_1_En_35_Fig1_HTML.jpg)

一个包含5列和6行的电子表格文档截图。其中一些单元格包含数字数据。第5列和第6行分别显示每列和每行的总和。

图 35.1

具有5行4列的电子表格

要输入表格大小，我们为用户提供了以下简单的网页界面：

**<!DOCTYPE html>****<html>****<head>****<title>**电子表格**</title>****<noscript>**请启用JavaScript！**</noscript>****</head>****<body>****<script** src="spreadsheet.js"**></script>****<h1>**设置表格大小**</h1>****<form>**行：**<br>****<input** id="rows" type="text" value="0"**><p></p>**列：**<br>****<input** id="columns" type="text" value="0"**><p></p>****<input** type="button" value="创建表格"onclick="createTable()"**>****</form>****</body>****</html>**

当你点击“创建表格”按钮时，**spreadsheet.js** 文件中的 JavaScript 函数 **createTable()** 被调用。这个函数如下所示：

1 **function** createTable() {2 **var** num_rows = Number(document.getElementById('rows').value);3 **var** num_columns =Number(document.getElementById('columns').value);4 **var** i,f;56 document.write('<H1>电子表格文档</H1>');7 document.write('<form><table>');89 *// 写入单元格*10 **for**(i = 1; i <= num_rows; i++) {11 document.write('<tr>');12 **for**(f = 1; f <= num_columns; f++) {13 document.write('<td><input id="R', i, 'C', f, '" \type="text" value=""></td>');14 }15 *// 为总和列添加单元格*16 document.write('<td><input id="SUM_R', i, '" type="text" \value="" readonly="true" style="background-color: \#d1d1d1; "></td>')17 document.write('</tr>');18 }1920 *// 添加总和行*21 document.write('<tr>');22 **for**(f = 1; f <= num_columns; f++) {23 document.write('<td><input id="SUM_C', f, '" type="text" \value="" readonly="true" style="background-color: \#d1d1d1;"></td>');24 }25 document.write('</tr>');2627 document.write('</table>');2829 document.write('<input type="hidden" id="nrows" \value="', num_rows,'">');30 document.write('<input type="hidden" id="ncolumns" \value="', num_columns,'">');3132 document.write("<p></p>")33 document.write('<input type="button" value="计算" \onclick="calculate()">');34 document.write("</form>");35 }

这段 JavaScript 代码为我们的电子表格创建了表格。简单的表格在 HTML 中具有以下形式：

**<table>****<tr><td>**第 1 行，第 1 列**</td><td>**第 1 行，第 2 列**</td></tr>****<tr><td>**第 2 行，第 1 列**</td><td>**第 2 行，第 2 列**</td></tr>****</table>**

各个表格行由 **tr** 元素（*表格行*）表示，行中包含的单元格由 **td** 元素（*表格数据*）表示。

外层的 **for** 循环，运行变量 **i** 的循环头可以在第 10 行找到，创建表格的行。在这个循环的主体部分是另一个 **for** 循环，其循环头在第 12 行。这个“内层循环”使用运行变量 **f**，为当前行（即由运行变量 **i** 在“外层” **for** 循环中指示的行）写入每个列的单元格。通过这种方式，两个嵌套的 **for** 循环完整地“遍历”矩形表格结构。

在第 16/17 行（此代码*不*在内层循环中！）为当前行写入另一个单元格，作为“总计”列的一部分。类似地，在两个循环之外（第 24–28 行），使用另一个循环来写入“总计”行。

请注意，我们给值单元格分配了类似 **R*****x*****C*****y*** 的 ID，其中 **x** 是行号，**y** 是单元格所在的列号。汇总行或列的 ID 采用 **SUM_R*****x*** 或 **SUM_C*****y*** 的形式。这种系统化的 ID 组成方式将使我们能够轻松访问各个单元格。

第29/30行中的表单元素也在这里帮助我们：它们的类型是**hidden**，最终它们只是信息的隐藏存储库。我们将行数和列数存储在这里，以便在求和时可以稍后访问它们。

求和由**calculate()**函数处理，用户可以通过我们在第33行创建的按钮触发该函数。或者，你可以将该函数作为事件处理程序附加到各个单元格输入字段的**change**或**input**事件上；为此，你只需在相应输入元素的**onchange**或**oninput**属性中提供对第13行**calculate()**函数的引用（试试看！）

**calculate()**函数的代码如下所示：

1 **function** calculate() {2 **var** num_rows = Number(document.getElementById('nrows').value);3 **var** num_columns = Number(document.getElementById('ncolumns').value);4 **var** i, f, sum, sum_column;56 *// 计算行总和*7 **for**(i = 1; i <= num_rows; i++) {8 sum_cell = document.getElementById('SUM_R' + i);9 sum = 0;10 **for**(f = 1; f <= num_columns; f++) {11 sum = sum + Number(document.getElementById('R' + i + 'C' + f).value);12 }13 sum_cell.value = sum;14 }1516 // 计算列总和17 **for**(f = 1; f <= num_columns; f++) {18 sum_cell = document.getElementById('SUM_C' + f);19 sum = 0;20 **for**(i = 1; i <= num_rows; i++) {21 sum = sum + Number(document.getElementById('R' + i + 'C' + f).value);22 }23 sum_cell.value = sum;24 }25 }

**calculate()**首先从我们的两个**hidden**表单元素中查询行数和列数（第2行和第3行）。然后，我们计算行总和（第7-14行）和列总和（第17-24行）。我们利用了这样一个事实：数值单元格的ID形式为**R*****x*****C*****y***，而行和列总和单元格的ID形式分别为**SUM_R*****x***和**SUM_C*****y***。

以行总和为例，我们通过**for**循环（第7行）遍历所有行，并首先选择“总和”列的相应单元格（第8行）。然后，我们只需要遍历各个数值列（第10行），加上其中的数字（第11行），并将总和写入该表格行的对应总和单元格（第13行）。

35.1 [10分钟]如果输出我们的数组**friends**到控制台，两个**for**循环应该是什么样子的？

+   一个循环仅显示每隔一个的条目

+   另一个循环显示每个条目，但是从后往前进行的？

35.2 [60分钟]

开发一个应用程序，用户可以首先通过滑动条根据红色、绿色和蓝色分量指定一个颜色。根据此颜色，阴影表格将被扩展，以使每个表格单元显示不同的颜色。在水平方向上，红色部分增加，在垂直方向上，蓝色部分增加，共有10步，直到255（根据RGB方案的最大值）。绿色部分保持用户设置的值不变。

当用户移动任一滑块时，阴影表应自动更新。

你完成的应用程序可能看起来像图◘[35.2](#Fig2)。![](../images/474412_1_En_35_Chapter/474412_1_En_35_Fig2_HTML.jpg)

一个包含10列10行单元格并有多种颜色阴影的阴影表截图。表格上方有三个滑块，分别用于红色、绿色和蓝色。

图 35.2

练习应用中的阴影表

一些提示：

+   使用**Number**对象的**toString()**方法将十进制数转换为十六进制数，这在HTML标准格式**#RRGGBB**中显示为RGB颜色值。**toString()**方法的参数是要转换的数字系统的基数，对于十六进制数来说是**16**。

+   请记住，使用格式**#RRGGBB**时，每个颜色部分必须始终有两个数字！小于16的数字会导致*一位数*的十六进制数。这些必须在前面加上0。

+   你计算的颜色组件必须是整数。为了确保安全，使用**Math.floor(number)**函数将其四舍五入。该函数会返回传入参数的下一个更小的整数。

### 35.1.2 使用对象运行变量的for-循环（for…of）

JavaScript中已知的**for-loops**的第二种形式并不对数值型运行变量进行增减，而是遍历一组对象；此时，运行变量的内容就是相应循环迭代的对象。

有了这个，上一节的示例可以这样写：

**>** friends = [**'**Peter**'**, **'**Sophie**'**, **'**Helen**'**, 'Mike**'**, **'**Mohamed**'**]**>** i = 0;for(myfriend of friends) {i++;console.log(**'**Friend no. **'**, i, **'**:**'**, myfriend)}

在这里，我们需要手动增加变量**i**。它不是循环的运行变量（运行变量是**myFriend**），而仅仅作为我们在控制台输出时生成连续编号的工具。

这将给出以下输出：

Friend no. 1 : PeterFriend no. 2 : SophieFriend no. 3 : HellenFriend no. 4 : MikeFriend no. 5 : Fatih

因此，**for-of**循环的一般形式是：

***for***(runVariable of iterableObject) {*// 这是重复的代码块*}

我们在此遍历的*可迭代对象*是一个数组。其他对象也可以是可迭代的；例如，表示地址的对象可以使其属性（如街道名称、门牌号和邮政编码）变为可迭代的，从而能够通过**for-of**循环进行遍历。然而，要实现这一点，需要超出初级JavaScript的范围，因此不在我们本节的讨论范围内。

顺便说一下，字符串（也可以用数组表示法访问，► 第[31.4](474412_1_En_31_Chapter.xhtml#Sec10)节）也是可迭代对象，可以通过**for-of**循环进行遍历：

**for**(character of **'**Hello World!**'**) {console.log(character);}

请注意，在通过**for-of**循环时，运行变量并不仅仅是我们可迭代对象元素的*副本*，它实际上就是*元素本身*。因此，在**for-of**循环中对运行变量所做的更改会影响正在被迭代的对象！

## 35.2 条件循环（while和do-while）

对于**while**和**do-while**循环，JavaScript有两种条件循环。**while**循环是*头控型*的，也就是说，条件在循环开始时就会被检查，因此如果条件从一开始就没有满足，循环根本不会执行。**do-while**是*尾控型*循环。无论如何，它至少会执行一次；在第一次执行结束后，会检查条件是否满足以决定循环是否应该第二次执行，并在每次后续循环中如此。

这两个循环通常具有以下结构：

**while**(*condition*) {*// 重复的代码块*}and**do** {*// 重复的代码块*}**while**(*condition*)

我们在上一节中得到的**friends**数组输出可以通过**while**循环来实现，例如：

**>** friends = [**'**Peter**'**, **'**Sophie**'**, **'**Helen**'**, 'Mike**'**, **'**Mohamed**'**]**>** i = 0;while(i <= friends.length - 1) {console.log(**'F**riend no. **'**, i+1, **'**: **'**, friends[i]);i = i + 1;}

使用**do-while**的表达式可能看起来是这样的：

i = 0;**do** {console.log('Friend no. **'**, i+1, **'**:**'**, friends[i]);i = i + 1;}**while**(i <= friends.length - 1)

**do-while**循环应该仅在你可以安全地假设循环的运行条件在第一次迭代时就会满足时使用；在这里，这不是问题，因为我们知道前面没有一个空数组。

在我们的例子中，我们使用了**while**和**do-while**循环来解决一个通常会使用**for**循环的任务，因为循环次数可以通过数组的**length**属性轻松确定。条件循环通常在执行依赖于一般条件且循环次数不能提前确定的情况下使用。然而，我们的例子很好地说明了我们之前遇到的一个原则：任何可以通过计数循环解决的问题，也可以通过条件循环来解决，因为在不确定的情况下，你也可以将一个数值运行变量的值作为条件进行检查，正如我们在例子中所做的那样。从这个意义上说，*计数*循环是一种特殊形式的*条件循环*，即其条件检查一个运行变量，而计数循环恰好负责初始化并递增该变量。

35.3 [10 min] 编写另外两个版本的**while**循环，将此节中的**friends**数组输出到控制台，其中

1.  (a)

    一旦“运行变量”**i**初始化为1（而不是0）

1.  (b)

    条件中使用的是小于操作符，而不是小于等于操作符。

35.4 [30 分钟]

开发一个函数**countCells()**，该函数可选地计算我们的电子表格应用程序根据►节[35.1.1](#Sec2)创建的表格的行或列。使用**while**循环遍历单元格的ID。利用**document.getElementById()**函数的特点，如果找不到具有指定ID的元素，它会返回**null**。

你在这里开发的函数可以被我们的**calculate()**函数用来获取行和列的数量，前提是我们没有通过在HTML文档的页面源代码中使用**hidden**元素将其“缓存”。

## 35.3 总结

在本章中，我们学习了如何使用计数（**for**，**for-of**）和条件（**while**，**do-while**）循环在JavaScript中重复代码。

请确保从本章中记住以下要点：

+   在JavaScript中，计数循环的形式为**for(*****initialization*****;** ***check*****;** ***increment*****) {** ***statements*** **}**。这里，初始化为某个值的数字型运行变量在每次循环之前根据递增语句进行改变，并检查新值是否满足检查条件。如果满足条件，则执行后续的语句块；如果不满足条件，则程序继续执行循环后的代码，运行变量保持在上次递增前的值。

+   运行变量也可以减少，即，随着每次循环运行，运行变量变小。

+   递增和递减操作可以通过递增操作符**++**和递减操作符**--**来实现，形式为**variable++**或**variable--**。

+   形式为**for(*****runVariable*** **of** ***iterableObject*****) {** ***statements*** **}**的**for-of**循环可以用来遍历那些其元素是可迭代的对象，即它们可以被JavaScript以任何顺序排列的对象，比如数组。在这种情况下，运行变量不是数值，而是当前循环迭代应用的可迭代对象的元素。对运行变量的更改会影响正在遍历的可迭代对象。

+   条件循环可以是头驱动的，形式为**while(*****condition*****) {** ***statements*** **}**，也可以是尾驱动的，形式为**do {** ***statements*** **} while(*****condition*****)**。后一种类型的循环至少执行一次，因为条件检查是在循环结束后进行的。

## 35.4 练习解答

练习 35.1

只显示数组中每隔一个元素的循环可能如下所示：

**for**(i = 0; i <= friends.length-1; i=i+2) {console.log(**'**Friend no. **'**, i+1, **'**:**'**, friends[i]);}

一个从后向前遍历数组条目的循环可能如下所示：

**for**(i = friends.length-1; i >= 0; i--) {console.log(**'F**riend no. **'**, i+1, **'**:**'**, friends[i]);} 练习 35.2

我们的阴影表格应用程序的界面可以像这样用 HTML 代码设计：

**<!DOCTYPE html>****<html>****<head>****<title>**色彩表格**</title>****<noscript>**请启用 JavaScript！**</noscript>****</head>****<body>****<script** src="colortable.js"**></script>****<form>**<**p>**红色：**<input** id="red" type="range" min=0max=255 value="0" onchange="colorsNew()"**><p>****<p>**绿色：**<input** id="green" type="range" min=0max=255 value="0" onchange="colorsNew()"**><p>****<p>**蓝色：**<input** id="blue" type="range" min=0max=255 value="0" onchange="colorsNew()"**><p>****</form>****<table** id="colortable"**>****</table>****</body>****</html>**

为此目的，JavaScript 文件**colortable.js**：

**function** colorsNew() {**var** colorRed = Number(document.getElementById('red').value);**var** colorGreen = Number(document.getElementById('green').value);**var** colorBlue = Number(document.getElementById('blue').value);**var** tab = document.getElementById('colortable');**var** i,f, colorValue, stepRed, stepBlue;stepRed = Math.floor((255-colorRed)/10);stepBlue = Math.floor((255-colorBlue)/10);tableHTML = "";**for**(i = 1; i <= 10; i**++**){tableHTML = tableHTML + '<tr>';**for**(f = 1; f <= 10; f**++**) {colorRedNew = (colorRed + i*stepRed).toString(16);colorGreenNew = colorGreen.toString(16);colorBlueNew = (colorBlue + f*stepBlue).toString(16);if(colorRedNew.length == 1)colorRedNew = '0' + colorRedNew;if(colorGreenNew.length == 1)colorGreenNew = '0' + colorGreenNew;if(colorBlueNew.length == 1)colorBlueNew = '0' + colorBlueNew;colorVal = "#" + colorRedNew + colorGreenNew + colorBlueNew;tableHTML = tableHTML + '<td style="background-color: ' +colorValue + '; color: ' + colorValue + '">xxxx</td>';}tableHTML = tableHTML + '</tr>';}tab.innerHTML = tableHTML;}练习 35.3

1.  (a)

    一个**while**循环，遍历数组并从1开始：

i = 1;**while**(i <= friends.length) {console.log(**'**Friend no. **'**, i, **'**:**'**, friends[i-1]);i = i + 1;}

1.  (b)

    一个**while**循环，遍历数组并在运行条件中使用小于运算符：

i = 0;**while**(i < friends.length) {console.log(**'F**riend no. **'**, i+1, **'**:**'**, friends[i]);i = i + 1;}练习 35.4

函数**countCells()**可以如下所示：

**function** countCells(columnRow = 'column') {**var** num = 0;**var** id;**do** {num = num + 1;**if**(columnRow == 'column') {id = 'R1C' + num;}**else** {id = 'R' + num + 'C1';}}**while**(document.getElementById(id) != **null**)**return** num - 1;}

我们在这里使用一个参数**columnRow**，其默认值为"**column**"，用于指定是返回列数还是行数。然后，通过在**do-while**循环中组合单元格ID来确定数量（我们假设至少存在一列或一行，这样我们也可以在循环结束时测试循环的运行条件），并尝试使用**getElementById()**选择这些单元格。如果失败了，因为单元格不存在，**getElementById()**将返回**null**，并且循环结束。在循环中递增的行/列数**num**将是函数的返回值。
