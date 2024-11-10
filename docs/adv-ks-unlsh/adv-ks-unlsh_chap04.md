## 闭包

闭包是 JavaScript 中的基本主题之一，对于初学者来说可能比较难以理解。它是一个强大的特性，深入理解这一主题是至关重要的。在本模块中，我们将更深入地探讨闭包是什么以及它们是如何工作的。

### 什么是闭包？

闭包是以下两个事物的组合：

+   一个 `Function`

+   对于创建该函数的环境/作用域的引用

换句话说，每当我们在 JavaScript 中定义一个函数时，该函数会保存一个对其创建环境的引用。这被称为闭包：一个函数以及对其创建环境的引用。

闭包允许嵌套函数访问包含函数内部的声明，即使包含函数的执行已经结束。

```js
 1 function outerFn() {
 2  const outerVar = 123;
 3 
 4  return function inner() {
 5    console.log(outerVar);
 6  };
 7 }
 8 
 9 const innerFn = outerFn();
10 innerFn();

```

这是上述代码的一个 Replit：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/Example1”>`

返回的 `innerFn` 函数是如何访问在 `outerFn` 中声明的 `outerVar` 变量的，即使在`outerFn`执行完成后？

上述代码之所以有效，是因为 JavaScript 函数在创建时总是会创建闭包。在某些编程语言中，函数的局部变量仅在该函数执行期间存在；当函数执行结束时，其局部作用域中定义的变量会被销毁。但在 JavaScript 中并非如此，这从上面的代码示例中可以明显看出。那么，闭包是如何工作的呢？

### 闭包是如何工作的？

要理解闭包是如何工作的，我们需要理解 JavaScript 如何解析任何标识符的作用域。

尽管我们在之前的一个模块中详细讨论了作用域，但我们还是简单回顾一下词法作用域是如何解析的。考虑以下代码示例：

```js
1 let isReading = true;
2 
3 function learnJavaScript() {
4   console.log(isReading);
5 }
6 
7 learnJavaScript();

```

这是上述代码的一个 Replit：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/Example2”>`

当调用 `learnJavaScript` 函数以记录 `isReading` 变量的值时，JavaScript 首先需要识别该变量的定义位置。JavaScript 首先搜索的地方是 `learnJavaScript` 函数的局部作用域，因为在这里找到了对 `isReading` 变量的引用。

由于 `isReading` 变量没有在 `learnJavaScript` 函数的局部作用域中定义，JavaScript 将在外部作用域中搜索该变量，在此情况下是全局作用域。JavaScript 会在全局作用域中找到 `isReading` 变量的声明，因此会获取其值并将其传递给 `console.log` 函数，以便将其记录到控制台。

让我们看一个涉及嵌套函数的代码示例：

```js
 1 let isReading = true;
 2 
 3 function learnJavaScript() {
 4  function stepsToLearnJavaScript() {
 5    console.log(isReading);
 6  }
 7 
 8  stepsToLearnJavaScript();
 9 }
10 
11 learnJavaScript();

```

这是上述代码的一个 Replit：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/Example3”>`

在这个代码示例中，我们有一个嵌套函数 `stepsToLearnJavaScript`，它记录了在全局作用域中定义的变量的值。如果 JavaScript 还没有确定 `isReading` 变量的作用域，它将如何找到它的声明？回想一下作用域链！

JavaScript 将需要遍历作用域链以找到 `isReading` 变量的声明。与之前的示例一样，首先在当前作用域中搜索声明，在本例中是 `stepsToLearnJavaScript` 函数的局部作用域。如果当前作用域中没有 JavaScript 正在寻找的声明，搜索将顺序扩展到外部作用域。在我们的示例中，`stepsToLearnJavaScript` 函数中没有 `isReading` 变量的声明，因此搜索移向外部作用域，而在本例中是 `learnJavaScript` 函数的局部作用域。这个作用域中也不存在该声明；JavaScript 继续向外部作用域遍历，当前外部作用域是全局作用域。

在上面的代码示例中，变量声明是在全局作用域中找到的，因此当搜索达到全局作用域时，变量声明的搜索将被停止。但是如果我们从上述代码示例中删除变量声明，会发生什么呢？

```js
1 function learnJavaScript() {
2   function stepsToLearnJavaScript() {
3     console.log(isReading);
4   }
5 
6   stepsToLearnJavaScript();
7 }
8 
9 learnJavaScript();

```

这里是上面代码的 Replit：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/Example4”>`

现在，`stepsToLearnJavaScript` 函数正在记录一个未声明的变量。那么，当搜索变量声明达到全局作用域时，会发生什么呢？此时，JavaScript 将执行以下两件事之一：

