## `‘this’`关键字

`this`关键字是JavaScript语言中最令人困惑的概念之一。混淆的原因在于`this`关键字的值在不同上下文中以不同方式设置。

在本模块中，我们将尝试揭开`this`关键字的神秘面纱。我们将理解`this`值设置的不同方式。`this`关键字可以在不同的上下文中使用：函数内部、全局作用域、模块内部等。我们将探索不同的上下文以及`this`在这些上下文中是如何设置的。

### 函数上下文

`this`关键字主要用于函数内部，指代调用该函数的对象。换句话说，当一个函数作为“方法”（使用对象调用）被调用时，`this`关键字适用于引用用于调用该函数的对象。

`this`关键字就像是一个隐式参数，传递给函数。就像显式函数参数一样，隐式参数`this`的值在函数被`调用`时设置。这是一个重要的观点。函数内部的`this`值取决于该函数是`如何`被`调用`的。

考虑以下代码示例：

```js
 1 const student = {
 2  id: 123,
 3  name: "John Doe",
 4  email: "john@email.com",
 5  printInfo: function () {
 6    console.log(`${this.id} - ${this.name} - ${this.email}`);
 7  }
 8 };
 9 
10 student.printInfo();
11 // 123 - John Doe - john@email.com

```

这里是上面代码的`Replit`：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/what-is-this-example1”>`

上述代码示例中的`printInfo`函数使用了`this`关键字，查看代码，我们可以知道`printInfo`函数假定`this`在函数内部的值将是一个具有三个属性的对象：`id`、`name`和`email`。但如前所述，函数内部的`this`值取决于函数是`如何`被调用的。

在上述代码示例中，`printInfo`函数使用`student`对象调用，当函数使用对象调用时，该函数内部的`this`指向用于调用该函数的对象。因此在我们的代码示例中，`printInfo`中的`this`指向`student`对象。由于`student`对象具有通过`this`关键字在`printInfo`函数内部访问的三个属性，它们的值被记录到控制台。

如果函数没有作为“方法”调用，`this`将指向什么？考虑以下代码示例：

```js
1 function orderFood() {
2   console.log("Order confirmed against the name: " + this.fullName);
3 }
4 
5 orderFood();
6 // Order confirmed against the name: undefined

```

这里是上面代码的`Replit`：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/what-is-this-example2”>`

`orderFood`函数内部的`this`指向什么？

上面问题的答案取决于我们的代码是否在[`严格模式`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)下执行。如果是非严格模式，当函数未作为方法调用时，函数内部的`this`指向全局对象，而在浏览器中，全局对象是`window`对象。然而，在严格模式下，当函数未作为方法调用时，函数内部的`this`值为`undefined`。

你能从上面代码的输出中猜出代码是以哪种模式执行的吗？因为`this.fullName`的值为`undefined`，所以代码是在非严格模式下执行的。

如果我们在严格模式下执行上面的代码：

```js
1 "use strict";
2 
3 function orderFood() {
4   console.log("Order confirmed against the name: " + this.fullName);
5 }
6 
7 orderFood();
8 // Uncaught TypeError: this is undefined

```

这里是上面代码的`Replit`：

`<ReplitEmbed src="https://replit.com/@newlineauthors/what-is-this-example3">`

有错误吗？为什么？

回想一下在严格模式下“函数”内`this`的值是什么。它是`undefined`。因此，`this.fullName`抛出一个错误，因为我们无法访问`undefined`值上的任何属性。

### 全局上下文

在全局作用域中，`this`的值取决于我们JavaScript代码执行的环境。

JavaScript代码可以在不同的环境中执行，例如浏览器、`NodeJS`等。在全局作用域中，`this`的值在不同的环境中是不同的。在浏览器的情况下，全局作用域中的`this`值是`window`对象。

