## 作用域

作用域是计算机科学领域中的一个概念，指的是程序中可以访问特定变量、函数等的部分。换句话说，标识符（变量、函数等）的作用域是程序中可见或可引用的部分。

现代JavaScript有四种主要的作用域类型，具体如下：

+   全局作用域

+   函数作用域

+   块作用域

+   模块作用域

在讨论上述JavaScript中的作用域类型之前，我们需要理解什么是“词法”作用域。

### 词法作用域

在JavaScript中，不同标识符（变量、函数等）的作用域是在**编译时**确定的。在编译过程中，JavaScript引擎通过分析代码结构来确定在代码中声明的不同标识符的作用域。这意味着在JavaScript代码的逐步执行开始之前，JavaScript引擎会确定代码中不同声明的作用域。

作用域可以嵌套在其他作用域内，每个嵌套的作用域都有权访问外部或父作用域。

```js
1 const myName = "John doe";
2 
3 function hello() {
4   const greeting = "hello " + myName;
5   console.log(greeting);
6 }

```

在上述代码示例中，有三种不同的声明：

+   ``myName``变量声明

+   ``hello``函数声明

    +   ``greeting``变量声明

上述声明的作用域取决于它们在代码结构中的书写位置。``myName``变量和``hello``函数都处于全局作用域，因此在上述代码中全局可用。``greeting``变量声明在``hello``函数内部，因此其作用域是局部于``hello``函数。

这种作用域在编译时通过分析代码结构确定，称为词法作用域。JavaScript并不是唯一拥有词法作用域的语言。其他语言，如Java，也有词法作用域。

:::info

