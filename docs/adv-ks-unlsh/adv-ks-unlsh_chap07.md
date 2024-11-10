## `Symbol`

`symbol`是一种可以使用名为`Symbol`的函数创建的原始值。这种原始值有趣之处在于，它保证是唯一的。这种唯一性的保证是`symbols`的卖点。

随着`ES2015`中引入`symbols`，JavaScript发生了两个变化：

+   语言中引入了一种新类型的值。

+   只有字符串可以作为属性键添加到对象中。现在，`symbols`也可以作为键。

在我们讨论如何在代码中使用symbols之前，让我们先理解将symbols添加到JavaScript语言的动机。

`Symbols`最初是作为一种机制，用于向对象添加私有属性，原本被称为“私有名称对象”。但后来，它们的名称被改为`symbols`，并成为了一种原始值。

事实证明，每个`symbol`都是唯一值，这一点非常有用，因为它允许JavaScript语言进行扩展，并保持向后兼容性。`Symbols`允许JavaScript向对象添加新的属性，这些属性不会与其他人代码中可能使用的现有属性冲突。

`TC39`的主要目标之一是保持JavaScript的向后兼容性。考虑到这一目标，任何添加到语言的新特性都不能破坏现有代码。`Symbols`帮助保持向后兼容性的承诺。

JavaScript语言中的某些特性需要在对象上查找属性。这样的特性可以选择什么属性键？选择任何字符串属性名称是不可能的，因为可能有人在其代码中使用了该属性，使用该属性作为新特性可能会破坏他们的代码。

例如，在将对象转换为原始值时，类型转换算法会在对象上查找一个名为`[Symbol.toPrimitive](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol/toPrimitive)`的特殊属性。如果存在这样的属性，并且它的值是一个函数，则其返回值将作为对象的原始表示。否则，将使用调用`toString`和`valueOf`方法的默认机制，以不同的顺序，如在先前关于强制转换的模块中所解释的。

想想如何能通过字符串属性将这样的特性添加到语言中。可能会选择什么名称以保证不会破坏现有代码？

这正是symbols的优势所在。将symbols用作属性可以通过向对象添加独特的属性来实现这样的特性，这些属性不可能破坏现有代码，因为：

+   `symbols`在`ES2015`之前是不存在的，且

+   每个`symbol`都是唯一值

符号值可以使用`Symbol`函数创建。重要的是要注意，`Symbol`函数必须在没有`new`关键字的情况下调用。尝试使用`new`关键字调用`Symbol`函数会导致错误。这是因为它阻止了在符号周围创建对象包装器。每次调用`Symbol`函数必须创建一个新的唯一符号值。

```js
1 const sym = Symbol();

```

一旦创建了符号，可以使用方括号表示法将其作为属性添加到现有对象中：

```js
1 const sym = Symbol();
2 
3 const obj = {};
4 obj[sym] = "hello";
5 
6 console.log(obj[sym]); // hello

```

你可以在下面的`Replit`中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/creating-symbols-example2" />`

或者，可以使用计算属性表示法将符号作为属性添加到对象中：

```js
1 const sym = Symbol();
2 
3 const obj = {
4   [sym]: "hello"
5 };
6 
7 console.log(obj[sym]); // hello

```

你可以在下面的`Replit`中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/creating-symbols-example3" />`

### 符号与隐私

对象上的常规`string`属性可以通过多种方式访问。例如，考虑以下代码示例：

```js
1 const name = "name";
2 
3 const person = {
4   [name]: "John Doe"
5 };
6 
7 console.log(person.name); // John Doe
8 console.log(person["name"]); // John Doe
9 console.log(person[name]); // John Doe

```

你可以在下面的`Replit`中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/creating-symbols-example4" />`

在此示例中，属性键`name`通过计算属性名称添加到`person`对象中。可以通过多种方式访问此属性，如上面的代码示例所示。但是，如果将`name`变量的值从`string`更改为符号，会发生什么？

```js
1 const name = Symbol();
2 
3 const person = {
4   [name]: "John Doe"
5 };
6 
7 console.log(person.name); // undefined
8 console.log(person["name"]); // undefined
9 console.log(person[name]); // John Doe

```

你可以在下面的`Replit`中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/creating-symbols-example5" />`