+   如果代码在严格模式下，将抛出错误

+   在非严格模式下为您声明一个全局变量（回顾一下作用域模块中的“隐式全局”）

### 不同的作用域是如何链接的？

此时，我们知道作用域是如何解析的，不同的作用域是如何连接在一起的，形成了一个称为“作用域链”的链条。但你有没有想过不同的作用域是如何连接的？这不可能是魔法；一定有某种机制将不同的作用域连接在一起。JavaScript 如何确定当前作用域的外部作用域？

让我们回顾一下本课之前展示的代码示例：

```js
1 let isReading = true;
2 
3 function learnJavaScript() {
4   console.log(isReading);
5 }
6 
7 learnJavaScript();

```

这里是上面代码的 Replit：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/Example5”>`

我们知道，当 `learnJavaScript` 函数被调用时，这个函数的局部作用域与全局作用域是连接在一起的，但这是如何实现的呢？答案是一个名为 `[[[Environment]]]` 的隐藏内部槽位（[https://tc39.es/ecma262/#table-internal-slots-of-ecmascript-function-objects](https://tc39.es/ecma262/#table-internal-slots-of-ecmascript-function-objects)）。这个 `[[Environment]]` 内部槽位存在于函数中，并且包含对外部作用域/环境的引用。换句话说，这个内部槽位包含了包含函数“闭合”或形成“闭包”的作用域的引用。

`:::info`

在 ECMAScript 规范中提到了许多 [隐藏内部槽](https://stackoverflow.com/questions/33075262/what-is-an-internal-slot-of-an-object-in-javascript)。规范利用这些隐藏内部槽来定义所需的行为。这些隐藏内部槽，和抽象操作一样，可能并不是由不同 JavaScript 引擎实际实现的东西。  

:::  

在上面的代码示例中，当 `learnJavaScript` 函数被创建时，由于它是在全局作用域中创建的，因此对全局环境的引用被保存在函数对象的内部 `[[Environment]]` 槽中。稍后，当函数被调用时，会为函数内部代码的执行创建一个新的环境。这个环境（函数的局部作用域）通过获取保存在 `learnJavaScript` 函数的 `[[Environment]]` 槽中的值并将其保存在名为 `[[[OuterEnv]]]` 的内部槽中，从而与全局环境相链接（https://tc39.es/ecma262/#sec-environment-records）。每个环境对象都有一个内部槽，包含对外部环境的引用。  

上述示例中作用域的链接可以在下面的图像中概念性地可视化：  

![作用域链接](images/missing.png)

`作用域链接`  

让我们回顾一下本课中涉及嵌套函数的早期示例：  

```js
 1 let isReading = true;
 2 
 3 function learnJavaScript() {
 4  function stepsToLearnJavaScript() {
 5    console.log(isReading);
 6  }
 7 
 8  stepsToLearnJavaScript();
 9 }
10 
11 learnJavaScript();

```

这里是上面代码的 Replit：  

<ReplitEmbed src=”https://replit.com/@newlineauthors/Example6”>  

在这个代码示例中，我们有三个不同的环境：  

+   全球环境  

+   `learnJavaScript` 函数的局部环境（在函数被调用时创建）  

+   `stepsToLearnJavaScript` 函数的局部环境（在函数被调用时创建）  

不同作用域之间的链接可以在下面的图像中可视化：  

![作用域链接](images/module_05----lesson_05.01----public----assets----closure-scope-linkage-2.png)  

`作用域链接`  

希望以上两个代码示例和图像能够阐明不同作用域是如何链接在一起，形成作用域链的。这个作用域链在需要时由 JavaScript 引擎遍历，以解析任何标识符的作用域。  

这种不同环境之间的链接，即作用域链，使得 JavaScript 中的闭包成为可能。由于这个作用域链，嵌套函数即使在外部函数执行结束后，仍然可以访问外部函数的变量。只要内部函数有对外部环境的引用，外部环境就会保留在内存中。  

现在，让我们回顾一下本课中的第一个代码示例，该示例涉及从与定义该嵌套函数不同的作用域中调用嵌套函数。  

```js
 1 function outerFn() {
 2  const outerVar = 123;
 3 
 4  return function inner() {
 5    console.log(outerVar);
 6  };
 7 }
 8 
 9 const innerFn = outerFn();
10 innerFn();

