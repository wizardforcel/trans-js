## `提升`

在JavaScript中，变量和函数可以在实际声明之前被访问，而在JavaScript中描述这种情况的术语是`提升`。

### `var`声明

“提升”这个术语通常与函数声明和使用`var`关键字声明的变量相关。让我们看看`提升`是如何与`var`变量相关的。

考虑以下代码示例：

```js
1 console.log(result); // undefined
2 var result = 5 + 10;

```

你可以在下面的`Replit`中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/hoisting-example1" />`

上述代码的输出显示了`提升`的实际效果。上述代码的第一行在控制台输出`undefined`，但这怎么可能呢？我们如何能够在第二行实际声明之前访问`result`变量？

这是由于在代码执行之前的`解析`步骤使其成为可能。JavaScript代码在执行前的预处理允许JavaScript引擎提前检测到一些错误，而无需执行任何代码。以下代码示例展示了这一过程：

```js
1 function print(obj) {
2   console.log(obj;    // error
3 }
4 
5 console.log("hello world");

```

这里是运行上述代码的`Replit`：

`<ReplitEmbed src="https://replit.com/@newlineauthors/hoisting-example2" />`

如果没有对代码进行任何预处理，JavaScript引擎在函数被调用或调用之前无法检测到`print`函数中的语法错误，而上述代码应该在控制台上记录`hello world`，且不会抛出任何错误，因为包含语法错误的函数尚未被调用。但是上述代码却抛出了错误，而不是在控制台上记录`hello world`。这是为什么呢？答案在于代码执行前的处理步骤。

JavaScript引擎在执行代码之前会扫描代码，这使它能够在执行任何代码之前检测到一些错误。这也使引擎能够通过注册当前作用域中声明的变量来处理变量声明。在任何作用域开始之前，该作用域中声明的所有变量都会被注册。换句话说，在该作用域中的代码执行之前，所有在该作用域中声明的变量都为该作用域保留。这种代码执行前的预处理使得`提升`成为可能。这使我们能够在`var`变量实际声明之前引用它们。

让我们重新审视上面那个将`undefined`记录到控制台的代码示例。

```js
1 console.log(result); // undefined
2 var result = 5 + 10;

```

如果`var`变量是`提升`的，并且我们可以在声明之前引用它们，那么为什么在控制台上记录的是`undefined`而不是`result`变量的实际值，后者应该是`15`呢？

`var`变量的提升问题在于只有它们的`声明`被提升，而不是它们的值。这些变量被赋值为`undefined`，而实际值`15`在代码逐步执行的声明阶段被赋值。

### `函数`声明

函数声明与使用`var`关键字声明的变量一样，也会被提升。以下代码示例展示了函数声明提升的实际情况：

```js
1 startCar(); // starting the car...
2 
3 function startCar() {
4   console.log("starting the car...");
5 }

```

这是运行上述代码的Replit：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/hoisting-example4” />`

如果在变量声明执行之前`var`变量被赋值为`undefined`，我们如何能够在其声明之前调用函数？函数声明的提升与使用`var`关键字声明的变量的提升有什么不同？不同之处在于，函数声明的情况下，函数的名称作为变量在包含函数声明的作用域中被注册，并用函数本身进行初始化。

在上述代码示例中，`startCar`作为变量在全局作用域中注册，并赋值为该函数。与`var`变量不同，函数声明的情况下没有用`undefined`值进行初始化。

在看到函数声明的提升之前，很难想象提升会是编程语言的一个有用特性。能够在函数声明`before`或`after`调用函数确实很有用，解放了开发者使代码安排成每个函数声明都在调用之前的方式。这有助于代码组织，因为我们可以在代码文件的顶部或底部一起声明函数，并从文件中的任何位置调用它们。

### 块内的函数声明

很长一段时间内，块内的函数声明并不属于ECMAScript规范，但在ES2015引入后情况发生了变化。由于在2015年前函数声明不属于规范，并且在JavaScript引擎中被允许，因此不同的引擎处理的方式有所不同。

在ES2015中，ECMAScript规范定义了处理函数声明的`standard`和`legacy`规则。

#### 标准规则

根据标准规则，块内的函数声明会被`hoisted`到块的顶部，转换为函数表达式，并分配给使用`let`关键字声明的变量。

在块内提升的函数仅限于包含块，无法被包含该函数的块外的代码访问。

:::note

重要的是要注意，标准规则仅在[`strict mode`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)中生效。

:::

以下代码示例将帮助你更好地理解块内函数声明的标准规则：

```js
 1 "use strict";
 2 
 3 function process() {
 4  if (true) {
 5    console.log("processing...");
 6 
 7    function fnInsideBlock() {
 8      console.log("I am inside a block");
 9    }
10   }
11 }