将会注意到`person.name`和`person["name"]`输出`undefined`，但是最后的`console.log`语句按预期记录了名称。那么，前两个语句和最后一个语句有什么区别呢？前两个语句记录`undefined`，因为在获得原始符号之前无法访问符号属性。只有上面代码示例中的最后一个`console.log`语句使用了原始符号，这就是它记录名称而不是`undefined`的原因。

所以，如果原始符号不可访问，这是否意味着符号属性是私有属性？如果迭代对象的属性会发生什么？让我们来看看对象的符号属性是否可以获取。

```js
 1 const name = Symbol();
 2 
 3 const person = {
 4  [name]: "John Doe",
 5  age: 20
 6 };
 7 
 8 // only sees the "age" property
 9 for (const prop in person) {
10   console.log(prop);
11 }
12 
13 console.log(Object.keys(person)); // ["age"]
14 
15 console.log(Object.getOwnPropertyNames(person)); // ["age"]

```

你可以在下面的`Replit`中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/creating-symbols-example6" />`

查看上述代码示例的输出，可能会假设符号属性确实是私有的。然而，这种假设是错误的。正如下一个代码示例所示，符号属性并不是私有的。

```js
 1 const name = Symbol();
 2 
 3 const person = {
 4  [name]: "John Doe",
 5  age: 20
 6 };
 7 
 8 console.log(Object.getOwnPropertyDescriptors(person));
 9 
10 console.log(Object.getOwnPropertySymbols(person));

```

你可以在下面的`Replit`中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/creating-symbols-example7" />`

上面的代码示例显示，可以使用`Object.getOwnPropertyDescriptors`或`Object.getOwnPropertySymbols`等方法发现符号属性。虽然与`string`属性相比，符号属性的访问可能稍显不便，但它们并不是私有的。JavaScript有真正的`[private properties](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Private_class_fields)`，符号并不打算用作私有属性。

### 向符号添加描述

在创建符号时，可以为每个符号提供描述。这一描述对于调试目的可能很有用。以下代码示例创建了一个带描述的符号：

```js
1 const propSymbol = Symbol("property symbol");

```

描述作为参数传递给`Symbol`函数。然后可以使用名为`description`的属性访问提供的描述。

```js
1 const propSymbol = Symbol("property symbol");
2 
3 console.log(propSymbol.description);
4 // property symbol

```

您可以在下面的`Replit`中运行上述代码：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/creating-symbols-example9” />`

`description`属性只能用于获取符号的属性；不能用于设置描述。以下代码示例显示，将值分配给符号的`description`属性并不会改变其值。`description`属性实际上是一个getter，而此属性没有定义setter。因此，描述只能通过此属性获取，而不能设置。

```js
1 const propSymbol = Symbol("property symbol");
2 
3 console.log(propSymbol.description);
4 // property symbol
5 
6 propSymbol.description = "123";
7 
8 console.log(propSymbol.description);
9 // property symbol

```

您可以在下面的`Replit`中运行上述代码：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/creating-symbols-example10” />`

每次调用`Symbol`函数都会创建一个新的唯一符号。然而，JavaScript还允许我们创建可以跨文件或`[realms](https://weizmangal.com/2022/10/28/what-is-a-realm-in-js/#:~:text=You%20can%20informally%20think%20of,order%20to%20exist%20within%20it.)`共享的符号。这就是全局符号库的概念。

我们可以使用`Symbol.for`方法在全局符号库中创建一个全局符号。

```js
1 const globalSymbolKey = "my-global-Symbol";
2 const mySymbol = Symbol.for(globalSymbolKey);
3 
4 console.log(mySymbol === Symbol.for(globalSymbolKey));
5 // true

```

您可以在下面的`Replit`中运行上述代码：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/global-symbols-example” />`

我们将一个键传递给`Symbol.for`方法，使用这个键，我们可以在全局符号库中检索与之关联的符号。如果该键在库中存在，`Symbol.for`方法将返回与之关联的符号；否则，它将在库中创建一个新的符号并将其与给定的键关联。

如果我们有一个全局符号，可以使用`Symbol.keyFor`方法获取与之关联的键。

```js
1 const globalSymbolKey = "my-global-Symbol";
2 const mySymbol = Symbol.for(globalSymbolKey);
3 
4 console.log(Symbol.keyFor(mySymbol));
5 // my-global-Symbol

```

这是一个`Replit`，您可以在其中运行上述代码：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/global-symbols-example2” />`

