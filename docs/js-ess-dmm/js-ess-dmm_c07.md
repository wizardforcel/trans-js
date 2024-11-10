第 7 章

# 工作与数组

本章内容

![Bullet](images/check.png) **声明数组变量**

![Bullet](images/check.png) **用数据填充数组**

![Bullet](images/check.png) **迭代数组**

![Bullet](images/check.png) **使用 JavaScript 的``Array``对象**

在本章中，您将通过探索 JavaScript 最重要的概念之一——数组，将编码效率提升到一个新的水平。数组不仅因为它们极其高效且功能强大而重要，还因为一旦您知道如何使用它们，您将想出无数种用途。为了确保您准备好迎接充满数组的新生活，本章解释了它们是什么以及它们为何如此有用，然后探讨了数组如何让您的编码生活更轻松的所有奇妙方式。## 什么是数组？

在 JavaScript 中，每当您有一个相关数据的变量集合时，可以将它们组合到一个叫做``array``的单一变量中。您可以将任意数量的值输入数组，JavaScript 使用``index number``跟踪每个值。例如，您添加的第一个值的索引为 0。您放入数组的第二个值的索引为 1；第三个值的索引为 2；依此类推。然后，您可以通过指定您想要的索引号访问数组中的任何值。## 声明数组

因为数组是一种变量类型，所以在使用之前需要声明它。您可以使用四种语法。以下是最具信息性的语法：

``const arrayName = new Array();``

这里，``arrayName``是您想要用作数组变量名称的名称。

在 JavaScript 中，数组实际上是一个对象，因此``new``关键字在这里的作用是创建一个新的``Array``对象。语句中的``Array()``部分称为``constructor``，因为它的工作是在内存中构造对象。例如，要创建一个名为``dogPhotos``的新数组，您可以使用以下语句：

``const dogPhotos = new Array();``

第二种语法在您预先知道要放入数组的值（或``elements``）数量时非常有用：

``const arrayName = new Array(num);``

各个部分如下：

+   ``arrayName``：你想要使用的数组变量名称

+   ``num``：你将要放入数组的值的数量

例如，这里有一个声明新``dogPhotos``数组的语句，包含五个元素：

``const dogPhotos = new Array(5);`` ## 填充数组

在声明数组后，您可以开始用要存储的数据值填充它。以下是这样做的一般语法：

``arrayName[index] = value;``

各个部分如下：

+   ``arrayName``：你想要使用的数组变量名称

+   ``index``：您希望存储值的数组索引号

+   ``value``：你在数组中存储的值

JavaScript 准许将几乎任何类型的数据放入数组中，包括数字、字符串、布尔值，甚至其他数组！你甚至可以在一个数组中混合多种数据类型。

作为示例，这里有几个语句，声明一个名为 `dogPhotos` 的新数组，然后将五个字符串值输入数组：

``const dogPhotos = new Array(5); dogPhotos[0] = "dog-1"; dogPhotos[1] = "dog-2"; dogPhotos[2] = "dog-3"; dogPhotos[3] = "dog-4"; dogPhotos[4] = "dog-5";``

要引用一个数组值（例如，在表达式中使用它），你指定相应的索引：

``strURL + dogPhotos[3]``

### 同时声明并填充数组

之前，我提到 JavaScript 还有两种其他语法用于声明数组。两者都使你能够仅用一个语句声明一个数组并填充它。

第一种方法使用 `Array()` 构造函数，其一般格式如下：

``const arrayName = new Array(value1, value2, …);``

这里是各个部分的含义：

+   `arrayName`：你想要使用的数组变量的名称

+   `value1, value2, …`：你想用来填充数组的初始值

这里是一个例子：

``const dogPhotos = new Array("dog-1", "dog-2", "dog-3", "dog-4", "dog-5");``

JavaScript 还支持创建 `array literals`。你通过将一个或多个值放在方括号中来创建数组字面量。这里是一般格式：

``const arrayName = [value1, value2, …];``

这里是各个部分的含义：

+   `arrayName`：你想要使用的数组变量的名称

+   `value1, value2, …`：你想用来填充数组的初始值

一个例子：