```

这里是上面代码的 Replit：  

<ReplitEmbed src=”https://replit.com/@newlineauthors/Example7”>  

希望你现在能够解释为什么嵌套函数在 `outerFn` 执行完成后仍然能够访问 `outerVar` 变量。  

`inner`函数对`outerFn`函数的局部作用域有一个引用，保存在其`[[Environment]]`内部槽中。当从`outerFn`函数返回`inner`函数时，尽管`outerFn`的执行已经结束，`inner`函数仍然保留对`outerFn`局部作用域的引用。当调用`inner`函数时，`inner`函数的`[[Environment]]`槽的值会保存在为执行`inner`函数创建的环境的`[[OuterEnv]]`内部槽中。

总结来说，每当创建一个JavaScript函数时，都会形成一个闭包，这使得该函数可以访问在其定义时有效的作用域链。每次创建函数时，JavaScript都会在函数对象的内部`[[Environment]]`槽中保存对函数周围环境的引用。当调用该函数时，会为该函数调用创建一个新的环境，并且JavaScript会将函数的`[[Environment]]`槽的值保存在环境对象的`[[OuterEnv]]`槽中。

初学者常常误以为闭包仅在任何函数返回嵌套函数时才会形成，但事实并非如此。

每次在JavaScript中创建函数时，它都会在创建该函数时形成对环境的闭包。形成闭包是指当函数被创建时，它保存了对创建时环境的引用。

这种误解的原因是什么？主要有以下两个原因：

+   许多在线资源通过包含返回嵌套函数的函数的代码示例来介绍闭包的概念。

+   只有当函数从与其定义不同的作用域中调用时，闭包才会显而易见。

大多数函数通常是在其定义的相同作用域中被调用的。这使得闭包不易察觉。只有当函数从与其定义不同的作用域中被调用时，闭包才会变得显而易见。

在下面的代码示例中，从全局作用域定义并调用了一个函数，因此由该函数形成的闭包不易察觉。

```js
1 let score = 150;
2 
3 function logScore() {
4   console.log(score);
5 }
6 
7 logScore();

```

你可以在这个`Replit`中看到上面的代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/closure-misconception-example1">`

与上面的代码示例不同，在下面的代码示例中，闭包是显而易见的，因为嵌套的`greet`函数在`createGreeting`函数完成后仍然可以访问其`greetMsg`参数。闭包之所以明显，是因为`greet`函数是从与其定义不同的作用域中调用的。`greet`函数在`createGreeting`函数的局部作用域中定义，但它是从全局作用域中调用的。

```js
 1 function createGreeting(greetMsg) {
 2  function greet(personName) {
 3    console.log(`${greetMsg}${personName}!`);
 4  }
 5 
 6  return greet;
 7 }
 8 
 9 const sayHello = createGreeting("Hello");
10 sayHello("Mike");

```

这里是上面代码的一个`Replit`：

`<ReplitEmbed src="https://replit.com/@newlineauthors/closure-misconception-example2">`

你期望从以下代码示例中得到什么输出？

```js
1 for (var i = 1; i <= 3; i++) {
2   setTimeout(() => {
3     console.log(i);
4   }, 1000);
5 }

```

你可能期望以下输出：

```js
1 1;
2 2;
3 3;

```

尽管上述输出看起来合理，但它并不是我们从上述代码示例中得到的输出。实际输出如下所示：

```js
1 4;
2 4;
3 4;

```

这里是上述代码示例在`Replit`中的输出：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/closures-in-loops-example1”>`

如果这个输出让你感到惊讶，那么这节课就是为你准备的。即使没有，你是否理解这个输出背后的原因？在这节课中，我们将探讨导致这个问题的原因，也称为“`循环中的闭包`”问题，以及我们如何解决它。

### 这个问题的原因是什么？

上述代码示例受到这个臭名昭著的“`循环中的闭包`”问题的影响，因为每个`setTimeout`的回调函数都对`同一`变量`i`形成了闭包。由于我们的示例中总共有三次循环迭代，`setTimeout`被调用三次，因此我们有三个回调函数，全部对`同一`变量`i`形成闭包。

每个`setTimeout`调用的回调函数在循环执行完成`后`被调用。循环最后一次迭代后，变量`i`的值是“`4`”，由于每个“`setTimeout`”的回调函数都对`同一`变量`i`形成了闭包，因此它们都看到`i`的值为“`4`”。这就是它们在控制台上都记录“`4`”的原因。

上述代码示例的作用域链接可以在下图中可视化：

![作用域链接](images/module_05----lesson_05.03----public----assets----closure-in-loop-problem.png)

作用域链接

重要的是要注意，函数对变量形成闭包，而不是对其值。对变量的闭包意味着每个函数记录它所闭包的变量的`最新`值；如果函数对值而不是变量形成闭包，它们将记录在形成闭包时值的快照。

在我们的示例中，如果闭包是围绕`i`的值而不是`i`变量，那么每个回调将记录在创建该回调时迭代中有效的`i`值。这意味着我们将得到预期的输出，即`1 2 3`而不是`4 4 4`。但从代码示例的输出中显而易见，闭包是围绕变量形成的。因此，每个`setTimeout`的回调函数都对变量`i`形成了闭包，当每个回调被执行时，它看到的是`i`的最新值。

### 如何解决这个问题？

现在我们理解了“`循环中的闭包`”问题是什么以及其原因，让我们讨论一下在`ES2015`之前是如何解决这个问题的。

#### 预`ES2015`解决方案

在引入`ES2015`（也称为`ES6`）之前，解决这个问题的一种方法是使用[`IIFE（立即调用函数表达式）`](https://developer.mozilla.org/en-US/docs/Glossary/IIFE)。以下代码示例展示了使用`IIFE`如何解决这个问题。

```js
 1 for (var i = 1; i <= 3; i++) {
 2  ((counter) => {
 3    setTimeout(() => {
 4      console.log(counter);
 5    }, 1000);
 6  })(i);
 7 }
 8 
 9 /* output
10 ---------
11 1
12 2
13 3
14 ---------
15 */