在`NodeJS`中，`this`的值取决于我们使用的是`ECMAScript`模块还是`CommonJS`模块。在`ECMAScript`模块中，模块顶层的`this`值为`undefined`。这是因为`ECMAScript`模块中的代码在严格模式下执行。在`CommonJS`模块中，在模块的顶层，`this`引用的是`module.exports`对象。

:::info

在`Node.js`中，JavaScript代码在技术上并不是在全局作用域中执行的。相反，它是在模块作用域中执行的，常用的模块有`CommonJS`和`ECMAScript`模块。

:::

在`[web workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API)`中，`this`的值在顶层引用的是web worker的全局作用域，这与浏览器中包含`window`对象的全局作用域不同。代码在web worker内部在其自己的独立上下文中执行，并具有自己的全局作用域。

### 构造函数上下文

当一个函数被用`new`关键字作为构造函数调用时，构造函数内部的`this`关键字引用的是新创建的对象。`new`关键字创建一个新对象并将其作为`this`的值。因此，我们可以在构造函数内部使用`this`来向新创建的对象添加属性。

```js
1 function Recipe(name, ingredients) {
2   this.name = name;
3   this.ingredients = ingredients;
4 }

```

上面的函数在作为构造函数调用时，将向新创建的对象添加两个属性：`name`和`ingredients`。

### 类上下文

JavaScript中类内部的代码在严格模式下执行。因此，方法内部的`this`值如果没有在对象上调用则为`undefined`，否则为用于调用方法的类实例本身。

```js
 1 class Shape {
 2  constructor(color) {
 3    this.color = color;
 4  }
 5 
 6  printColor() {
 7    console.log(this.color);
 8  }
 9 }
10 
11 const circle = new Shape("Red");
12 const printColorFn = circle.printColor;
13 printColorFn();
14 // Error: this is undefined

```

这里是上面代码的`Replit`：

`<ReplitEmbed src="https://replit.com/@newlineauthors/what-is-this-example5">`

上面的代码示例抛出一个错误，因为我们将`printColor`方法作为“函数”调用。如前所述，类内部的代码在严格模式下执行，因此，在严格模式下的函数中，`this`在方法内部是`undefined`。

### DOM事件处理程序上下文

我们已经知道，在函数内部`this`的值取决于函数的调用方式。那么，对于我们没有调用的回调函数呢？比如DOM事件处理程序，这些函数并不是由我们调用，而是每当触发点击事件时由JavaScript为我们调用。在这种情况下，`this`的值是什么？

事件监听器回调被调用时，`this`被设置为触发事件的HTML元素。考虑以下代码示例：

```js
 1 <button>Submit</button>
 2 
 3 <script>
 4  const btn = document.querySelector("button");
 5 
 6  class FormHandler {
 7    constructor(submitBtn) {
 8      submitBtn.addEventListener("click", this.submitForm);
 9    }
10 
11     submitForm() {
12       console.log("form submitted");
13       console.log(this);
14     }
15   }
16 
17   new FormHandler(btn);
18 </script>

```

这里是上面代码的Replit：

`<ReplitEmbed src="https://replit.com/@newlineauthors/what-is-this-example6">`

在浏览器中运行上述代码，并检查浏览器开发者工具中的控制台。特别注意`submitForm`方法记录的`this`的值。当它作为事件监听器回调被调用时，这个方法内部的`this`值是按钮元素，而不是我们通常预期的类的实例。

如果我们在事件监听器回调函数内部使用`this`时不小心，这可能会导致问题。想象一下我们需要在`FormHandler`类中调用另一个方法的场景：

```js
 1 <button>Submit</button>
 2 
 3 <script>
 4  const btn = document.querySelector("button");
 5 
 6  class FormHandler {
 7    constructor(submitBtn) {
 8      submitBtn.addEventListener("click", this.submitForm);
 9    }
10 
11     submitForm() {
12       this.sendRequest();
13       // ERROR: this.sendRequest is not a function
14     }
15 
16     sendRequest() {
17       console.log("sending request...");
18     }
19   }
20 
21   new FormHandler(btn);
22 </script>

```

