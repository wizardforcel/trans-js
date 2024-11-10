# 第4章

控制结构

让我们谈谈编程的一个支柱：控制结构。它们是任何编程语言逻辑的基础，允许你以智能和高效的方式引导代码的执行流。在 JavaScript 中，我们有几种控制结构，帮助我们根据特定条件做出决策和重复动作。今天，我们将探索条件结构、重复结构、函数和作用域。深入理解这些主题对于编写干净、高效的代码至关重要。

条件结构（`if`、`else`、`switch`）

条件结构用于在代码中做出决策。它们允许根据特定条件执行不同的代码块。

if、else if、else：这些是 JavaScript 中最基本和最常用的条件结构。它们允许在条件为真时执行代码块。

```jsjavascript

let age = 20;

if (age < 18) {

console.log("Minor");

} else if (age >= 18 && age < 65) {

console.log("Adult");

} else {

console.log("Elderly");

}

```

在这个示例中，我们验证年龄并根据年龄范围打印相应的消息。

switch：`switch` 是 `if-else` 的一种替代，尤其在你有多个条件需要检查时非常有用。它将一个表达式与多个案例进行比较，并执行相应的代码块。

```jsjavascript

let diaSemana = 3;

switch (diaSemana) {

case 1:

console.log("Monday");

break;

case 2:

console.log("Tuesday");

break;

case 3:

console.log("Wednesday");

break;

case 4:

console.log("Thursday");

break;

case 5:

console.log("Friday");

break;

case 6:

console.log("Saturday");

break;

case 7:

console.log("Domingo");

break;

default:

console.log("Invalid day");

}

```

在上面的示例中，`switch` 检查 `dayWeek` 的值并打印相应的日期。如果没有匹配的情况，则执行默认块。

重复结构（`for`、`while`、`do-while`）

重复结构用于根据条件多次执行一个代码块。JavaScript 提供了几种选项，每种选项适合不同的场景。

for：`for` 循环是最常见和多用途的重复结构之一。它在我们知道想要执行的确切迭代次数时使用。

```jsjavascript

for (let i = 0; i < 5; i++) {

console.log(`Iteration ${i}`);

}

```

在这个示例中，`for` 循环运行代码块五次，每次打印迭代次数。

while：`while` 循环用于当我们不知道确切的迭代次数时，但希望在条件为真的情况下继续执行代码块。

```jsjavascript

let counter = 0;

while (contador < 5) {

console.log(`Counter: ${counter}`);

counter++;

}

```

上面的 `while` 循环会一直执行，直到 `counter` 的值等于或大于 5。

do-while：`do-while` 循环类似于 `while` 循环，但它确保在检查条件之前至少执行一次代码块。

```jsjavascript

let number = 0;

do {

console.log(`Number: ${number}`);

number++;

} while (number < 5);

```

即使在开始时条件为假，`do-while` 循环中的代码块也至少会执行一次。

函数与作用域

函数是执行特定任务的代码块，可以在程序的不同部分重复调用。它们对于代码的模块化和重用至关重要。

函数声明：函数可以使用 `function` 关键字声明。

```jsjavascript

function greeting(name) {

return `Hello, ${name}!`;

}

console.log(saudacao("Maria"));

```

在这个示例中，`saudacao` 函数接受一个 `name` 参数并返回个性化的问候。

函数表达式：函数也可以定义为表达式并赋值给变量。

```jsjavascript

const multiplicar = function(a, b) {

return a * b;

};

console.log(multiply(3, 4));

```

箭头函数：箭头函数在 ES6 中引入，提供了更简洁的语法，特别适用于回调函数。

```jsjavascript

const dividir = (a, b) => a / b;

console.log(split(10, 2));

```

作用域：作用域决定了变量在代码不同部分的可访问性。在 JavaScript 中，我们有两种主要的作用域：全局作用域和局部作用域。

全局作用域：在任何函数外声明的变量具有全局作用域，可以在代码的任何地方访问。

```jsjavascript

let message = "Hello world!";

function displayMessage() {

console.log(message);

}

displayMessage();

```

局部作用域：在函数内声明的变量具有局部作用域，仅能在该函数内部访问。

```jsjavascript

function calcularSoma(a, b) {

let soma = a + b;

return soma;

}

console.log(calcularSoma(5, 7));

// console.log(sum); // This would result in an error as 'sum' is not defined in the global scope.

```

块级作用域：随着 ES6 中 `let` 和 `const` 的引入，JavaScript 增加了块级作用域。用 `let` 或 `const` 声明的变量仅限于其定义的块，例如在循环或条件语句中。

```jsjavascript

if (true) {

let message = "Inside the block";

console.log(message); // It works

}

// console.log(message); // Error: message is not defined in global scope

```

闭包：JavaScript 中函数的强大特性之一是闭包。闭包是一个函数，它记住了创建时的作用域，即使该作用域已经关闭。

```jsjavascript

function criarContador() {

let counter = 0;

return function() {

counter++;

return contador;

};

}

const counter1 = createCounter();

console.log(contador1()); // 1

console.log(contador1()); // 2

const counter2 = createCounter();

console.log(contador2()); // 1

```

在上面的例子中，每个 `criarCounter` 的实例为变量 `counter` 创建了一个新的作用域，返回的函数记住了这个作用域，从而允许独立操作变量 `counter`。

我们探索 JavaScript 中的控制结构，从条件语句和循环到函数和作用域。这些工具对于编写高效、模块化和可维护的代码至关重要。理解和掌握这些结构将使你能够创建更复杂和强大的程序，面对任何挑战。在接下来的学习中，我们将继续在这些基础上发展，探索 JavaScript 的更高级应用。准备好将每一行代码变成学习和创新的机会吧。
