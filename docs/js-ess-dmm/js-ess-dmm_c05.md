第五章

# 函数的强大力量

本章内容

![Bullet](images/check.png) 了解 JavaScript 函数

![Bullet](images/check.png) 创建并使用自定义函数

![Bullet](images/check.png) 传递和返回函数值

![Bullet](images/check.png) 使用匿名函数和箭头函数

几乎每个超出最简单脚本的 JavaScript 项目都会需要一个或多个（通常更多）任务或计算，这些任务或计算不属于 JavaScript 语言或任何 Web API。那么程序员该怎么办呢？你挽起袖子，写自己的代码来完成任务或执行计算。

本章将向你展示如何创建这样的自定义代码。在接下来的页面中，你将探索自定义函数这一强大且无穷有用的领域，在哪里你可以编写可重用的代码，执行一些 JavaScript 原生无法做到的任务。

`function` 是一组与脚本其他部分分开的 JavaScript 语句，执行指定的任务。当脚本需要执行该任务时，你会告诉它运行——或者用通俗的说法就是 `执行`——该函数。

函数的基本结构如下所示：

`function *functionName*([*arguments*]) { *JavaScript 语句* }`

下面是函数各部分的总结：

+   `function`：标识紧随其后的代码块为一个函数。

+   `functionName`：函数的唯一名称。我在[第 2 章](c02.xhtml)中为变量概述的命名规则和准则也适用于函数名。

+   `arguments`：传递给函数的一个或多个值，作为函数内部的变量。参数（有时也称为 `parameters`）通常是一个或多个值，函数用它们作为任务或计算的原料。你总是将参数放在函数名后的圆括号中，并用逗号分隔多个参数。如果你不使用参数，仍然需要在函数名后加上圆括号。

+   `JavaScript 语句`：这是执行函数任务或计算的代码。

还要注意花括号（`{` 和 `}`）的使用。这些花括号用于将函数的语句括在一个代码块中，告诉你（以及浏览器）函数的代码从哪里开始，到哪里结束。关于花括号的位置，只有两条规则：

+   开始的花括号必须出现在函数的圆括号之后，并在第一个函数语句之前。

+   结束的花括号必须出现在最后一个函数语句之后。 ## 调用函数

在函数定义后，你最终需要告诉浏览器执行——或者 `调用`——该函数。主要有三种方式来实现这一点：

+   当浏览器解析 `<script>` 标签时。

+   页面加载后。

+   响应事件，例如用户点击按钮。

接下来的三节将分别涵盖这些场景。

### 当浏览器解析 `<script>` 标签时

调用函数的最简单方法是，在脚本中包含一个仅由函数名和圆括号组成的语句（暂时假设你的函数不使用参数）。以下代码提供了一个示例。（我列出了整个页面，以便向你展示函数及其调用语句在页面代码中的位置。）

`<!DOCTYPE html> <html lang="en"> <head> <meta charset="utf-8"> <title>在 `<script>` 标签解析时调用函数</title> <script> function displayGreeting() { const currentHour = new Date().getHours(); if (currentHour < 12) { console.log("早上好！"); } else { console.log("你好！"); } } displayGreeting(); </script> </head> <body> </body> </html>`