词法作用域也称为“静态”作用域。另一种类型的作用域是[动态作用域](https://en.wikipedia.org/wiki/Scope_(computer_science)#Lexical_scope_vs._dynamic_scope)。

:::

全局作用域通常是包含所有其他嵌套作用域的最外层作用域。每个嵌套作用域都有权访问全局作用域。在JavaScript中，全局作用域是浏览器窗口，或更准确地说，是浏览器窗口标签。全局作用域通过``window``对象暴露给JavaScript代码。

使用``var``关键字创建的变量或在全局作用域中声明的函数声明被添加为``window``对象的属性。以下代码示例验证了这一说法：

```js
1 var todoList = ["grocery", "exercise", "meeting"];
2 
3 function emptyTodoList() {
4   todoList = [];
5 }
6 
7 console.log(window.hasOwnProperty("todoList")); // true
8 console.log(window.hasOwnProperty("emptyTodoList")); // true

```

如果``todoList``是使用``let``或``const``声明的，它就不会作为``window``对象的属性被添加，但它仍然是一个全局变量。同样，如果``emptyTodoList``是函数表达式而不是函数声明，并且引用这个函数表达式的标识符是使用``let``或``const``声明的，它也不会作为``window``对象的属性。相反，它只是一个全局函数表达式。

```js
1 const todoList = ["grocery", "exercise", "meeting"];
2 
3 let emptyTodoList = function () {
4   todoList = [];
5 };
6 
7 console.log(window.hasOwnProperty("todoList")); // false
8 console.log(window.hasOwnProperty("emptyTodoList")); // false

```

### 避免污染全局作用域

*“避免污染全局作用域”* - 作为一名`JavaScript`开发者，你要么已经听过这个建议，要么迟早会从某人那里听到。但“污染”全局作用域究竟意味着什么？为什么应该避免它？

声明所有内容（不必要地）在全局作用域中被视为“污染”全局作用域。全局作用域中声明过多可能导致不必要的问题。

全局作用域是所有其他作用域的父作用域；因此，全局作用域中的声明对所有其他作用域都是可见的。这可能导致变量名称冲突、遮蔽等问题。全局作用域的另一个特点是，直到应用程序关闭，它才会被销毁，因此如果我们不小心，全局作用域中的声明可能会一直保留在内存中，无论它们是否需要，直到应用程序关闭。

说到这里，全局作用域中的声明通常是不可避免的。因此，我们能做的就是尽量避免全局作用域。将全局声明保持在最低限度。如果一个变量仅在函数内部使用，就没有必要在全局作用域中声明它。

所以，如果你之前没听说过，现在你听到了：“*避免污染全局作用域*。”

### `隐式全局`

`JavaScript`作为一种语言有许多怪癖。其中之一是隐式创建全局变量。每当对一个*未声明*变量进行赋值时，`JavaScript`会将该未声明的变量声明为一个**全局**变量。这很可能是程序员的错误，而`JavaScript`并不抛出错误，而是通过自动声明一个同名的全局变量来隐藏这一点。

```js
1 function printSquare(num) {
2   result = num * num;
3   console.log(result); // 64
4 }
5 
6 printSquare(8);
7 
8 console.log("implicit global: " + result); // WHAT??!!

```

下面是上面代码在`Replit`中的实际运行：

`<ReplitEmbed src="https://replit.com/@newlineauthors/global-scope-example3" />`

注意，`result`变量并未被声明。它被赋值为乘法结果，仿佛它已经被声明。正常情况下，人们会期待在这种情况下抛出错误，但`JavaScript`会为你将`result`声明为全局变量。

需要提到的是，这种奇怪的行为仅在非严格模式下发生。在严格模式下，`JavaScript`会抛出错误，通知程序员对未声明变量的赋值。

这也是始终在严格模式下编写`JavaScript`代码的原因之一。使用严格模式可以避免`JavaScript`的这种混淆行为影响我们的代码。

#### `HTML`属性

除了对未声明变量的赋值，还有另一种方式我们会获得*隐式*全局变量。`HTML`元素的`id`属性或`name`属性的值也会作为变量添加到`JavaScript`的全局作用域中。

```js
1 <h1 id="mainHeading">Hello World!</h1>

```

上述`h1`元素的`id`被作为变量添加到全局作用域。我们可以在JavaScript代码中使用`mainHeading`作为变量来访问`h1`元素。这个特性被称为[Window对象的命名访问](https://html.spec.whatwg.org/multipage/nav-history-apis.html#named-access-on-the-window-object)。

这一点最初是由`Internet Explorer`浏览器添加的，并逐渐在其他浏览器中实现，仅仅是出于兼容性原因。有些网站依赖于这种行为，因此为了向后兼容，浏览器别无选择，只能实现这种行为。

虽然大多数浏览器支持此功能，但不应过于依赖此特性，我们应该始终使用标准机制来定位HTML元素。应使用像`getElementById`或`querySelector`这样的函数，而不是依赖这种行为。

编写依赖于此特性的代码是个坏主意，因为这可能导致代码难以阅读和维护。想象一下，在代码中看到一个标识符却无法识别它的声明位置。这样的代码容易与我们代码中的其他变量发生名称冲突。此外，请记住，如果HTML标记发生变化，依赖于HTML标记的代码可能会很容易中断。简而言之，避免依赖此特性，并在JavaScript代码中使用更好的替代方案来定位HTML元素。

##### 进一步阅读

+   [全局变量是不好的 - （文章）](http://wiki.c2.com/?GlobalVariablesAreBad)

+   [带有ID的DOM树元素是否会变成全局属性？ - （stackoverflow帖子）](https://stackoverflow.com/questions/3434278/do-dom-tree-elements-with-ids-become-global-properties)

函数作用域指的是函数体内的代码区域。函数作用域从函数体的开括号开始，到闭括号之前结束。函数作用域内的声明仅限于该函数的作用域，无法被该函数外部的代码直接访问。

### 遮蔽声明

嵌套作用域内的声明可以“遮蔽”外部作用域中同名的声明。这被称为“遮蔽声明”或简单地称为“遮蔽”。

请考虑以下代码示例：

```js
1 let hobby = "reading";
2 
3 function printHobbies() {
4   const hobby = "traveling";
5   console.log(hobby); // traveling
6 }
7 
8 printHobbies();

```

这里是上面代码的`Replit`：

`<ReplitEmbed src="https://replit.com/@newlineauthors/function-scope-example1">`

函数内部的变量`hobby`正在遮蔽全局作用域中声明的`hobby`变量。

通常不理想去遮蔽其他声明，因为这会降低代码的可读性。这也可能使得嵌套作用域中的代码无法访问被遮蔽的声明。请考虑以下代码示例：

```js
1 let prefix = ">";
2 
3 function log(logLevel, msg) {
4   let prefix = ":::";
5   console.log(`${prefix}${logLevel} : ${msg}`);
6 }
7 
8 log("debug", "error caught"); // ::: debug : error caught

```

这里是上面代码的`Replit`：

`<ReplitEmbed src="https://replit.com/@newlineauthors/function-scope-example2">`

在上面的代码示例中，我们已经遮蔽了在全局作用域中声明的`prefix`变量，而`log`函数内部的代码无法访问全局`prefix`变量。

:::note

回想一下，全局作用域中的`var`声明作为属性添加到`window`对象上。因此，如果全局`prefix`变量是使用`var`关键字声明的，我们可以使用`window.prefix`来访问被遮蔽的变量。

::::

### `函数参数作用域`

一个常见的误解是函数参数是在函数的局部作用域中定义的，或者参数的行为就像是在函数的局部作用域中定义的一样，但这并不总是正确的。

首先，我们需要区分“简单”和“非简单”参数列表。如果函数参数是以使用ES2015+特性（如[默认参数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)、[解构](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)或[剩余参数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)）的方式定义的，这些参数被视为`非简单`参数；如果参数不使用任何这些特性，则被视为`简单`参数。

```js
1 function simpleParameters(val1, val2) {
2   // code...
3 }
4 
5 function nonSimpleParameters(val1 = 12, ...restParams) {
6   // code...
7 }

```

如果参数是简单的，它们的行为就像是在函数的局部作用域中声明的，但如果参数是非简单的，它们是在自己的作用域中声明的。非简单参数作用域可以被看作是在函数作用域与包含函数的作用域之间。

如果具有非简单参数的函数在全局作用域中定义，其参数作用域可以被概念化为如下图所示：

![函数参数作用域](images/module_03----lesson_03.03----public----assets----parameter-scope.png)

`函数参数作用域`

以下代码示例证明非简单参数确实存在于与函数的局部作用域不同的作用域中：

```js
1 function paramScope(arr = ["initial array"], buff = () => arr) {
2   var arr = [1, 2, 3];
3   console.log(arr); // [1, 2, 3]
4   console.log(buff()); // ["initial array"]
5 }
6 
7 paramScope();

```

这里是上述代码的`Replit`：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/function-scope-example4”>`

上述代码示例中的`paramScope`函数具有非简单参数列表；第一个参数`arr`具有数组作为默认值，而第二个参数`buff`具有函数作为默认值。

在函数内部，有一个与`paramScope`函数的第一个参数同名的`var`声明。函数内部的两个`console.log`调用在控制台上打印了两个不同的值；这是为什么呢？为什么`buff`参数返回的是`arr`参数的默认值，而不是函数局部作用域内的`arr`的值？

答案是，`arr`参数和函数内部的`arr`变量是两个存在于两个`不同`作用域的`不同`变量。函数内部的`arr`遮蔽了`arr`参数，但调用`buff`函数时返回的是参数`arr`。如果参数和局部的`arr`是同一个变量，`buff`函数将返回`[1, 2, 3]`而不是`arr`参数的默认值。

删除函数内部的`var`关键字以显示不同的输出：

```js
1 function paramScope(arr = ["initial array"], buff = () => arr) {
2   arr = [1, 2, 3];
3   console.log(arr); // [1, 2, 3]
4   console.log(buff()); // [1, 2, 3]
5 }
6 
7 paramScope();

```

这里是上述代码的`Replit`：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/function-scope-example5”>`

现在函数内部的`arr`指的是`arr`参数，因此在函数内部对`arr`的任何赋值在调用`buff`函数时都会反映出来。

### 函数表达式名称作用域

函数表达式大多以匿名函数表达式的形式编写，如下所示：

```js
1 let fn = function () {
2   // code ...
3 };

```

这是一个匿名函数表达式，被赋值给`fn`变量。

我们也可以写一个`命名`函数表达式，如下所示：

```js
1 let fn = function namedFn() {
2   // code ...
3 };

```

在上面的代码示例中，函数表达式`namedFn`的名称仅在函数体内部可访问。因此，有些人可能错误地认为命名函数表达式的名称是在函数体内部声明的，但这并不正确；名称是在`不同`作用域中声明的。以下代码证明了这一点：

```js
1 let fn = function namedFn() {
2   let namedFn = 123;
3   console.log(namedFn);
4 };

```

这是上面代码的Replit：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/function-scope-example8”>`

`let`不允许重新声明变量。因此，如果`nameFn`是在函数作用域内部声明的，那么上面的代码示例应该会抛出一个错误；相反，没有错误，这段代码是有效的。函数体内的`nameFn`实际上是遮蔽了函数表达式的名称。

命名函数表达式的名称作用域位于包含函数表达式的作用域和函数表达式的局部作用域之间，类似于上述讨论的非简单参数列表的作用域。

##### 进一步阅读

+   [参数在词法环境中的位置在哪里？ - (stackoverflow帖子)](https://stackoverflow.com/questions/61208843/where-are-arguments-positioned-in-the-lexical-environment/)

+   [隐含作用域](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/apA.md#implied-scopes)

+   [命名函数表达式 - (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/function#named_function_expression)

### 块作用域

JavaScript中的块作用域是指在代码块之间存在的作用域，例如`if`块或循环。

在JavaScript语言引入块作用域的`let`和`const`之前，使用`var`关键字在块中定义的变量在该块外部也可以访问。这是因为使用`var`关键字声明的变量具有函数作用域。然而，使用`let`声明的变量或使用`const`声明的常量仅限于其定义的块，除非它们在全局作用域中声明，这样会使它们成为全局变量。

块作用域的`let`和`const`解决了诸如不必要的变量暴露在块外、循环中的闭包等问题。我们将在与闭包主题相关的模块中讨论循环中的闭包问题。

另一个关于块作用域需要了解的事情是如何处理块内部的函数声明。这在与提升相关的模块中讨论过。

### `模块作用域`

模块也是近年来添加到JavaScript中的特性之一。模块解决了涉及多个JavaScript文件的代码库中存在的许多代码管理问题。模块使我们能够将代码分割成可管理的块。

在ES模块内部的代码存在于模块作用域中。换句话说，模块内部的声明仅限于该模块，并且不会暴露到模块外部，除非是`explicitly`从模块导出的代码。模块顶部级别的声明仅限于模块，并不属于全局作用域。

##### 进一步阅读

+   [JavaScript模块 - (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules#other_differences_between_modules_and_standard_scripts)

+   [ES模块：卡通深入探讨 - (MDN)](https://hacks.mozilla.org/2018/03/es-modules-a-cartoon-deep-dive/)

### `作用域链`

不同的作用域可以嵌套在其他作用域内部，形成作用域链。这被称为`scope chain`。

每次创建新的作用域时，它都会链接到其封闭作用域。不同作用域之间的这种链接创建了一个作用域链，可以用于查找在当前作用域中找不到的标识符。

当在特定作用域中遇到标识符时，JavaScript引擎会在当前作用域的父作用域中查找该变量的声明。如果在父作用域中未找到该声明，则JavaScript引擎会在父作用域的外部（父）作用域中查找该变量声明。这个遍历作用域链的过程将继续，直到到达全局作用域，并且没有其他作用域可供查找该声明。

考虑以下代码示例：

```js
 1 const myName = "John doe";
 2 
 3 function hello() {
 4  const greeting = "hello " + myName;
 5 
 6  function greet() {
 7    console.log(greeting);
 8  }
 9 
10   greet();
11 }
12 
13 hello();

```

您可以在这个Replit中预览上面的代码：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/scope-chain-example1”>`

由`hello`函数调用创建的作用域链可以概念上可视化如下：

![作用域链](images/module_03----lesson_03.06----public----assets----scope-chain.png)

`作用域链`

作用域链使得能够查找当前作用域中未声明的标识符。

#### 优化作用域链查找

现代 JavaScript 应用程序包含许多行必须在最短时间内编译和执行的 JavaScript 代码，以确保应用用户不会经历较差的应用性能。因此，现代 JavaScript 引擎对我们编写的 JavaScript 代码进行了大量优化，以使其尽可能高效地执行。在代码执行之前，对代码进行转换时会执行不同的优化。优化不仅限于代码执行`前`的步骤，代码在执行过程中也会进行优化（回忆一下 `JIT` 编译）。

由于 JavaScript 的作用域是在编译时确定的，在大多数情况下，这些信息允许 JavaScript 引擎避免在代码执行期间遍历作用域链。如果 JavaScript 已经知道某个特定变量定义在哪个作用域中，那么每次在当前作用域中找不到特定变量声明时遍历作用域链是极其低效的。

因此，除非在编译时无法确定变量的作用域，JavaScript 引擎在运行时不需要遍历作用域链。然而，可能会有某些情况，在编译时无法确定特定标识符的作用域；在这些情况下，JavaScript 引擎别无选择，只能在运行时遍历作用域链以确定该标识符声明在哪个作用域中。

##### 深入阅读

+   [作用域链](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/ch3.md)
