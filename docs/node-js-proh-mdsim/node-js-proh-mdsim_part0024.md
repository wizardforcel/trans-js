# 第四章：JavaScript 函数

在第三章中，我们探讨了 JavaScript 中的控制流语句，它们使我们能够做出决策并重复代码块。现在，让我们深入了解 JavaScript 函数，它们是构建模块化和可重用代码的关键部分。

# 4.1 函数简介

JavaScript 中的函数是执行特定任务或计算某个值的代码块。函数使我们能够将代码组织成逻辑清晰、可重用的单元。它们有助于提高代码的可读性，促进代码重用，并使我们的程序更加易于管理。

# 4.2 函数声明

在 JavaScript 中，我们可以使用 `function` 关键字声明一个函数，后面跟上函数名、参数列表（可选）以及用大括号括起来的代码块。以下是函数声明的基本语法：

```jsjavascript

function functionName(parameter1, parameter2, ...) {

// code to be executed

}

```

让我们定义一个简单的函数，用来计算一个数字的平方：

```jsjavascript

function square(number) {

var result = number * number;

return result;

}

```

在这个示例中，我们声明了一个名为 `square` 的函数，它接受一个名为 `number` 的参数。在函数内部，我们通过将 `number` 乘以自身来计算 `number` 的平方，并将结果赋值给一个名为 `result` 的变量。最后，我们使用 `return` 语句返回计算结果。

# 4.3 函数调用

为了执行一个函数并获得期望的结果，我们需要通过使用函数名后跟圆括号 `()` 并传递必要的参数（如果有的话）来调用或执行该函数。以下是调用 `square` 函数的示例：

```jsjavascript

var number = 5;

var squaredNumber = square(number);

console.log(squaredNumber); // Output: 25

```

在这个示例中，我们将值 `5` 赋给变量 `number`。然后，我们通过传递 `number` 作为参数来调用 `square` 函数。返回的结果 `25` 被赋值给变量 `squaredNumber`，然后我们将其输出到控制台。

# 4.4 函数参数和参数值

函数可以接受参数，参数充当在调用函数时传递给函数的值的占位符。参数使得函数具有灵活性，可以处理不同的值。当我们调用一个函数时，我们传递实际的值（即参数的值），这些值替代了函数中的参数。让我们修改我们的`square`函数，利用参数的优势：

```jsjavascript

function square(number) {

var result = number * number;

return result;

}

var number = 5;

var squaredNumber = square(number);

console.log(squaredNumber); // Output: 25

```

在这个例子中，函数声明中的`number`参数充当我们在调用函数时传递的值的占位符（在此情况下是`5`）。

# 4.5 函数返回语句

函数中的`return`语句用于指定函数应返回的值。它标志着函数执行的结束，并将指定的值返回给调用者。让我们修改我们的`square`函数，加入返回语句：

```jsjavascript

function square(number) {

return number * number;

}

var number = 5;

var squaredNumber = square(number);

console.log(squaredNumber); // Output: 25

```

在这个更新版本中，`return`语句直接返回计算结果，而无需使用中间变量。

# 4.6 函数作用域

JavaScript中的函数有它们自己的作用域。函数内部声明的变量是局部作用域的，这意味着它们只能在函数内部访问。相反，函数外部声明的变量具有全局作用域，可以在代码的任何地方访问。让我们通过一个例子来检查函数作用域的概念：

```jsjavascript

var globalVariable = "I'm a global variable";

function myFunction() {

var localVariable = "I'm a local variable";

console.log(localVariable);     // Output: I'm a local variable

console.log(globalVariable);    // Output: I'm a global variable

}

myFunction();

console.log(localVariable);        // Error: localVariable is not defined

console.log(globalVariable);       // Output: I'm a global variable

```

在这个例子中，我们有一个名为`globalVariable`的全局变量，它可以在代码的任何地方访问。在`myFunction`函数内部，我们声明了一个名为`localVariable`的局部变量，它只能在函数内部访问。当我们调用`myFunction`时，它会正确地打印`localVariable`和`globalVariable`的值。然而，如果我们尝试在函数外部访问`localVariable`，将会发生错误，因为它没有在全局作用域中定义。

# 4.7 函数表达式

除了函数声明，JavaScript 还支持函数表达式。函数表达式涉及将一个函数赋值给变量，使其成为一个可以传递和调用的对象。以下是一个函数表达式的示例：

```jsjavascript

var greet = function(name) {

console.log("Hello, " + name + "!");

};

greet("John");     // Output: Hello, John!

```

在这个示例中，我们通过将一个匿名函数赋值给变量 `greet` 来创建一个函数表达式。该函数接受一个 `name` 参数并将问候语输出到控制台。然后我们可以通过调用 `greet` 并传递参数来执行该函数。

# 4.8 箭头函数

ES6 引入了箭头函数，它提供了一种简洁的语法来编写函数。箭头函数特别适用于编写简短且可读性更强的代码。以下是一个箭头函数的示例：

```jsjavascript

var double = (number) => number * 2;

console.log(double(5));    // Output: 10

```

在这个示例中，我们定义了一个名为 `double` 的箭头函数，该函数接受一个 `number` 参数并返回该数字的双倍值。箭头函数语法 `(number) => number * 2` 代表了一种简洁的函数编写方式。

4.9 结论

在本章中，我们探讨了 JavaScript 函数，它允许我们将代码组织成可重用的块并执行特定任务。我们学习了函数声明、调用、参数、返回语句、函数作用域、函数表达式和箭头函数。函数是 JavaScript 编程的基础构建块，使我们能够编写模块化、可重用和高效的代码。

在下一章，我们将深入探讨 JavaScript 数组，这是一个强大的数据结构，允许我们存储和操作元素集合。准备好探索数组的世界，释放它们的全部潜力吧！