JavaScript语言使用多个内置符号来使不同功能工作，例如本模块早期课程中描述的`Symbol.toPrimitive`。这些符号被ECMAScript规范称为“众所周知的符号”。

尽管在 JavaScript 语言中的完整著名符号列表可以在 [ECMAScript 规范](https://tc39.es/ecma262/#sec-well-known-symbols) 中找到，但本节描述了一些著名符号。

### `Symbol.toPrimitive`

正如本模块早前的课程中所解释的，`Symbol.toPrimitive` 代表一个符号属性，该属性在 JavaScript 中被对象用于原始值转换过程。它的值是一个函数，该函数接收一个 `hint` 或 `preferred type`，用于表示被转换为原始值的对象。返回值用作对象的原始值。

以下代码示例将对象连接到 `movie` 对象的原始值转换过程，并根据 `hint` 参数的值返回对象的不同表示。

```js
 1 const movie = {
 2  name: "Jurassic Park",
 3  releaseDate: "09,June,1993",
 4 
 5  [Symbol.toPrimitive](hint) {
 6    if (hint === "number") {
 7      return new Date(this.releaseDate).getTime();
 8    } else {
 9      return this.name;
10     }
11   }
12 };
13 
14 console.log(Number(movie));
15 console.log(String(movie));

```

你可以在这个 Replit 中看到上述代码示例的输出：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/well-known-symbols-example1” />`

### `Symbol.toStringTag`

`Object.prototype.toString` 方法的默认实现对用户定义的对象并不是很有用。

```js
1 console.log({}.toString()); // [object Object]

```

对于某些内置对象，`toString` 方法的默认实现也不太有用。因此，许多对象重写了默认的 `toString` 实现。

```js
1 const arr = [1, 2, 3];
2 // overridden implementation
3 console.log(arr.toString()); // "1,2,3"
4 
5 // default implementation from Object.prototype
6 console.log(Object.prototype.toString.call(arr)); // [object Array]

```

你可以在这个 Replit 中看到上述代码示例的输出：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/well-known-symbols-example3” />`

注意默认 `toString` 实现的输出中的“Array”部分。这被称为标签。对于某些内置对象，标签是值的类型，例如，对于数组而言是“Array”，对于字符串而言是“String”。

对于用户定义的对象，默认的 `toString` 输出如上所示，是 `[object Object]`，其中标签是“Object”——这并不是很有用。

众所周知的符号 `Symbol.toStringTag` 允许我们改变标签的值。

```js
1 const task = {
2   title: "exercise",
3   isComplete: false,
4   [Symbol.toStringTag]: "Task"
5 };
6 
7 console.log(task.toString()); // [object Task]

```

你可以在这个 Replit 中看到上述代码示例的输出：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/well-known-symbols-example4” />`

### `Symbol.isConcatSpreadable`

`[Symbol.isConcatSpreadable]` 属性由数组的 `concat` 方法查找，以确定传递给 `concat` 方法的数组或类数组对象的元素是否应该被 `spread` 或扁平化。

```js
1 const arr = [1, 2, 3];
2 console.log([].concat(arr));
3 // [1, 2, 3]
4 
5 arr[Symbol.isConcatSpreadable] = false;
6 console.log([].concat(arr));
7 // [[1, 2, 3]]

```

你可以在这个 Replit 中看到上述代码示例的输出：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/well-known-symbols-example5” />`

正如上述代码示例的输出所示，数组的默认行为是展开其元素。可以通过将 `Symbol.isConcatSpreadable` 设置为 `false` 来覆盖此默认行为。

对于 [类数组对象](https://stackoverflow.com/questions/29707568/javascript-difference-between-array-and-array-like-object)，默认行为是不展开其属性。可以通过将 `Symbol.isConcatSpreadable` 设置为 `true` 来覆盖此行为。

```js
1 const obj = {
2   0: 123,
3   1: 456,
4   length: 2,
5   [Symbol.isConcatSpreadable]: true
6 };
7 
8 console.log([].concat(obj));
9 // [123, 456]

```

你可以在这个 Replit 中查看上述代码示例的输出：

`<ReplitEmbed src="https://replit.com/@newlineauthors/well-known-symbols-example6" />`

还有其他一些众所周知的符号，它们使我们能够连接到 JavaScript 中不同的内置操作。完整列表可以在 [`ECMAScript 规范`](https://tc39.es/ecma262/#sec-well-known-symbols) 或 [`MDN - Symbol`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol) 中查看。