```

根据标准规则，`if`块内的函数应如下所示：

```js
 1 "use strict";
 2 
 3 function process() {
 4  if (true) {
 5    let fnInsideBlock = function fnInsideBlock() {
 6      console.log("I am inside a block");
 7    };
 8 
 9    console.log("processing...");
10   }
11 }

```

上述代码中的`fnInsideBlock`函数只能在`if`块内被调用。

#### 旧规则

[遗留规则](https://262.ecma-international.org/13.0/#sec-block-level-function-declarations-web-legacy-compatibility-semantics)适用于 Web 浏览器中的非严格代码。根据遗留规则，除了块内函数声明的`let`变量外，包含函数作用域中还存在一个`var`变量。

让我们以上节中的代码示例为例，添加函数调用：

```js
 1 "use strict";
 2 
 3 function process() {
 4  if (true) {
 5    console.log("processing...");
 6 
 7    function fnInsideBlock() {
 8      console.log("I am inside a block");
 9    }
10   }
11 
12   fnInsideBlock();
13 }
14 
15 process(); // error

```

你可以在下面的 Replit 中运行上述代码：

<ReplitEmbed src="https://replit.com/@newlineauthors/hoisting-example7" />

当上述代码在严格模式下执行时，标准规则适用；因此，上述代码抛出一个错误，因为如上节所解释的，块内的函数被提升到包含作用域的顶部，并且只能在该块内访问。因此，`if`块外的函数调用会抛出错误。

如果上面的代码中移除了`"use strict"`指令，它将会正常执行而不会产生任何错误。这是因为在非严格模式下，块内的函数声明适用遗留规则，而根据遗留规则，块内的提升函数被赋值给在包含函数作用域中声明的`var`变量。

上述代码在非严格模式下执行时，JavaScript 引擎的处理如下所示：

```js
 1 function process() {
 2  var fnInsideBlockVar;
 3 
 4  if (true) {
 5    let fnInsideBlock = function fnInsideBlock() {
 6      console.log("I am inside a block");
 7    };
 8 
 9    console.log("processing...");
10 
11     fnInsideBlockVar = fnInsideBlock;
12   }
13 
14   fnInsideBlockVar();
15 }
16 
17 process();

```

这是一个演示上述代码的 Replit：

<ReplitEmbed src="https://replit.com/@newlineauthors/hoisting-example8" />

:::note

在上面的转换代码中，`fnInsideBlockVar` 和 `fnInsideBlock` 是 JavaScript 引擎背后处理的相同变量。为了说明根据遗留规则块内的函数声明是如何处理的，这些名称看似不同。

:::

现在，应该清楚为什么移除`"use strict"`指令允许代码在没有任何错误的情况下执行。块内的提升函数被赋值给在函数作用域中定义的`var`变量。因此，块内的函数在包含的`if`块外是可访问的。

:::tip

遗留规则复杂且令人困惑；因此，我们不应该依赖于依赖遗留规则的代码来进行块内的函数声明。我们应该在严格模式下编写代码，以防混乱的复杂性进入我们的代码。

:::

##### 深入阅读

+   [ES6 中块级函数的精确语义是什么？ - (stackoverflow 帖子)](https://stackoverflow.com/questions/31419897/what-are-the-precise-semantics-of-block-level-functions-in-es6)

+   [为什么块内赋值会改变全局变量？ - (stackoverflow 帖子)](https://stackoverflow.com/questions/61191014/why-does-block-assigned-value-change-global-variable)

+   [块内函数声明如何将临时值移出块？ - (stackoverflow 帖子)](https://stackoverflow.com/questions/58619924/function-declaration-in-block-moving-temporary-value-outside-of-block)

### 类声明

像函数声明一样，类声明也被提升，但与函数声明相比，它们是*以不同的方式*被提升的。

虽然我们可以在函数声明*之前*访问它，但在类声明的情况下我们不能这样做。这难道不意味着类声明没有被提升吗？不，它们是被提升的，但*以不同的方式*。

让我们先通过以下代码示例验证类声明确实被提升：

```js
1 let Car = "Honda";
2 
3 if (true) {
4   console.log(typeof Car); // error
5 
6   class Car {}
7 }