``const dogPhotos= ["dog-1", "dog-2", "dog-3", "dog-4", "dog-5"];``

大多数 JavaScript 程序员更喜欢这种语法而不是使用 `Array` 构造函数。 ### 使用循环填充数组

你可以使用循环和某种计数变量以编程方式访问数组的索引号来填充数组。这里是一个例子：

``const dogPhotos = []; for (let counter = 0; counter < 5; counter += 1) { dogPhotos[counter] = "dog-" + (counter + 1); }``

`for()` 循环中的语句使用变量 `counter` 作为数组的索引。例如，当 `counter` 为 `0` 时，语句看起来像这样：

``dogPhotos[0] = "dog-" + (0 + 1);``

在这种情况下，等号右边的表达式的值为 `"dog-1"`，这是正确的值。 ## 迭代数组

数组确实可以帮助使你的代码更高效，通过使你能够将这些冗长的过程缩短为适合函数的更短例程。这些例程是 `Array` 对象的迭代方法，其中 `iterative` 意味着方法遍历数组中的项目，并且对于每个项目，一个函数（称为 `callback`）对该项目执行某种操作。

`Array`对象实际上有14种迭代方法。我不会涵盖它们全部，但在接下来的几节中，我会讨论最有用的几种。

### 迭代数组：`forEach()`

`Array`对象的`forEach()`方法为数组中的每个元素运行一个回调函数。该回调最多接受三个参数：

+   `value`：元素的值。

+   `index`：可选，元素的数组索引。

+   `array`：可选，被迭代的数组。

您可以使用以下任何语法：

`*array*.forEach(*namedFunction*); *array*.forEach(function (*value*, *index*, *array*) { *code* }); *array*.forEach((*value*, *index*, *array*) => { *code* });`

各部分的具体内容如下：

+   `array`：您要迭代的`Array`对象。

+   `namedFunction`：一个现有函数的名称。此函数应接受`value`参数，并可能还接受可选的`index`和`array`参数。

+   `code`：在每次迭代中运行的语句。

这里有一个示例：

`// Declare the array const dogPhotos= ["dog-1", "dog-2", "dog-3", "dog-4", "dog-5"];  // Iterate through the array dogPhotos.forEach((value, index) => { console.log("Element " + index + " has the value " + value); });`  ### 迭代以创建新数组：`map()`

当您迭代一个数组时，通常会对每个元素值应用某些操作。然而，在某些情况下，您希望保留原始数组值并创建一个包含更新值的新数组。

创建一个新数组以存储现有数组的更新值的最简单方法是使用`Array`对象的`map()`方法。您可以使用三种语法：

`*array*.map(*namedFunction*); *array*.map(function (*value*, *index*, *array*) { *code* }); *array*.map((*value*, *index*, *array*) => { *code* });`

各部分的具体内容如下：

+   `array`：您要使用的值的`Array`对象。

+   `namedFunction`：一个现有函数的名称，该函数在每个数组值上执行操作。此函数应接受`value`参数，并可能还接受可选的`index`和`array`参数。

+   `code`：在每次迭代中运行的语句，以对每个值执行操作。

`map()`方法返回一个包含更新值的`Array`对象，因此请确保将结果存储在一个变量中。

这里有一个示例：

`// Declare an array of Fahrenheit temperatures const tempsFahrenheit = [-40, 0, 32, 100, 212];  // Convert each array value to Celsius const tempsCelsius = tempsFahrenheit.map(currentTemp => { return (currentTemp - 32) * 0.5556; });  // Output the result console.log(tempsCelsius);`  ### 迭代数组到一个值：`reduce()`

一个常见的迭代模式是在数组的每个元素上执行累加操作，以生成一个值。例如，您可能想知道数组中所有值的总和。

以这种方式迭代数组并生成一个值是`Array`对象的`reduce()`方法的工作。您可以使用三种语法：

`array.reduce(namedFunction, initialValue); array.reduce(function (accumulator, value, index, array) { code }, initialValue); array.reduce((accumulator, value, index, array) => { code }, initialValue);`

各部分内容如下：

+   `array`：您希望减少的值的`Array`对象。