```

这是上述代码示例在Replit中的输出：

`<ReplitEmbed src="https://replit.com/@newlineauthors/closures-in-loops-example2">`

使用 IIFE 如何解决这个问题？

回想一下，问题是由于不同回调对*同一个*变量的闭包造成的。但通过使用 IIFE，我们可以在每次迭代中将 `i` 的值作为参数传递给 IIFE。这个参数（`counter`）随后在 `setTimeout` 函数的回调函数中使用。这解决了问题，因为 `counter` 参数被每个回调函数的闭包所封闭，并且在每次迭代中都会创建一个新的 IIFE，以及新的 `setTimeout` 回调函数。每个 IIFE 的新实例都会传递一个新的 `i` 值，即在第一次迭代中为“1”，第二次迭代中为“2”，依此类推。因此，现在，通过使用 IIFE，每个回调函数都有一个不同的 `counter` 变量的闭包。

下面的图片帮助可视化上述代码示例中的作用域链（为了简单起见，函数对象未在下面的图片中显示）：

![作用域链接](images/module_05----lesson_05.03----public----assets----closure-problem-pre-es6-solution.png)

`作用域链接`

尽管 `setTimeout` 函数的回调记录了 `counter` 变量，但它们仍然可以访问 `i` 变量。如果我们同时记录 `counter` 和 `i` 会怎样？输出会如何变化？

```js
 1 for (var i = 1; i <= 3; i++) {
 2  ((counter) => {
 3    setTimeout(() => {
 4      console.log(counter, i);
 5    }, 1000);
 6  })(i);
 7 }
 8 
 9 /* output
10 ---------
11 1 4
12 2 4
13 3 4
14 ---------
15 */

```

以上代码示例的输出可以在下面的 Replit 中查看：

`<ReplitEmbed src="https://replit.com/@newlineauthors/closures-in-loops-example3">`

每个回调都对*不同*实例的 `counter` 变量有一个闭包，但它们仍然共享来自全局作用域的*同一个*变量 `i`。结果，它们记录了 `i` 的最新值，即“4”。

#### `ES2015 解决方案`

ES2015 引入了块级作用域的变量和常量，分别使用 `let` 和 `const` 关键字。我们可以通过将原始代码示例中的 `var` 关键字替换为 `let` 关键字，简单地解决“循环中的闭包”问题。

```js
 1 for (let i = 1; i <= 3; i++) {
 2  setTimeout(() => {
 3    console.log(i);
 4  }, 1000);
 5 }
 6 
 7 /* output
 8 ---------
 9 1
10 2
11 3
12 ---------
13 */