`<script>` 标签中包含一个名为 `displayGreeting` 的函数，该函数根据当前时间确定是早上还是其他时间，然后将问候语写入控制台（请查看 [图 5-1](#c05-fig-0001)；你将在 [第9章](c09.xhtml) 学到更多关于控制台的内容）。该函数通过紧跟其后的 `displayGreeting` 语句被调用。

![调用函数时 `<script>` 标签被解析的示例快照。](images/9781394263219-fg0501.png)

[图 5-1：](#rc05-fig-0001) 在 `<script>` 标签解析时调用函数的示例。  ### 当页面加载完成时

如果你的函数引用了页面元素，那么从页面头部部分调用函数将不起作用，因为当浏览器解析脚本时，页面的其余部分尚未加载，因此你的元素引用将失败。

为了解决这个问题，可以在页面的 `body` 部分末尾、闭合的 `</body>` 标签之前放置另一个 `<script>` 标签，如下所示：

`<!DOCTYPE html> <html lang="en"> <head> <meta charset="utf-8"> <title>在页面加载后调用函数</title> <script> function makeBackgroundRed() { document.body.style.backgroundColor = "red"; console.log("背景现在是红色的。"); } </script> </head> <body> <!-- 其他页面元素在这里 -->  <script> makeBackgroundRed(); </script> </body> </html>`

`makeBackgroundRed` 函数做了两件事：它使用 `document.body.style.backgroundColor` 将 `body` 元素的背景色改为红色，并使用 `console.log` 将这个信息写入控制台。

在这个函数中，`document.body` 是指向 `body` 元素的引用，而该元素在页面完全加载之前是“不存在”的。这意味着，如果你尝试在初始脚本中调用该函数，将会出现错误。为了正确执行该函数，第二个 `<script>` 标签出现在 `body` 元素的底部，该脚本通过以下语句调用函数：

`makeBackgroundRed();`

当浏览器执行该语句时，`body` 元素已经存在，因此函数可以顺利运行而不会出错（请查看 [图 5-2](#c05-fig-0002)）。

![页面加载后响应事件调用函数的示例快照。](images/9781394263219-fg0502.png)

`[图 5-2:](#rc05-fig-0002)` 页面加载后调用函数的示例。

JavaScript 函数最常见的调用方式之一是响应某个事件。事件是一个非常重要的话题，我在 `[第 6 章](c06.xhtml)` 中专门讲解了它们。现在，来看一个相对简单的应用：当用户点击按钮时执行函数。以下代码展示了实现这一点的其中一种方法：

`<!DOCTYPE html> <html lang="en"> <head> <meta charset="utf-8"> <title>响应事件调用函数</title> <script> function makeBackgroundRed() { document.body.style.backgroundColor= "red"; } function makeBackgroundWhite() { document.body.style.backgroundColor= "white"; } </script> </head> <body> <button onclick="makeBackgroundRed()"> 使背景变红 </button> <button onclick="makeBackgroundWhite()"> 使背景变白 </button> </body> </html>`

我在这里做的是将两个函数放入脚本中：`makeBackgroundRed`将页面背景更改为红色，`makeBackgroundWhite`将背景颜色恢复为白色。

这些按钮是标准的 HTML `button` 元素（参见 `[图 5-3](#c05-fig-0003)`），每个按钮都包括 `onclick` 属性。这个属性定义了一个 `handler`——即要执行的函数——用于响应用户点击按钮时触发的事件。例如，考虑第一个按钮：

`<button onclick="makeBackgroundRed()">`

![响应事件调用函数的示例快照。](images/9781394263219-fg0503.png)

`[图 5-3:](#rc05-fig-0003)` 响应事件调用函数的示例。

这里的`onclick`属性实际上是说：“当有人点击这个按钮时，调用名为`makeBackgroundRed`的函数。”

使用函数的主要原因之一是能够控制某些 JavaScript 代码执行的时机。例如，上一节就讨论了如何利用函数来设置，确保代码在用户点击按钮之前不会执行。

然而，使用函数还有另一个重要原因：避免不必要的重复代码。为了理解我的意思，考虑一下上一节中的两个函数：

`function makeBackgroundRed() { document.body.style.backgroundColor= "red"; } function makeBackgroundWhite() { document.body.style.backgroundColor= "white"; }`

这两个函数执行相同的任务——改变背景颜色——它们之间的唯一区别是一个将颜色更改为红色，而另一个将其更改为白色。每当你遇到两个或更多本质上做同样事情的函数时，你就知道你的代码效率不高。

那么，如何提高代码的效率呢？这时前面提到的参数就发挥了作用。`argument`（参数）是一个被“传送”——或者在编程术语中称为“传递”——给函数的值。参数就像一个变量，它会自动存储传递给它的任何值。

### 向函数传递一个值

作为一个例子，你可以将之前的两个函数合并为一个函数，并将颜色值设置为参数。这里有一个实现这一功能的新函数：

`function changeBackgroundColor(newColor) { document.body.style.backgroundColor = newColor; }`

参数被命名为`newColor`，并被添加到函数名称后的括号中。JavaScript会自动将`newColor`声明为一个变量，因此你不需要单独使用`let`或`const`语句。然后，函数使用`newColor`的值来改变背景颜色。那么，如何向函数传递一个值呢？以下代码展示了一个实现这一功能的示例文件：

`<!DOCTYPE html> <html lang="en"> <head> <meta charset="utf-8"> <title>向函数传递一个值</title> <script> function changeBackgroundColor(newColor) { document.body.style.backgroundColor = newColor; } </script> </head> <body> <button onclick="changeBackgroundColor('red')"> 设置背景为红色 </button> <button onclick="changeBackgroundColor('white')"> 设置背景为白色 </button> </body> </html>`

这里的关键是出现在两个`<button>`标签中的`onclick`属性。例如：

`onclick="changeBackgroundColor('red')"`

字符串`'red'`被插入到函数名称后的括号中，这样该值就会传递给函数本身。另一个按钮传递值`'white'`，函数结果会相应地变化。

![警告](images/warning.png) 在示例代码中的两个`onclick`属性中，请注意传递给函数的值被单引号（`'`）括起来。这是必要的，因为`onclick`的值整体是用双引号（`"`）括起来的。### 向函数传递两个或更多值

对于更复杂的函数，你可能需要使用多个参数，以便传递不同类型的值。如果使用多个参数，每个参数之间需要用逗号分隔，如下所示：

`function changeColors(newBackColor, newForeColor) { document.body.style.backgroundColor = newBackColor; document.body.style.color = newForeColor; }`

在这个函数中，`document.body.style.color`语句改变了前景色（即页面文本的颜色）。以下代码展示了一个修改后的页面，其中按钮将两个值传递给函数：

`<!DOCTYPE html> <html lang="en"> <head> <meta charset="utf-8"> <title>将多个值传递给函数</title> <script> function changeColors(newBackColor, newForeColor) { document.body.style.backgroundColor = newBackColor; document.body.style.color = newForeColor; } </script> </head> <body> <h1>将多个值传递给函数</h1> <button onclick="changeColors('red', 'white')"> 红色背景，白色文本 </button> <button onclick="changeColors('white', 'red')"> 白色背景，红色文本 </button> </body> </html>`

![警告](images/warning.png) 如果你定义一个函数有多个参数，你必须始终为每个参数传递值。如果不传递值，`undefined`会被传递，这可能会导致问题。  ## 从函数获取值

到目前为止，我已经概述了使用函数的两个主要优点：

+   你可以用它们来控制代码的执行时机。

+   你可以用它们将重复的代码整合成一个单一的例程。

函数为JavaScript带来的第三大好处是，你可以用它们来执行计算并返回结果。作为示例，这里是一个计算餐厅账单小费的函数：

`function calculateTip(preTip, tipPercent) { const tipResult = preTip * tipPercent; return tipResult; }  const preTipTotal = 100.00; const tipPercentage = 0.15; const tipCost = calculateTip(preTipTotal, tipPercentage); const totalBill = preTipTotal + tipCost; document.write("Your total bill is $" + totalBill);`

名为`calculateTip`的函数接受两个参数：`preTip`是小费之前账单的总额，`tipPercent`是用于计算小费的百分比。函数接着声明一个名为`tipResult`的变量，并用它来存储计算结果——`preTip`乘以`tipPercent`。这个示例的关键是函数的第二行：

`return tipResult;`

`return`语句是JavaScript返回值给调用函数语句的方式。该语句位于函数之后：

`tipCost = calculateTip(preTipTotal, tipPercentage);`

该语句首先将`preTipTotal`（之前在脚本中初始化为`100.00`）和`tipPercentage`（之前初始化为`0.15`）的值传递给`calculateTip`函数。当该函数返回其结果时，整个表达式`calculateTip(preTipTotal, tipPercentage)`会被该结果替换，这意味着结果会存储在`tipCost`变量中。然后，`preTipTotal`和`tipCost`相加，结果存储在`totalBill`中，`document.write`语句显示最终计算结果（查看[图 5-4](#c05-fig-0004)）。

![一张快照显示输出如下。您的总账单是115美元。](images/9781394263219-fg0504.png)

[图 5-4：](#rc05-fig-0004) 输出包括自定义函数计算的返回值。 ## 使用匿名函数

这里是本章早些时候函数语法的另一个视角：

`function *functionName*([arguments]) { JavaScript statements }`

这种函数语法创建了一个所谓的`named function`，因为——你猜对了——这个函数有一个名字。

然而，创建一个没有名字的函数也是可能的：

`function ([arguments]) { JavaScript statements }`

这种函数语法创建了一个所谓的`anonymous function`，因为——没错——这个函数没有名字。

为什么使用匿名函数？好吧，首先，如果你不想的话，你并不需要。其次，使用匿名函数的主要原因是为了避免在不需要时创建一个命名对象。每个大型网页项目都有一个巨大的`namespace`，它指的是你分配给变量和函数等事物的标识符的完整集合。命名空间越大，发生`namespace collision`的可能性就越大，即你为两个不同的事物使用相同的标识符。坏消息！

![记住](images/remember.png) 匿名函数是在ES6中引入的，因此如果你需要支持非常旧的浏览器，比如Internet Explorer 11，就不要使用它们。

如果你有一个只在项目中使用一次的函数，现代编程实践认为将其设为匿名函数是一个好主意，这样可以在命名空间中减少一个标识符。

好吧，我听到你在想，早些时候你说我们通过使用函数名来调用函数。如果一个匿名函数没有名字，我们该如何运行它？好问题！我们可以看两个主要方法：

+   将函数赋值给变量

+   用函数本身替换函数调用

### 将匿名函数赋值给变量

上一节的示例代码定义了命名函数`calculateTip()`，并稍后使用`tipCost`变量存储函数结果。这是一个完美的示例，说明在仅使用命名函数计算`tipCost`值时不需要命名函数。当你不需要时给命名空间添加一个身份被称为`polluting`命名空间，在现代JavaScript编程中这是一个大忌。

你可以将这段代码重写为使用匿名函数：

`const preTipTotal = 100.00; const tipPercentage = 0.15;  // 使用匿名函数声明tipCost const tipCost = function (preTip, tipPercent) { const tipResult = preTip * tipPercent; return (tipResult); } const totalBill = preTipTotal + tipCost(preTipTotal, tipPercentage); document.write("Your total bill is $" + totalBill);`

这里最大的变化是，我将`tipCost`变量的值声明为一个匿名函数。这个匿名函数与之前的`calculateTip()`命名函数是相同的，只是没有名字。在倒数第二个语句中，我通过使用`tipCost(preTipTotal, tipPercentage)`调用了匿名函数。 ### 用匿名函数替换函数调用

匿名函数最常见的用途之一是当你需要将一个函数作为参数传递给另一个函数时。被传递的函数被称为`callback`函数。

首先，这里是一个使用命名函数的示例：

`<body> <button id="bgRed"> 将背景设为红色 </button> <button id="bgWhite"> 将背景设为白色 </button> <script> function makeBackgroundRed() { document.body.style.backgroundColor= 'red'; } function makeBackgroundWhite() { document.body.style.backgroundColor= 'white'; } document.getElementById('bgRed').addEventListener( 'click', makeBackgroundRed ); document.getElementById('bgWhite').addEventListener( 'click', makeBackgroundWhite ); </script> </body>`

脚本声明了两个命名函数：`makeBackgroundRed()`和`makeBackgroundWhite()`。代码然后创建了两个事件监听器。其中一个监听`id`值为`bgRed`的按钮的点击事件，当检测到点击时，运行`makeBackgroundRed()`回调函数。另一个事件监听器监听`id`值为`bgWhite`的按钮的点击事件，当检测到点击时，运行`makeBackgroundWhite()`回调函数。有关`document`对象以及`getElementById()`和`addEventListener()`方法的详细信息，请参阅[第6章](c06.xhtml)。

再次，你有两个不需要命名的函数，因此你可以通过用匿名函数替换回调函数来将它们从命名空间中移除。以下是修订后的代码：

`<body> <button id="bgRed"> 将背景设为红色 </button> <button id="bgWhite"> 将背景设为白色 </button> <script> document.getElementById('bgRed').addEventListener( 'click', function() { document.body.style.backgroundColor= 'red'; } ); document.getElementById('bgWhite').addEventListener( 'click', function() { document.body.style.backgroundColor= 'white'; } ); </script> </body>`  ## 使用箭头函数

随着你在JavaScript中的进步，你会发现自己不断使用匿名函数。当你达到那个阶段时，你会高兴地知道ES6还提供了一种更简单的匿名函数语法。也就是说，而不是使用这个：

``function ([*arguments*]) { *JavaScript statements* }``

你可以使用这个：

``([*arguments*]) => { *JavaScript statements* }``

所有我在这里做的就是去掉`function`关键字，并用字符`=`和`>`替换了参数和打开大括号之间的字符。字符`=>`看起来像箭头（JavaScripters称之为`fat arrow`），因此这种语法版本被称为`arrow function`。

![记住](images/remember.png) `箭头函数`是ES6的发明，因此如果你需要支持非常旧的浏览器，如Internet Explorer 11，请不要使用它们。

例如，这里有一个来自早些时候的匿名函数（“[将匿名函数赋值给变量](#c05-sec-0012)”部分）：

``// 使用匿名函数声明tipCost const tipCost = function (preTip, tipPercent) { const tipResult = preTip * tipPercent; return (tipResult); }``

你可以使用箭头函数重写它：

```javascript

如果你的匿名函数由单个语句组成，你可以利用一个称为*隐式返回*的箭头函数特性：

```javascript

这里，JavaScript假设单语句函数意味着函数在执行完语句后立即返回，因此你可以省略花括号和`return`关键字。这是一个例子：

```javascript

类似地，这里是上一节中的一个匿名回调函数：

```javascript

你可以将这段代码重写如下，以使用带有隐式返回的箭头函数：

```javascript