从`submitForm`方法内部调用`sendRequest`方法会抛出一个错误，因为如前所述，在事件处理函数`submitForm`中，`this`是触发事件的HTML元素。因此，与我们预期的不同，`this.sendRequest`会抛出错误。如果在`submitForm`方法内部的`this`是`FormHandler`类的实例，这种情况就不会发生。那么，我们该如何从`submitForm`方法调用`sendRequest`方法呢？有多种方法可以实现这一点，但我们将在本模块的后续课程中讨论。

在深入探讨`this`在箭头函数中的工作原理之前，我们首先要探讨使用`this`关键字在常规函数中存在的问题。考虑以下代码示例：

```js
 1 function Counter(startingValue) {
 2  this.value = startingValue;
 3 }
 4 
 5 Counter.prototype.incrementFactory = function (incrementStep) {
 6  return function () {
 7    this.value += incrementStep;
 8    console.log(this.value);
 9  };
10 };
11 
12 const counter = new Counter(0);
13 const increment5 = counter.incrementFactory(5);
14 increment5(); // NaN
15 increment5(); // NaN
16 increment5(); // NaN

```

你可以在下面的Replit中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/arrow-functions-and-this-example1" />`

为什么我们得到`NaN`作为输出？产生意外输出的原因是`incrementFactory`函数返回的函数内部的`this`值不正确。

回想一下，`this`的值是如何在函数内部设置的。这取决于函数是`如何`被调用的。在上面的代码示例中，`increment5`函数是如何被调用的？它是作为“方法”还是独立函数被调用的？它是作为“函数”被调用的，因此，`this`的值取决于我们的代码是否处于严格模式下。假设我们的代码处于非严格模式，`increment5`函数内部的`this`值是全局对象，即在浏览器中是`window`对象。因此，`this.value`实际上是`window.value`，并且它是`undefined`，因为`window`对象默认没有`value`属性。因此，当`undefined`与一个数字相加时，我们得到`NaN`值，即`incrementStep`参数的值。

我们如何解决这个问题？如何确保`increment5`函数内部的`this`值是我们想要的？处理这个问题有多种方法。一种方法是在返回函数之前在`incrementFactory`函数内部保存`this`的值，然后在返回的函数中，使用包含`this`值的变量，而不是直接使用`this`。以下代码示例展示了这种方法的实际应用：

```js
 1 function Counter(startingValue) {
 2  this.value = startingValue;
 3 }
 4 
 5 Counter.prototype.incrementFactory = function (incrementStep) {
 6  const thisVal = this; // save `this` value
 7  return function () {
 8    // use `thisVar` variable instead of `this`
 9    thisVal.value += incrementStep;
10     console.log(thisVal.value);
11   };
12 };
13 
14 const counter = new Counter(0);
15 const increment5 = counter.incrementFactory(5);
16 increment5(); // 5
17 increment5(); // 10
18 increment5(); // 15

```

你可以在下面的Replit中运行上述代码：

<ReplitEmbed src="https://replit.com/@newlineauthors/arrow-functions-and-this-example2" />

上述方法常用于修复类似的问题，其中需要来自周围上下文的`this`值，而不是当前函数内部实际使用的`this`值。在上面的代码示例中，我们需要来自`incrementFactory`函数的周围上下文的`this`值，而不是`increment5`函数内部的`this`值。

### 箭头函数来拯救我们

另一种解决上述问题的方法是使用箭头函数。让我们将上面的代码示例更改为使用箭头函数：

```js
 1 function Counter(startingValue) {
 2  this.value = startingValue;
 3 }
 4 
 5 Counter.prototype.incrementFactory = function (incrementStep) {
 6  // use an arrow function
 7  return () => {
 8    this.value += incrementStep;
 9    console.log(this.value);
10   };
11 };
12 
13 const counter = new Counter(0);
14 const increment5 = counter.incrementFactory(5);
15 increment5(); // 5
16 increment5(); // 10
17 increment5(); // 15

```