+   `namedFunction`：执行每个数组值的累加操作的现有函数的名称。此函数应接受`accumulator`和`value`参数，并可能还接受可选的`index`和`array`参数。

+   `code`：在每次迭代中运行的语句，以对每个值执行操作。

+   `initialValue`：`accumulator`的起始值。如果省略`initialValue`，JavaScript将使用数组中第一个元素的值。

这里有一个示例：

`// Declare an array of product inventory const unitsInStock = [547, 213, 156, 844, 449, 71, 313, 117];  // Get the total units in stock const initialUnits = 0; const totalUnits = unitsInStock.reduce((accumulatedUnits, currentInventoryValue) => { return accumulatedUnits + currentInventoryValue; }, initialUnits);  // Output the result console.log("Total units in stock: " + totalUnits);`  ### 迭代以定位元素：`find()`

要在数组中查找第一个匹配某个条件的元素，使用`Array`对象的`find()`方法。您可以使用三种语法：

`array.find(namedFunction); array.find(function (value, index, array) { code }); array.find((value, index, array) => { code });`

下面是各部分的说明：

+   `array`：包含要搜索的值的`Array`对象。

+   `namedFunction`：现有函数的名称，该函数将条件应用于每个数组值。此函数应接受`value`参数，也可能接受可选的`index`和`array`参数。

+   `code`：在每次迭代期间运行的语句，用于将条件应用于每个值。

在`namedFunction`或`code`中，您设置一个逻辑条件，测试数组中的每个元素，并使用`return`语句将测试的结果返回给`find()`方法。`find()`方法返回的最终值是第一个测试结果为`true`的元素，或者如果所有数组元素的测试结果为`false`，则返回`undefined`。

这是一个示例：

`// 声明一个产品对象数组 const products = [ { name: 'doodad', units: 547 }, { name: 'gizmo', units: 213 }, { name: 'gimcrackery', units: 156 }, { name: 'knickknack', units: 844 }, { name: 'bric-a-brac', units: 449 }, { name: 'thingamajig', units: 71 }, { name: 'watchamacallit', units: 313 }, { name: 'widget', units: 117 } ];  // 查询数组 const strQuery = "gizmo"; const stock = products.find((currentProduct) => { return currentProduct.name === strQuery; });  // 输出结果 if (stock) { console.log("产品 " + stock.name + " 有 " + stock.units + " 个库存。"); } else { console.log("未找到产品 " + strQuery + "。"); }`  ## 操作数组

就像任何好的对象一样，`Array`带有一大堆属性和方法，您可以使用它们并进行操作。本章的其余部分将介绍一些最有用的属性和方法。

### length属性

`Array`对象只有几个属性，但其中唯一一个您会经常使用的是`length`属性：

`array.length`

`length`属性返回当前指定数组中的元素数量。 ### 一些有用的数组方法

有许多方法与数组相关，但由于空间限制，我无法详细介绍它们。为了激发你的兴趣，[表7-1](#c07-tbl-0001)列出了几种最有用的数组方法。

[TABLE 7-1](#rc07-tbl-0001) 有用的数组方法

| 方法 | 语法 | 描述 |
| --- | --- | --- |
| `concat()` | `array.concat(array1, array2, …)` | 将一个或多个现有数组的元素连接到现有数组中，以创建一个新数组。 |
| `join()` | `array.join(separator)` | 获取数组中的现有值并将它们连接成一个字符串。 |
| `pop()` | `array.pop()` | 移除数组中的最后一个元素，并返回该元素的值。 |
| `push()` | `array.push(value1, value2, …)` | 向数组末尾添加一个或多个元素。 |
| `reverse()` | `array.reverse()` | 反转指定数组中元素的顺序。 |
| `shift()` | `array.shift()` | 移除数组中的第一个元素，并返回该元素的值。 |
| `slice()` | `array.slice(start, end)` | 返回一个新数组，该数组包含现有数组中某个子集的元素。 |
| `sort()` | `array.sort()` | 对指定的数组进行排序。 |
| `unshift()` | `array.unshift(value1, value2, …)` | 在数组开头插入一个或多个值，并返回数组的新长度。 |