```

这是上述代码示例在 Replit 中的输出：

`<ReplitEmbed src="https://replit.com/@newlineauthors/closures-in-loops-example4">`

使用 `let` 关键字解决了这个问题，因为与每个回调函数闭包于*同一个*变量 `i` 不同，`let` 是块级作用域，导致每次循环迭代都有一个*不同*的 `i` 变量副本。这是解决“循环中的闭包”问题的关键思路。每次迭代都有自己的*独立*副本的 `i` 变量，这意味着在每次迭代中创建的 `setTimeout` 回调闭包于那个特定迭代的 `i` 变量副本。

在我们的代码示例中，我们有三次循环迭代和 `i` 变量的独立副本，每个副本仅限于特定的循环迭代。尽管看似我们只有一个 `i` 变量，但在幕后，每次迭代都有自己的 `i` 变量副本。

为了理解每次迭代如何获得自己的 `i` 变量副本，以下步骤解释了上述代码是如何执行的：

1.  在 `for` 循环开始执行之前，会创建一个环境对象（我们称之为 `initEnv`），它包含 `for` 循环初始化部分声明的变量。在我们的案例中，我们只有一个变量 `i`，因此 `initEnv` 环境对象包含变量 `i` 的副本。这个环境对象通过在 `[[OuterEnv]]` 内部插槽中保存对外部环境的引用，与外部环境链接。在这种情况下，外部环境是全局环境。

1.  为了开始 `for` 循环的第一次迭代，会创建一个新的环境对象（我们称之为 `iter1Env`）。这个环境对象也将全局环境作为其外部环境。变量 `i` 被从 `initEnv` 对象（在步骤 1 中创建）中复制到这个新创建的 `iter1Env` 对象。

1.  循环条件 `i <= 3` 为 `true`，因此循环体在循环的第一次迭代中被执行。`setTimeout` 的回调函数被创建，并将第一次循环迭代的环境对象 `iter1Env`（在步骤 2 中创建）保存在回调函数的内部 `[[Environment]]` 插槽中。之后，回调函数作为参数传递给 `setTimeout` 函数以便稍后执行。

    第一轮迭代已完成。以下图像显示了迄今为止创建的不同环境之间的链接：

    ![`循环中的闭包` - 第一次迭代](images/module_05----lesson_05.03----public----assets----closure-loop-iter-1.png)

    `循环中的闭包` - 第一次迭代

1.  现在，为了开始第二次迭代，创建了一个新的环境对象（我们称之为`iter2Env`）。变量`i`是从`initEnv`环境对象（在第1步中创建）复制过来的，但在`iter2Env`中的`i`的值是`iter1Env`中的`i`的值（在第2步中创建）。由于`for`循环的增量部分（`i++`），`iter2Env`中的`i`的值随后被增加。

1.  与前一次迭代一样，创建了一个新的回调函数，并将对`iter2Env`的引用保存在其`[[Environment]]`内部槽中。然后，将回调函数作为参数传递给`setTimeout`函数。

1.  此过程在循环的第三次也是最后一次迭代中重复进行。

下图显示了在循环的三次迭代后，不同环境是如何连接在一起的：

![`closue` 在循环中 - 所有迭代](images/module_05----lesson_05.03----public----assets----closure-loop-iter.png)

`closue` 在循环中 - 所有迭代

希望最终的图解可以澄清为什么使用`let`关键字解决了“循环中的闭包”问题。由于为循环的每次迭代创建的每个环境对象都有其`单独的`变量`i`的副本，因此在循环的不同迭代中创建的每个回调的闭包对变量`i`的单独副本形成了闭包。因此，它们记录了它们闭合的值，给出了我们预期的输出，即`1 2 3`。

随着JavaScript语言的最新增加，现在可以在JavaScript中拥有[私有字段和方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Private_class_fields)。然而，在这些更改引入之前，闭包是隐藏公共访问数据的首选选项。在面向对象编程术语中，这被称为“数据隐藏”和“封装”。

以下是如何使用闭包拥有私有变量和方法的示例：

```js
 1 const bank = (function () {
 2  // private data
 3  const accounts = [];
 4 
 5  // private function
 6  function getInternalBankLogs() {
 7    // ...
 8  }
 9 
10   /***  public functions ***/
11 
12   function openAccount(data) {
13     // some logic...
14     // ...
15     accounts.push(newAccount);
16   }
17 
18   function deposit(accountNum, amount) {
19     // ...
20   }
21 
22   function withdraw(accoutNum, amount) {
23     // ...
24   }
25 
26   return {
27     openAccount,
28     deposit,
29     withdraw
30   };
31 })();
32 
33 bank.openAccount({}); // ok
34 bank.accounts(); // error, not accessible

```

`IIFE`内部的代码被执行，并从`IIFE`中返回一个对象，该对象被赋值给`bank`变量。返回的对象只包含需要从外部访问的数据，而不返回旨在私有的代码；因此，这些数据保持私有，限制在`IIFE`的边界墙内。然而，得益于闭包，从`IIFE`返回的公共暴露数据仍然可以访问`IIFE`内部的私有数据。

##### 进一步阅读

+   [使用闭包模拟私有方法 - (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures#emulating_private_methods_with_closures)