你可以在下面的Replit中运行上述代码：

<ReplitEmbed src="https://replit.com/@newlineauthors/arrow-functions-and-this-example3" />

使用箭头函数解决了这个问题，因为与常规函数不同，常规函数在被调用时会获得自己的`this`值，而箭头函数不会获得自己的`this`值；相反，箭头函数内部的`this`值是从周围上下文中获取的。

周围上下文是定义箭头函数的环境。在我们的代码示例中，箭头函数是在使用`counter`对象调用`incrementFactory`函数时创建的。因此，`incrementFactory`函数内部的`this`指向`counter`对象，这就是返回自`incrementFactory`函数的箭头函数的周围上下文。结果，箭头函数内部的`this`值在调用时也是`counter`对象，这正是我们想要`increment5`函数内部的`this`值，使我们的代码示例能够正常工作。

让我们回顾一下我们在上节课讨论的例子：

```js
 1 <button>Submit</button>
 2 
 3 <script>
 4  const btn = document.querySelector("button");
 5 
 6  class FormHandler {
 7    constructor(submitBtn) {
 8      submitBtn.addEventListener("click", this.submitForm);
 9    }
10 
11     submitForm() {
12       this.sendRequest();
13       // ERROR: this.sendRequest is not a function
14     }
15 
16     sendRequest() {
17       console.log("sending request...");
18     }
19   }
20 
21   new FormHandler(btn);
22 </script>

```

在上面的代码示例中点击`submit`按钮会抛出一个错误，因为`submitForm`方法内部的`this`值是按钮元素，而不是`FormHandler`类的实例。因此，`this.sendRequest()`调用会抛出错误，因为`this`需要指向`FormHandler`类的实例，以便允许我们从`submitForm`方法中调用该类的其他方法。那么问题是，我们如何从`submitForm`方法调用`sendRequest`方法？我们在上节课中说过，解决这个问题的方法不止一种。其中一种是使用箭头函数。

为了解决这个问题，在`FormHandler`类的构造函数内部，我们可以传递一个`箭头函数`作为回调函数，而不是``this.submitForm``，来处理点击事件。在`箭头函数`内部，我们可以调用`submitForm`方法来处理点击事件。

```js
1 class FormHandler {
2   constructor(submitBtn) {
3     submitBtn.addEventListener("click", () => this.submitForm());
4   }
5 
6   // methods...
7 }

```

为什么将`箭头函数`作为回调传递解决了问题？我们仍然在`箭头函数`内部调用`submitForm`方法，那么这与直接传递``this.submitForm``作为回调函数有什么不同呢？

`箭头函数`解决问题的原因在于，如前所述，`箭头函数`没有自己的``this``值；它们从周围环境中获取值。在这种情况下，周围环境是构造函数。构造函数内部``this``的值是什么？当使用`new`关键字调用构造函数时，它的值是`FormHandler`类的一个实例。因此，``this``在事件处理程序回调函数中指向一个`HTML`元素，而在`箭头函数`内部的值则与构造函数相同，即`FormHandler`类的一个实例。因此，当我们在`箭头函数`内部调用`submitForm`方法时，`submitForm`方法内部的``this``值也是`FormHandler`类的一个实例。结果，我们可以从`submitForm`方法内部调用任何其他方法。

在这个旧版本的代码中，抛出错误的事件处理程序是``this.submitForm``方法。它并不是由我们的代码显式调用的，而是每当点击提交按钮时由`JavaScript`调用。我们知道，函数内部``this``的值取决于函数的调用方式。在这种情况下，由于我们没有显式调用该函数，因此无法控制``this``在`submitForm`方法中的值。使用`箭头函数`使我们能够显式调用`submitForm`方法，从而控制其内部的``this``值。

