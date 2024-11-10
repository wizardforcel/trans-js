## `强制转换`

JavaScript 中的`强制转换`是将一种类型的值转换为另一种类型的值。

[MDN 对强制转换的定义](https://developer.mozilla.org/en-US/docs/Glossary/Type_coercion)是：

> `类型强制转换`是值从一种数据类型自动或隐式转换为另一种数据类型（例如字符串转换为数字）。

根据 MDN 的定义，如果值的转换是`隐式的`，那么这就是`强制转换`，而`类型转换`可以是`隐式`的也可以是`显式`的。

因此，如果开发者表达了将一种类型的值转换为另一种类型的意图，那就是`类型转换`。以下代码示例是一个`显式`类型转换的例子：

```js
1 const age = Number(ageStr);

```

如果类型转换是`隐式的`，也就是说开发者并没有表达任何将某个值转换为另一个值的意图，那么这就是`隐式类型转换`或`强制转换`。以下代码是`强制转换`的一个示例：

```js
1 const result = "50" - 20; // 30

```

每当 JavaScript 在一个期望不同类型值的上下文中看到一种类型的值时，它都会尝试将该值强制转换或转换为预期类型。在上面的代码示例中，`"50"`是意外的值类型，因为操作是减法。减法是在数字之间，而不是在字符串和数字之间。因此，作为意外值的`"50"`被转换为数字，即`50`。

然而，有些人可能会争辩说，在动态类型语言中，任何类型的转换都可以被视为`强制转换`。此外，`隐式`和`显式`类型转换之间的区别取决于人们如何看待`隐式`和`显式`类型转换。

话虽如此，重要的是我们要理解 JavaScript 中的`类型转换`过程。本模块的目标是帮助你理解 JavaScript 如何将一种类型的值转换为另一种类型，并使`类型转换`（无论是隐式还是显式）变得不那么可怕。

`强制转换`是许多 JavaScript 开发者普遍误解的主题，这主要是因为大多数在线资源建议远离`强制转换`，并将其呈现为一个应该避免的话题，而不是花时间去理解并在可能的情况下加以利用。

让许多 JavaScript 开发者，尤其是初学者，感到`强制转换`可怕的原因在于缺乏对这一主题的理解。`强制转换`被视为 JavaScript 的一种特性，通常更应该避免而不是理解。

`强制转换`是 JavaScript 的核心主题之一，其理解对深入理解 JavaScript 至关重要。无论多少在线资源告诉你要避免这个主题，只要你使用 JavaScript，就无法避免。与其回避，不如努力去理解它。考虑到这一点，在本模块中，我们将深入探讨这一主题，希望到模块结束时，你能对`类型强制转换`有一个扎实的理解。

强制类型转换是JavaScript的核心主题之一，其理解是深入理解JavaScript的关键。无论有多少在线资源告诉你避免这个主题，如果你使用JavaScript，这个主题是不可避免的。因此，与其避免它，不如试着去理解它？考虑到这一点，在本模块中，我们将更深入地探讨这个主题，希望到模块结束时，你能对类型强制转换有一个扎实的理解。

要深入理解强制类型转换，我们需要了解JavaScript如何将一个值转换为另一种类型的值。我们需要理解JavaScript执行类型转换时所采取的算法或步骤。

为了深入了解强制类型转换，让我们理解以下内容：

+   抽象操作

+   抽象相等运算符（`==`）

+   加法运算符（`+`）

+   关系运算符（`<`，`>`，`<=`，`>=`）

理解上述主题将帮助我们奠定理解JavaScript中类型转换过程的基础。因此，事不宜迟，让我们开始理解我们列表中的第一个项目，即抽象操作。

ECMAScript规范记录了几种机制，JavaScript语言用于将一种类型的值转换为另一种类型的值。这些机制被称为“**抽象操作**”；抽象的意思是这些并不是可以被JavaScript代码引用或调用的真实函数；相反，它们只是语言内部用于执行类型转换的算法步骤。

这些抽象操作在规范中写成似乎是实际函数的样子。例如，`operationName(arg1, arg2, ...)`，但规范明确指出，抽象操作是算法而不是可以被调用的实际函数。

ECMAScript规范中提到了许多[抽象操作](https://262.ecma-international.org/13.0/#sec-abstract-operations)，但在处理强制转换时，以下一些常见操作也被提及：

+   `ToPrimitive`

+   `ToNumber`

+   `ToString`

+   `ToBoolean`

尽管上述提到的抽象操作名称自我描述，但让我们理解它们是如何在类型转换中发挥作用的。

### `ToPrimitive`

`[ToPrimitive](https://262.ecma-international.org/13.0/#sec-toprimitive)` 抽象操作用于将对象转换为原始值。该操作接受两个参数：

+   `input`：一个应该被转换为原始值的对象

+   `preferredType`：一个可选的第二个参数，指定在将对象转换为原始值时应优先考虑的类型

#### `OrdinaryToPrimitive`

该操作调用另一个抽象操作，称为 `OrdinaryToPrimitive`，以执行实际转换，并且它还接受两个参数：

+   `O`：一个应该被转换为原始值的对象

+   ``hint``：在将对象转换为原始值时应优先考虑的类型。

``ToPrimitive`` 抽象操作调用 ``OrdinaryToPrimitive`` 抽象操作，将要转换为原始值的对象作为第一个参数传入，第二个参数 ``hint`` 的值根据下面描述的 ``preferredType`` 参数来设定：

+   如果 ``preferredType`` 为“string”，则将 ``hint`` 设置为字符串。

+   如果 ``preferredType`` 为“number”，则将 ``hint`` 设置为数字。

+   如果未指定 ``preferredType``，则将 ``hint`` 设置为数字。

JavaScript中的每个对象都从继承层次结构顶端的对象，即 ``Object.prototype`` 对象，继承以下两个方法：

+   ``toString()``

+   ``valueOf()``

##### ``toString()``

``toString`` 方法用于将对象转换为其字符串表示。``toString`` 方法的默认行为是将对象转换为以下（不太有用）形式：

```js
1 const obj = { a: 123 };
2 obj.toString(); // [object Object]

```

下面是上述代码的实际应用：

<ReplitEmbed src=”https://replit.com/@newlineauthors/abstract-operations-example1” />

由于 ``toString`` 方法的默认实现完全没有用，因此不同的对象会重写此方法，使其输出更有用。例如，内置的 ``Date`` 对象在转换为字符串时，会输出可读性强的日期字符串：

```js
1 new Date().toString(); // Sat Feb 04 2023 20:44:23 GMT+0500

```

下面是上述代码的实际应用：

<ReplitEmbed src=”https://replit.com/@newlineauthors/abstract-operations-example2” />

##### ``valueOf()``

``valueOf`` 方法用于将对象转换为原始值。此方法的默认实现与 ``toString`` 方法类似，基本无用，因为它只返回调用该方法的对象。

```js
1 const arr = [];
2 arr.valueOf() === arr; // true

```

下面是上述代码的实际应用：

<ReplitEmbed src=”https://replit.com/@newlineauthors/abstract-operations-example3” />

这意味着可以被其他对象重写。许多内置对象重写了这个方法。例如，对于``Date``对象，该方法返回自1970年1月1日00:00:00 UTC以来的毫秒数。

```js
1 // number of milliseconds will be different for you,
2 // depending on when you execute the code below
3 new Date().valueOf(); // 1675526929129

```

上面的代码执行效果如下：

<ReplitEmbed src=”https://replit.com/@newlineauthors/abstract-operations-example4” />

``OrdinaryToPrimitive``抽象操作调用``toString``和``valueOf``方法将对象转换为原始值。在这两种方法中，在某些情况下，仅调用其中一种；在其他情况下，都会调用它们。

``hint``参数由``OrdinaryToPrimitive``抽象操作接收，决定先调用这两种方法中的哪一种。

#### 优先选择字符串。

如果``hint``参数是“string”，那么``OrdinaryToPrimitive``抽象操作会首先调用对象上的``toString``方法。如果``toString``方法返回原始值，``即使该原始值不是字符串类型``，那么该原始值将被用作对象的原始表示。

如果`toString`方法不存在或未返回原始值，则调用`valueOf`方法。如果`valueOf`方法返回原始值，则使用该值；否则，抛出`TypeError`，表示对象无法转换为原始值。

```js
 1 const obj = {
 2  toString() {
 3    console.log("toString invoked");
 4    return "hello world";
 5  },
 6  valueOf() {
 7    console.log("valueOf invoked");
 8    return 123;
 9  }
10 };
11 
12 console.log(`${obj}`);
13 // toString invoked
14 // hello world

```

上面的代码执行效果如下：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/abstract-operations-example5” />`

在上面的代码示例中，我们有一个包含重写的`toString`和`valueOf`方法的对象。在代码示例的末尾，我们尝试将`obj`记录在一个嵌入的[模板字面量](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)中输出到控制台。在这种情况下，`obj`将被转换为字符串。

如上所述，当`OrdinaryToPrimitive`抽象操作的`hint`参数为“string”时，会调用`toString`方法将对象转换为原始值，优先转换为字符串类型的值。

由于`obj`对象的`toString`实现返回的是字符串原始值，因此`valueOf`方法未被调用，`obj`对象的对象到原始值的转换过程在此时完成。`obj`对象的`toString`方法返回的原始值被模板字面量使用。

但是上面提到过，`toString`方法返回的值可以是非字符串原始类型。以下代码示例验证了这一说法：

```js
 1 const obj = {
 2  toString() {
 3    console.log("toString invoked");
 4    return true;
 5  },
 6  valueOf() {
 7    console.log("valueOf invoked");
 8    return 123;
 9  }
10 };
11 
12 console.log(`${obj}`);
13 // toString invoked
14 // true

```

上面的代码执行效果如下：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/abstract-operations-example6” />`

上述代码示例中的`toString`方法返回一个布尔（非字符串）原始值。与调用`valueOf`方法或将`toString`方法的非字符串返回值转换为字符串值不同，布尔值被接受为`obj`对象的原始表示。

我们需要验证的下一个案例是，如果`toString`方法没有返回原始值会发生什么。以下代码示例演示了这种情况：

```js
 1 const obj = {
 2  toString() {
 3    console.log("toString invoked");
 4    return [];
 5  },
 6  valueOf() {
 7    console.log("valueOf invoked");
 8    return 123;
 9  }
10 };
11 
12 console.log(`${obj}`);
13 // toString invoked
14 // valueOf invoked
15 // 123

```

这里是上述代码的实际运行：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/abstract-operations-example7” />`

如前所述，如果`toString`方法没有返回原始值，则会调用`valueOf`方法以获取对象的原始表示。在上面的代码示例中，`toString`方法返回一个空的对象类型数组；因此，调用了`valueOf`方法。

即使对象没有定义`toString`，也会调用`valueOf`方法。以下代码示例展示了这种行为：

```js
 1 const obj = {
 2  toString: undefined,
 3  valueOf() {
 4    console.log("valueOf invoked");
 5    return 123;
 6  }
 7 };
 8 
 9 console.log(`${obj}`);
10 // valueOf invoked
11 // 123

```

这里是上述代码的实际运行：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/abstract-operations-example8” />`

我们需要验证的最后一个案例是，当JavaScript在调用`toString`和`valueOf`方法后仍无法获取原始值时会发生什么。

```js
 1 const obj = {
 2  toString() {
 3    console.log("toString invoked");
 4    return [];
 5  },
 6  valueOf() {
 7    console.log("valueOf invoked");
 8    return [];
 9  }
10 };
11 
12 console.log(`${obj}`);
13 // toString invoked
14 // valueOf invoked
15 // TypeError ...

```

这里是上述代码的实际运行：

`<ReplitEmbed src="https://replit.com/@newlineauthors/abstract-operations-example9" />`

当JavaScript在调用了两个方法后仍无法获取原始值时，会抛出`TypeError`，指示对象无法转换为原始值。因此，重要的是要记住在重写这些方法时，至少其中一个方法应返回一个原始值。

我们已经讨论了当首选类型为字符串时在对象到原始值转换过程中的情况。接下来，让我们讨论当首选类型为数字时会发生什么。

#### 优先考虑数字

如果提示参数为“number”，那么`OrdinaryToPrimitive`抽象操作会首先调用`valueOf`方法，然后在需要时调用`toString`方法。

这类似于上面讨论的“优先考虑字符串”案例，不同之处在于调用`valueOf`和`toString`方法的顺序是相反的。

```js
 1 const obj = {
 2  toString() {
 3    console.log("toString invoked");
 4    return "hello";
 5  },
 6  valueOf() {
 7    console.log("valueOf invoked");
 8    return 123;
 9  }
10 };
11 
12 console.log(obj + 1);
13 // valueOf invoked
14 // 124

```

下面是上述代码的实际运行：

`<ReplitEmbed src="https://replit.com/@newlineauthors/abstract-operations-example10" />`

上面的代码示例与上面部分中显示的示例相同，除了我们不是将`obj`嵌入模板字面量并记录到控制台，而是将1加到`obj`。我们将`obj`视为数字。

因此，当JavaScript在期望数字的上下文中获取对象时，它会尝试将对象强制转换为原始类型，优先转换为数字类型。

在这种情况下，传递给`OrdinaryToPrimitive`抽象操作的`hint`参数是“number”；因此，首先调用`valueOf`方法。由于它返回了一个原始值，因此无需调用`toString`方法。

剩下的情况与“优先考虑字符串”部分中讨论的相同。唯一的区别是，当首选类型为“number”时，首先调用`valueOf`方法。

如果`valueOf`方法返回布尔值，会发生什么？这是一个原始值。它不是数字，但仍然是一个原始值。因此，JavaScript应该将其视为`obj`对象的原始表示，对吗？

考虑以下代码示例：

```js
 1 const obj = {
 2  valueOf() {
 3    console.log("valueOf invoked");
 4    return true;
 5  }
 6 };
 7 
 8 console.log(obj + 1);
 9 // valueOf invoked
10 // 2

```

下面是上述代码的实际运行：

`<ReplitEmbed src="https://replit.com/@newlineauthors/abstract-operations-example11" />`

我们为什么会得到2作为输出？答案是`true`被视为`obj`对象的原始表示，但我们无法将`true`与`1`相加。JavaScript在这个上下文中期望的是一个数字。因此，它会尝试将`true`强制转换为期望的值类型，在这种情况下为`1`。如果`valueOf`方法返回`false`，它将被强制转换为`0`。

#### 无偏好

当调用`ToPrimitive`抽象操作而没有指定首选类型或提示，或者如果提示被设置为“default”，那么该操作通常表现得好像提示是“number”。因此，默认情况下，`ToPrimitive`更倾向于转换为数字类型。

然而，对象可以通过实现[`Symbol.toPrimitive`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol/toPrimitive)函数来覆盖这种默认的`ToPrimitive`行为。该函数接受一个首选类型作为参数，并返回对象的原始表示。

```js
 1 const obj = {
 2  [Symbol.toPrimitive](hint) {
 3    if (hint === "string") {
 4      return "hello";
 5    } else {
 6      return 123;
 7    }
 8  }
 9 };
10 
11 console.log(`${obj}`); // hello
12 console.log(obj + 1); // 124

```

以上代码的实际效果如下：

<ReplitEmbed src=”https://replit.com/@newlineauthors/abstract-operations-example12” />

在内置对象中，只有`Date`和`Symbol`对象覆盖了`ToPrimitive`抽象操作的默认行为。`Date`对象将默认行为实现为首选类型或提示为“string”时的效果。

```js
1 new Date()[Symbol.toPrimitive]("default"); // Tue Feb 07 2023 23:47:42 GMT+0500

```

以上代码的实际效果如下：

<ReplitEmbed src=”https://replit.com/@newlineauthors/abstract-operations-example13” />

:::note

我们很少需要显式调用`Symbol.toPrimitive`函数。JavaScript在需要将对象转换为原始值时会自动调用此函数。

:::

`ToPrimitive`抽象操作在下面的图像中进行了总结：

![对象到原始值转换总结](images/module_04----lesson_04.03----public----assets----ToPrimitive.png)

对象到原始值转换的总结

### `ToNumber`

[`ToNumber`](https://262.ecma-international.org/13.0/#sec-tonumber)抽象操作在JavaScript需要将任何非数字值转换为数字时使用。

以下表格显示了此抽象操作应用于一些非数字值的结果：

| 值 | ToNumber(value) |
| --- | --- |
| ”” | 0 |
| “0” | 0 |
| “-0” | -0 |
| ” 123 “ | 123 |
| “45” | 45 |
| “abc” | NaN |
| false | 0 |
| true | 1 |
| undefined | NaN |
| null | 0 |

就对象而言，`ToNumber`抽象操作首先使用`ToPrimitive`抽象操作将对象转换为原始值，首选类型为“number”，然后将结果值转换为数字。

[`BigInt`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt)值允许*显式*转换为数字类型，但*隐式*转换是不允许的；隐式转换会抛出`TypeError`。

```js
1 console.log(Number(10n)); // 10
2 
3 console.log(+10n); // TypeError...

```

以上代码的实际效果如下：

<ReplitEmbed src=”https://replit.com/@newlineauthors/abstract-operations-example14” />

### `ToString`

[`ToString`](https://262.ecma-international.org/13.0/#sec-tostring)抽象操作用于将任何值转换为字符串。

以下表格显示了此抽象操作应用于一些非字符串值的结果：

| 值 | ToNumber(value) |
| --- | --- |
| null | “null” |
| undefined | “undefined” |
| 0 | “0” |
| -0 | “0” |
| true | “true” |
| false | “false” |
| 123 | “123” |
| NaN | “NaN” |

在对象的情况下，`ToString`抽象操作首先使用`ToPrimitive`抽象操作将对象转换为原始值，首选类型为“string”，然后将结果值转换为字符串。

### `ToBoolean`

[ToBoolean](https://262.ecma-international.org/13.0/#sec-toboolean)抽象操作用于将值转换为布尔值。

与上述抽象操作不同，此操作仅仅是检查一个值是否为[falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy)值。如果是，我们返回`false`；对于所有其他值，此操作返回`true`。

以下是虚假值的列表：

+   `false`

+   `0`, `-0`, `0n`

+   `undefined`

+   `null`

+   `NaN`

+   `""`

正如前面提到的，ECMAScript规范中提到了许多用于类型转换的[抽象操作](https://262.ecma-international.org/13.0/#sec-abstract-operations)；在本课中，我们只讨论了常见的操作。

##### 进一步阅读

+   [数字强制转换 - (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number#number_coercion)

+   [字符串强制转换 - (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String#string_coercion)

+   [布尔强制转换 - (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean#boolean_coercion)

+   [强制转换值 - (你还不知道的 JS)](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/types-grammar/ch4.md)

让我们讨论臭名昭著的`双等号`运算符，它用于`松散`比较两个值。它也被称为`抽象相等`运算符。

这个运算符臭名昭著，因为许多在线资源以及一般的JavaScript开发者都不鼓励使用它，原因在于其强制类型转换行为。我们不应该盲目忽视`双等于`运算符，而是应该尝试理解它的行为，然后我们可以自行决定是否在我们的代码中完全不使用它，或者在安全的情况下使用它。

尽管你听说过这个运算符的种种，但它的行为遵循一些预定义的算法步骤，如果我们理解它的工作原理，这个运算符就不会让我们感到恐惧，在某些情况下，我们甚至可能更喜欢这个运算符而非它的“表亲”严格相等运算符（`===`）。

当使用`双等于`运算符比较两个值时，JavaScript进行比较的步骤由一种称为[IsLooselyEqual](https://tc39.es/ecma262/multipage/abstract-operations.html#sec-islooselyequal)的抽象操作描述。

### 抽象相等运算符总结

`双等于`运算符的工作过程大致总结如下：

+   如果比较的值是同一类型，则执行[严格相等比较](https://tc39.es/ecma262/multipage/abstract-operations.html#sec-isstrictlyequal)。

+   如果一个值是`undefined`或`null`，而另一个值也为`undefined`或`null`，则返回真。

+   如果一个或两个值是对象，则将它们转换为原始类型，优先考虑数字类型。

+   如果两个值都是原始类型但类型不同，则转换类型直到匹配，优先考虑数字类型进行强制转换。

#### 委托给严格相等比较

想想上面提到的第一点。如果使用该运算符比较的值类型相同，那么在底层，这两个值将使用三重等于或严格相等运算符进行比较。因此，如果我们知道在某段代码中只会比较相同类型的值，那么使用双等于或三重等于运算符没有区别；在这种情况下，我们将始终使用严格相等运算符。

#### `null` 与 `undefined`

第二点也值得深思。与严格相等运算符不同，抽象或宽松相等运算符认为`null == undefined`的比较为真。

```js
1 console.log(null === null); // true
2 console.log(undefined === undefined); // true
3 console.log(null === undefined); // false
4 
5 console.log(null == null); // true
6 console.log(undefined == undefined); // true
7 console.log(null == undefined); // true

```

你可以在下面看到上面的代码的实际运行：

`<ReplitEmbed src="https://replit.com/@newlineauthors/abstract-equality-operator-example1" />`

根据抽象相等运算符，`null`和`undefined`彼此相等，这为抽象相等运算符提供了一个有趣的用例。在编写JavaScript代码时，常常需要检查一个值既不是`null`也不是`undefined`。

使用严格相等运算符时，我们会有一个类似于以下的检查：

```js
1 if (someVal !== null && someVal !== undefined) {
2   // code
3 }

```

而使用抽象相等运算符时，我们可以将此检查简化为一个条件：

```js
1 if (someVal != null) {
2   // code
3 }
4 
5 // or
6 
7 if (someVal != undefined) {
8   // code
9 }

```

考虑到我们在JavaScript代码中多么频繁地需要防止`null`和`undefined`，我觉得抽象相等运算符在这种情况下是理想的。尽管如此，如果你在这种情况下使用严格相等运算符也不会错。

#### “if”条件

尽管抽象相等运算符的强制行为是可预测的，但正如上面所解释的，人们常常因为如何在`if`语句条件中使用该运算符而陷入陷阱。考虑以下代码示例：

```js
1 const someVal = {};
2 
3 if (someVal == true) {
4   console.log("if");
5 } else {
6   console.log("else");
7 }

```

你可以在下面看到上面的代码在实际中的效果：

`<ReplitEmbed src="https://replit.com/@newlineauthors/abstract-equality-operator-example4" />`

我们从之前的课程中知道，对象是[真值](https://developer.mozilla.org/en-US/docs/Glossary/Truthy)值。因此，在上述代码示例中，假设`if`条件会被评估为`true`似乎是合理的，这将导致执行`if`块。但是，如果你执行上述代码，你可能会惊讶地发现，执行的是`else`，因为`someVal == true`检查会评估为`false`。

如果抽象相等运算符的任一操作数是布尔值，它会首先被转换为数字——`false`变为`0`，`true`变为`1`。因此，上述代码示例中的`if`条件将被评估如下：

1.  一个操作数是对象，另一个是布尔值，因此根据[isLooselyEqual](https://tc39.es/ecma262/multipage/abstract-operations.html#sec-islooselyequal)抽象操作的**第10步**，如果一个操作数是布尔值，则使用`ToNumber`抽象操作将其转换为数字。所以我们的条件将变为：

    ```js
    1 someVal == 1;

    ```

1.  在将布尔值转换为数字后，我们有一个对象与数字之间的比较。根据`isLooselyEqual`抽象操作的**第12步**，对象`someVal`将使用`ToPrimitive`抽象操作转换为原始值，优先类型为“数字”。对象字面量的默认原始表示为`"[object Object]"`，因此经过强制转换后的条件将变为：`js "[object Object]" == 1;`

1.  现在，我们有一个字符串与数字之间的比较。根据`isLooselyEqual`抽象操作的**第6步**，如果一个操作数是字符串，另一个是数字，则将字符串转换为数字。将`"[object Object]"`转换为数字将给我们`[NaN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/NaN)`。所以我们的条件将变为：

    ```js
    1 NaN == 1;

    ```

1.  在进行三次强制转换后，我们有一个`NaN`值与一个数字之间的比较。它们彼此不相等。（`NaN`值与任何其他值（包括它自身）都不相等。）因此我们的条件未能评估为`true`。

上述讨论的目的在于理解，使用抽象相等运算符检查一个值是`true`还是`false`并不总是如预期那样有效。在这种情况下，很容易指责抽象相等运算符。但事实是，编写这种代码的人需要帮助，以理解或记住抽象相等运算符的工作原理。

在这种情况下，如果我们想要检查一个值是真值还是假值，不需要使用抽象相等运算符，利用`if`语句的强制行为就足够了。我所说的是，上述代码中的`if`条件应该写为：

```js
1 if (someVal) {
2   // code
3 }

```

在上述条件下，我们将获得预期结果，因为`someVal`会被检查是否为真值；如果是，条件将评估为真，从而执行`if`块。

所以，作为建议，避免进行如`someVal == true`的检查，其中一个操作数是布尔值。在这种情况下，利用`if`语句的隐式强制特性将检查值是否有效。

##### 深入阅读

+   [布尔陷阱 - 你还不知道JS](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/types-grammar/ch4.md#-boolean-gotcha)

+   [“if”语句的运行时语义（ECMAScript规范）](https://tc39.es/ecma262/multipage/ecmascript-language-statements-and-declarations.html#sec-if-statement)

### 加法运算符

加法运算符可以用来对两个数字进行加法运算，也可以用来连接两个字符串，这被称为字符串连接。

该运算符的工作原理基于[ApplyStringOrNumericBinaryOperator](https://tc39.es/ecma262/multipage/ecmascript-language-expressions.html#sec-applystringornumericbinaryoperator)。其工作方式是，如果任一或两个操作数是非原始值，则使用`ToPrimitive`抽象操作将它们转换为原始值，并且未指定首选类型。因此，“number”在这种情况下是首选类型，因为这是`ToPrimitive`抽象操作的默认行为。

在检查非原始操作数并将它们（如果有的话）强制转换为原始值后，下一步是检查一个或两个操作数是否为字符串。如果是这种情况，则将非字符串操作数（如果有的话）强制转换为字符串，并执行字符串连接。

如果两个操作数都不是字符串，则在将非数字操作数强制转换为数字后执行加法。

### 关系运算符

关系运算符（`<`，`>`，`<=`，`>=`）用于比较字符串和数字。在关系运算符的情况下调用的抽象操作是[IsLessThan](https://tc39.es/ecma262/multipage/abstract-operations.html#sec-islessthan)抽象操作。尽管其名称如此，但该操作也处理`<=`、`>`和`>=`比较。

如果任一操作数是对象，则将其转换为原始值，首选类型为“number”。如果两个操作数都是字符串，则使用它们的Unicode码点进行比较。如果不是字符串，则操作数通常会转换为数字，然后进行比较。

我们还可以使用关系运算符比较`Date`对象。请记住，当使用`ToPrimitive`操作将`Date`对象转换为原始值时，它们会被转换为字符串，但在关系运算符的情况下，`Date`对象在转换为原始值时会以数字表示，因为在关系运算符的情况下，`ToPrimitive`抽象操作被传递了“number”作为首选类型。

```js
1 const d1 = new Date("2022-11-03");
2 const d2 = new Date("2023-05-10");
3 
4 console.log(d1 < d2); // true

```

这是上述代码的实际效果的Replit：

`<ReplitEmbed src="https://replit.com/@newlineauthors/relational-operators-example1" />`

现在我们已经更深入地了解了强制转换以及一些常见抽象操作如何工作以使强制转换生效，让我们测试一下我们在本模块中所学到的知识。以下练习将使我们巩固对强制转换主题的理解。

以下是一些涉及强制转换的表达式。根据您在本模块中获得的知识，尝试猜测输出。如果您不理解所有内容，请不要担心。它们的解释也在下面提供。您显然可以参考规范以及本模块中的早期课程，以理解和猜测下面表达式的输出。

```js
 1 0 == false
 2 
 3 "" == false
 4 
 5 0 == []
 6 
 7 [123] == 123
 8 
 9 [1] < [2]
10 
11 [] == ![]
12 
13 !!"true" == !!"false"
14 
15 [1, 2, 3] + [4, 5, 6]
16 
17 [undefined] == 0
18 
19 [[]] == ''
20 
21 [] + {}

```

下面是对上述每个表达式输出的解释。

#### `0 == false`

让我们从一个简单的开始，大多数人可能会正确理解，即使不阅读此模块。现在我们知道抽象相等运算符的工作原理，让我们理解评估该表达式为`true`时所采取的步骤。

1.  由于类型不相等且其中一个操作数是布尔值，因此布尔操作数使用`ToNumber`抽象操作转换为数字。因此，第一次强制转换步骤是将`false`转换为数字，即`0`。表达式变为：

    ```js
    1 0 == 0

    ```

1.  现在类型相等，因此执行严格相等比较，即`0 === 0`，输出为`true`。

#### `"" == false`

1.  由于类型不相等且其中一个操作数是布尔值，因此布尔操作数使用`ToNumber`抽象操作转换为数字。因此，第一次强制转换步骤是将`false`转换为数字，即`0`。表达式变为：

    ```js
    1 "" == 0

    ```

1.  现在，我们有一个字符串和一个数字。请记住，抽象相等运算符优先考虑数字比较，因此字符串操作数使用`ToNumber`抽象操作转换为数字。空字符串在转换为数字时输出为`0`。因此，表达式变为：

    ```js
    1 0 == 0

    ```

1.  类型相等，因此执行严格相等比较，即`0 === 0`，输出为`true`。

#### `0 == []`

1.  数组使用`ToPrimitive`抽象操作转换为原始值。由于抽象相等运算符优先考虑数字比较，因此数组转换为数字作为首选类型的原始值。空数组在转换为原始值时输出为空字符串。因此，表达式变为：

    ```js
    1 0 == ""

    ```

1.  接下来，字符串将被转换为数字。将空字符串转换为数字时输出为`0`。因此，表达式变为：

    ```js
    1 0 == 0

    ```

1.  类型相等，因此执行严格相等比较，即`0 === 0`，输出结果为`true`。

#### `[123] == 123`

1.  我们有一个数组和一个数字之间的比较。因此，数组将使用`ToPrimitive`抽象操作转换为原始值，以数字为首选类型。`valueOf`方法将首先被调用，因为首选类型是数字。但我们知道，`valueOf`方法的默认实现只是返回调用它的对象。因此，接下来调用`toString`。对于数组，`toString`方法对空数组返回一个空字符串；对于像`[1, 2, 3]`这样的数组，它返回数组的内容，以字符串形式用逗号连接，即`"1,2,3"`。每个数组元素被强制转换为字符串，然后用逗号连接。

    在我们的例子中，数组中有一个元素，即`[123]`，因此它将被强制转换为`"123"`。所以表达式变为：

    ```js
    1 "123" == 123

    ```

1.  接下来，字符串将被转换为数字。因此表达式变为：

    ```js
    1 123 == 123

    ```

1.  类型相等，因此执行严格相等比较，即`123 === 123`，输出结果为`true`。

:::info 关于数组转换为原始值的奇怪事实：包含`null`或`undefined`的数组会被强制转换为一个空字符串，即`[null]` —> `""` 和 `[undefined]` —> `""`。类似地，包含两者的数组会被强制转换为包含单个逗号的字符串，即`[null, undefined]` —> `","`。为什么我们不会得到`"null"`、`"undefined"`和`"null,undefined"`这样的数组呢？这只是强制转换的一个边缘情况。:::

#### `[1] < [2]`

1.  这是两个对象之间的比较。两个数组都使用`ToPrimitive`抽象操作被转换为原始值，以数字为首选类型。如前面的示例所述，`toString`最终会被调用，将两个数组转换为原始值，分别输出为`"1"`和`"2"`。因此表达式变为：

    ```js
    1 "1" < "2"

    ```

1.  现在，我们有两个字符串。类型相等，因此执行严格相等比较，即`"1" < "2"`，输出结果为`true`，因为字符串是根据它们的Unicode代码点进行比较的。

#### `[] == ![]`

1.  在这个比较中，我们有两个运算符：抽象相等运算符和[Not (!)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_NOT)运算符。Not运算符的优先级高于相等运算符，因此子表达式`![]`会被首先计算。

    Not运算符将`true`转换为`false`，反之亦然。但在这里它与非布尔值一起使用。那么，当JavaScript在期望不同类型值的上下文中看到某个类型的值时会发生什么？强制转换！所以`[]`会被强制转换为布尔值，因为布尔值是期望的类型，使用`ToBoolean`抽象操作。由于`[]`是一个真值，它被强制转换为`true`，然后Not运算符否定它，将`true`转换为`false`。因此表达式变为：

    ```js
    1 [] == false

    ```

1.  接下来，布尔操作数，即`false`被转换为数字，即`0`。表达式现在是：

    ```js
    1 [] == 0

    ```

1.  现在我们在对象和数字之间进行比较。回忆一下抽象相等运算符的工作方式，对象将被转换为原始值，优先考虑数字类型。如前面的一个示例所述，空数组被转换为一个空字符串，因此表达式变为：

    ```js
    1 "" == 0

    ```

1.  接下来，空字符串被转换为数字，即`0`，使用`ToNumber`抽象操作。

    ```js
    1 0 == 0

    ```

1.  类型相等，因此执行严格相等比较，即`0 === 0`，输出结果为`true`。

:::note 如果你想知道我是如何知道哪个操作数（左侧或右侧）首先被强制转换，以及执行了什么强制转换，我只是参考了ECMAScript规范中提到的步骤。例如，对于涉及使用抽象相等运算符的比较的表达式，我是参考[`IsLooselyEqual`](https://tc39.es/ecma262/multipage/abstract-operations.html#sec-islooselyequal)抽象操作的步骤。

这就是你应该做的。同样没有必要记住每一个步骤。只需理解强制转换的基本原理，涉及哪些抽象操作，并参考规范即可。:::

#### `!!"true" == !!"false"`

1.  再次，我们在一个表达式中有两个操作符。如前所述，逻辑 `Not` 运算符的优先级较高，因此子表达式 `!!"true"` 和 `!!"false"` 将首先被计算。

    表达式 `!!"true"` 中的字符串 `"true"` 是一个真值，因此它将被强制转换为布尔值 `true`。因此，表达式将变为 `!!true`。接下来，我们有两次 `Not` 运算符的出现。将其应用于 `true` 两次将首先将其转换为 `false`，然后再转换回 `true`。

    第二个子表达式 `!!"false"` 也将计算为 `true`，因为字符串 `"false"` 是一个真值，所以与第一个子表达式相同，表达式将变为 `!!true`，然后应用两次 `Not` 运算符将得到 `true`。因此，在子表达式被强制转换和计算后，我们的表达式将变为：

    ```js
    1 true == true

    ```

1.  类型相等，因此执行严格相等比较，即 `true === true`，输出为 `true`。

#### [`[1, 2, 3] + [4, 5, 6]`](https://tc39.es/ecma262/multipage/ecmascript-language-expressions.html#sec-applystringornumericbinaryoperator)

1.  回忆一下加法运算符是如何工作的。这里涉及的抽象操作是 [`ApplyStringOrNumericBinaryOperator`](https://tc39.es/ecma262/multipage/ecmascript-language-expressions.html#sec-applystringornumericbinaryoperator)。

    由于两个操作数都是对象，它们首先被转换为没有指定优先类型的原始值用于 `ToPrimitive` 抽象操作。因此，默认情况下，“数字”是优先类型。数组在强制转换为原始值时，使用 `toString` 方法进行转换。对于我们表达式中的数组，我们将分别得到 `"1,2,3"` 和 `"4,5,6"`。所以表达式变为：

    ```js
    1 "1,2,3" + "4,5,6"

    ```

1.  由于两个操作数在强制转换后都是字符串，因此不是加法，而是执行连接，将两个字符串连接在一起，输出为 `"1,2,34,5,6"`。

#### [`[undefined] == 0`](https://tc39.es/ecma262/multipage/ecmascript-language-expressions.html#sec-applystringornumericbinaryoperator)

1.  正如我们在本节课中多次看到的，当对象与数字进行比较时，使用抽象相等运算符，对象首先被转换为原始值。回忆一下本节课早些时候提到的，`[undefined]` 转换为原始值时输出一个空字符串。因此，表达式变为：

    ```js
    1 "" == 0

    ```

1.  空字符串在转换为数字时，给我们 `0`。所以表达式变为：

    ```js
    1 0 == 0

    ```

1.  类型相等，因此执行严格相等比较，即 `0 === 0`，输出为 `true`。

#### `[[]] == ''`

1.  在这个表达式中，我们有一个包含空数组和空字符串的数组。数组操作数首先被转换为原始值。回想一下数组是如何转换为原始值的。除了前面提到的一些特殊情况，数组通过将其元素强制转换为字符串并用逗号连接它们来转换为原始值。因此，嵌套的空数组将被转换为原始值。当空数组被转换为原始值时，我们得到什么？是的，一个空字符串。所以，外层数组也被转换为一个空字符串。强制转换后的表达式变为：

    ```js
    1 "" == ""

    ```

1.  空字符串等于空字符串，因此输出为 `true`。

#### `[] + {}`

1.  由于运算符是加法运算符，且两个操作数都是对象，因此它们都被转换为没有优先类型的原始值。因此，默认情况下，优先类型被设置为“数字”。

    空数组被转换为一个空字符串，而对象字面量的默认原始表示为字符串 `"[object Object]"`。所以表达式变为：

    ```js
    1 "" + "[object Object]"

    ```

1.  两个操作数现在都是字符串，并且被连接，输出为 `"[object Object]"`。

##### 参考文献

上述一些表达式来自以下 GitHub 仓库：[wtfjs](https://github.com/denysdovhan/wtfjs)