```

这是一个展示上述代码的Replit：

`<ReplitEmbed src="https://replit.com/@newlineauthors/hoisting-example9" />`

上述代码抛出错误，证明类声明确实被提升。

如果类声明没有被提升，那么`console.log`函数调用应该在控制台打印“Honda”，但事实并非如此。这是因为`if`块中的类声明是被提升的，而任何在`Car`声明之前或之后访问`Car`的代码将会访问类声明，而不是在`if`语句之前声明的`Car`变量。`if`块中标识符`Car`指向类声明而不是在`if`语句之前声明的`Car`变量，这证明了类声明确实是被提升的。

所以，如果类声明是被提升的，为什么我们不能在其声明*之前*访问它们呢？这个问题的答案是“**Temporal Dead Zone (TDZ)**”。

### Temporal Dead Zone (TDZ)

[Temporal Dead Zone (TDZ)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#temporal_dead_zone_tdz)指的是在块级作用域变量（`let`、`const`）或类声明无法被访问的时间。这个时间从作用域的开始到声明被执行的时间开始。以下代码示例将帮助我们可视化TDZ：

```js
1 {
2   // TDZ start
3   console.log("hello");
4   console.log("world");
5   let count = 5; // TDZ end
6 
7   // can access "count" after TDZ ends
8 }

```

TDZ是类声明无法在其声明被执行之前被访问的原因，发生在代码逐步执行的过程中。

#### `let`和`const`

由于TDZ也适用于`let`和`const`，那么使用`let`声明的变量或使用`const`声明的常量也被提升吗？是的，它们也是被提升的，但与类声明一样，它们的提升是*不同的*，因为TDZ的原因。

:::info

这是一个常见的误解，认为块级作用域变量和常量没有被提升，但正如我们之前讨论的，它们是被提升的；只不过它们的提升与使用`var`关键字声明的变量相比是*不同的*。

:::

```js
1 var count = 5;
2 
3 {
4   console.log(count); // hoisted but cannot access due to TDZ
5   let count = 10;
6 }

```

你可以在以下Replit中查看上述代码示例的实际情况：

`<ReplitEmbed src="https://replit.com/@newlineauthors/hoisting-example11" />`

### 函数和类表达式

函数和类表达式没有被提升。考虑以下代码示例：

```js
 1 console.log(typeof Car); // undefined
 2 console.log(typeof Person); // undefined
 3 
 4 var Car = class {
 5  constructor(model) {
 6    this.model = model;
 7  }
 8 };
 9 
10 var Person = function (name) {
11   this.name = name;
12 };

```

这是上述代码示例在Replit中的实际情况：

`<ReplitEmbed src="https://replit.com/@newlineauthors/hoisting-example12" />`

在上述代码示例中，由于变量`Car`和`Person`是使用`var`关键字声明的，我们可以在它们的声明之前访问它们，并且它们的值为`undefined`。这是因为只有声明被提升，而不是它们的值。在上述代码示例中，值是表达式，并没有被提升。

如果我们尝试创建`Car`类的实例或调用`Person`构造函数，我们会遇到一个错误。值得注意的是，在这种情况下我们得到的错误不是引用错误（在未声明标识符的情况下抛出的错误），而是类型错误，这是因为`Car`和`Person`被提升并初始化为`undefined`，我们不能将`undefined`作为构造函数调用。请记住，在这种情况下只有声明被提升，而不是它们的值。

提升可能是一个让人感到困惑的概念，特别是对于初学者，因为提升与`var`变量、函数声明以及ES2015变化（即块作用域变量/常量和ES2015类）之间的差异。

### 关于提升的常见误解

许多JavaScript初学者对提升的概念有误解，认为JavaScript引擎*移动*了提升的声明到文件的顶部。虽然这使得理解提升的概念变得容易，但这并不是现实。

JavaScript引擎不会将提升的声明移动到文件的顶部。相反，它们只是处理声明，然后逐步执行代码。在`var`变量的情况下，它们在声明被执行之前被赋值为`undefined`。在块作用域变量的情况下，它们被标记为“未初始化”。