`箭头函数`确实非常有用，是`JavaScript`语言的一个受欢迎的补充。它们解决的问题也可以通过其他方式解决，但其他解决方案比`箭头函数`更冗长。

到目前为止，我们讨论了``this``的值要么取决于`JavaScript`代码执行的环境，要么在函数的情况下取决于函数的调用方式。我们还讨论了`箭头函数`没有自己的``this``值；相反，它们从周围的上下文中获取值。

到目前为止，我们看到的所有设置``this``值的方法都是自动设置其值的。`JavaScript`还提供了显式将``this``设置为我们想要的值的方法。

我们可以使用以下三种内置方法中的任何一种显式设置``this``的值：

+   [`Function.prototype.call()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call)

+   [`Function.prototype.apply()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)

+   [`Function.prototype.bind()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)

我们不会详细介绍这些方法如何工作；你可以通过上面提供的链接学习每个方法的工作原理。然而，我们将看到显式设置`this`如何是有用的。

让我们重温上一个课程中关于箭头函数的代码示例：

```js
 1 function Counter(startingValue) {
 2  this.value = startingValue;
 3 }
 4 
 5 Counter.prototype.incrementFactory = function (incrementStep) {
 6  return function () {
 7    this.value += incrementStep;
 8    console.log(this.value);
 9  };
10 };
11 
12 const counter = new Counter(0);
13 const increment5 = counter.incrementFactory(5);
14 increment5(); // NaN
15 increment5(); // NaN
16 increment5(); // NaN

```

你可以在下面的`Replit`中运行上述代码：

<ReplitEmbed src="https://replit.com/@newlineauthors/binding-this-example1" />

在上一个课程中，我们看到使用箭头函数修复了上述代码示例。我们也可以通过显式地将`this`的值设置为所需的值，即`counter`对象来修复这段代码，它用于调用`incrementFactory`函数。我们可以使用`bind`方法来设置`this`的值，而不是使用箭头函数。

```js
 1 function Counter(startingValue) {
 2  this.value = startingValue;
 3 }
 4 
 5 Counter.prototype.incrementFactory = function (incrementStep) {
 6  const incrementFn = function () {
 7    this.value += incrementStep;
 8    console.log(this.value);
 9  };
10 
11   // return a function with `this` bound
12   // to the object used to invoke the
13   // `incrementFactory` method
14   return incrementFn.bind(this);
15 };
16 
17 const counter = new Counter(0);
18 const increment5 = counter.incrementFactory(5);
19 increment5(); // 5
20 increment5(); // 10
21 increment5(); // 15

```

你可以在下面的`Replit`中运行上述代码：

<ReplitEmbed src=”https://replit.com/@newlineauthors/binding-this-example2” />

### 借用方法

想象一下有一个对象，它包含对其他对象也有用的方法。我们如何能将这些方法与其他对象一起使用呢？一种选择是为每个需要这些方法的对象复制方法的定义。但我们不想要重复。有办法避免重复并重用现有的方法吗？

```js
 1 const john = {
 2  name: "John",
 3  sayHello() {
 4    console.log("Hello, I am " + this.name);
 5  }
 6 };
 7 
 8 const sarah = {
 9  name: "Sarah"
10 };
11 
12 // borrow method from john
13 const sayHello = john.sayHello;
14 sayHello.call(sarah);
15 // Hello, I am Sarah

```

你可以在下面的`Replit`中运行上述代码：

<ReplitEmbed src=”https://replit.com/@newlineauthors/binding-this-example3” />

我们可以在函数内部显式设置`this`的值，并使用上述提到的三种方法中的任何一种与其他对象一起使用。这使我们能够避免重复并重用代码。

在这一点上，你可能会问：*我们是否可以创建一个构造函数，使我们能够创建对象并在构造函数的原型属性中添加公共方法？*你说得对。创建一个构造函数是处理我们想要创建相似对象的正确方法。然而，显式地设置`this`的值使我们能够在无关对象之间重用代码。这是一个很好的选择，可以在合适的地方使用。

### `Chain`构造函数调用

在JavaScript引入类之前，继承另一个构造函数的传统方法是显式地设置原型链，并重用被继承的构造函数，将公共属性添加到新创建的对象。以下代码示例展示了我们如何将责任委托给现有构造函数，以将一些属性添加到新创建的对象：

```js
 1 function Employee(name, age, id) {
 2  this.name = name;
 3  this.age = age;
 4  this.id = id;
 5 }
 6 
 7 function BankEmployee(name, age, id, bankName) {
 8  // delegate the responsibility of adding
 9  // "name", "age", and "id" properties to
10   // the Person constructor
11   Employee.call(this, name, age, id);
12   this.bankName = bankName;
13 }

```

在上面的代码示例中，`call`方法被用来调用`Employee`构造函数，传入`Employee`构造函数可以在新创建的对象上设置的三个属性。但我们如何告诉`Employee`构造函数将属性添加到新创建的`BankEmployee`对象上呢？这就是传递给`call`方法的第一个参数的作用。我们将`this`作为第一个参数传递。回想一下，在函数内部`this`的值是如何设置的：它取决于函数是如何调用的。在这种情况下，我们希望`BankEmployee`函数作为构造函数使用`new`关键字来调用。因此，`BankEmployee`函数内部的`this`将是新创建的对象。这个新创建的对象在`Employee`构造函数内部显式设置为`this`的值。

换句话说，`Employee`构造函数是从`BankEmployee`构造函数内部调用的，`this`显式设置为新创建的`BankEmployee`对象。因此，添加到`Employee`构造函数内部的`this`的属性将实际添加到新创建的`BankEmployee`对象。这就是我们如何使用现有构造函数并减少代码重复。

### 重新审视`“this”`问题

让我们重新审视我们在第一课中讨论的例子。

```js
 1 <button>Submit</button>
 2 
 3 <script>
 4  const btn = document.querySelector("button");
 5 
 6  class FormHandler {
 7    constructor(submitBtn) {
 8      submitBtn.addEventListener("click", this.submitForm);
 9    }
10 
11     submitForm() {
12       this.sendRequest();
13       // ERROR: this.sendRequest is not a function
14     }
15 
16     sendRequest() {
17       console.log("sending request...");
18     }
19   }
20 
21   new FormHandler(btn);
22 </script>

```

我们要解决的问题是希望从事件处理程序回调内部调用同一类的其他方法，但尝试这样做会抛出错误，因为事件处理程序内部的`this`是触发DOM事件的HTML元素。在前一课中，我们看到箭头函数如何解决这个问题。还有另一种方法来修复这个问题，那就是在`submitForm`方法内部显式设置`this`的值。

```js
1 class FormHandler {
2   constructor(submitBtn) {
3     submitBtn.addEventListener("click", this.submitForm.bind(this));
4   }
5 
6   // methods...
7 }

```

在`submitForm`方法中显式设置`this`的值，使用`bind`方法解决了问题，因为它覆盖了事件回调函数内`this`的默认值。我们已经将其显式设置为`FormHandler`类构造函数内部的`this`的值，即`FormHandler`类的一个实例。

将 `this.submitForm` 和 `this.submitForm.bind(this)` 传递给 `addEventListener` 方法的区别在于，使用 `this.submitForm` 时，`submitForm` 方法内部的 `this` 的值取决于 `submitForm` 方法的调用方式。在这种情况下，我们知道其内部的 `this` 值将是 HTML 按钮元素，这并不是我们想要的。另一方面，传递 `this.submitForm.bind(this)` 解决了这个问题，因为与之前不同，`submitForm` 方法内部的 `this` 的值明确绑定为 `FormHandler` 类的实例。

``globalThis`` 是 JavaScript 中一个全局可用的属性，使我们能够访问全局对象，而不论我们的 JavaScript 代码在哪个环境中执行。它为我们提供了一种在不同 JavaScript 环境中访问全局对象的标准方式。

如我们所知，JavaScript 可以在不同的环境中执行，例如浏览器、``Node.js`` 运行时等。每个环境都有一个不同的全局对象可供在该环境中执行的 JavaScript 代码使用。在 ``globalThis`` 出现之前，访问全局对象没有一种跨环境的标准方式。这使得我们的代码可移植性降低。

``globalThis`` 属性使得访问全局对象成为可能，无需担心环境。如果我们知道我们的代码可以在不同的环境中执行，那么在现代 JavaScript 代码中，使用 ``globalThis`` 来访问全局对象是最佳选择。

想象一个场景，你想检查全局对象是否包含某个属性，而不论你的代码是在浏览器还是在 ``NodeJS`` 环境中执行。没有标准的方式来访问全局对象，你可能会写出以下代码：

```js
1 if (typeof window !== "undefined" && window.secretProperty) {
2   // execute code for browser
3 } else if (typeof global !== "undefined" && global.secretProperty) {
4   // execute code for nodejs
5 }

```

使用 ``globalThis``，我们可以简化上述代码，如下所示：

```js
1 if (globalThis.secretProperty) {
2   // execute code
3 }

```

尽管这个属性在现代浏览器中得到了[良好的支持](https://caniuse.com/?search=globalThis)，但旧版本的浏览器不支持。因此，在使用这个属性时，可能需要考虑浏览器的支持情况。

### ``this`` vs ``globalThis``

``globalThis`` 不应与 ``this`` 关键字混淆。我们在本模块中讨论了 ``this`` 的值如何因不同的执行上下文而变化，但 ``globalThis`` 只是访问不同 JavaScript 环境中的全局对象的标准方式。它的值仅因我们的代码执行的环境而异，而不受函数调用方式或代码是否处于严格模式的影响。

在 ``ECMAScript`` 模块中，代码是在严格模式下执行的。因此，模块作用域中的 ``this`` 的值是 ``undefined``，但 ``globalThis`` 的值是执行环境的全局对象；在 ``NodeJS`` 中，它是 ``global`` 对象，而在浏览器中，它是 ``window`` 对象。

本模块主要讨论``this``关键字；我们讨论了在不同上下文中如何设置其值的不同方式；我们还讨论了由于``this``的意外值可能出现的问题，并探索了修复这些问题的不同选项。

由于``this``在不同上下文中可以有不同的值，让我们总结一下``this``在不同上下文中的值：

+   在箭头函数的情况下，``this``的值是从周围的上下文中获取的。

+   在常规函数的情况下，``this``的值取决于*如何*调用函数，以及代码是否在严格模式下执行。

    +   如果一个函数作为构造函数被调用，并使用``new``关键字，那么``this``的值就是新创建的对象。

    +   如果``this``的值通过``bind``、``call``或``apply``函数显式设置，那么``this``的值就是传递给这些函数的第一个参数的值。

    +   如果一个函数被作为“方法”调用，那么``this``的值就是调用该方法的对象。

    +   如果函数在没有任何对象的情况下被调用，即作为一个“函数”，则在非严格模式下，`this`的值是全局对象，而在严格模式下是`undefined`。

+   在DOM事件处理回调中，`this`的值是触发事件的HTML元素。

+   在浏览器的全局作用域中，`this`指的是全局`window`对象。

+   在NodeJS中，顶层代码在模块作用域中执行。在ECMAScript模块中，模块顶层的`this`是`undefined`，因为ECMAScript模块中的代码隐式在严格模式下执行。在CommonJS模块中，模块顶层的`this`指的是`module.exports`对象。

希望这个模块能让你更好地理解`this`关键字，并帮助你理解在不同上下文中`this`的值是如何设置的。这个模块还旨在帮助你理解意外的`this`值可能在我们的代码中造成的各种问题，以及我们有哪些不同的选项可以解决这些问题。
