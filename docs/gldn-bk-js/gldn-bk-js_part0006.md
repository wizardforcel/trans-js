# `第3章`

`JavaScript基础`

想象一下我们在一个教室里，准备开始进入`JavaScript`的核心。本章至关重要，因为我们将奠定支持您未来所有语言知识的基础。让我们一起探索基本语法、原始数据类型，以及构成`JavaScript`基础的运算符和表达式。拿起您的咖啡或茶，让我们以轻松实用的方式开始关于`JavaScript`基础的讨论。

`基本语法`

`JavaScript`语法是语言的语法规则，决定了我们如何编写代码。理解基本语法就像学习新语言中的句子结构；这是有效沟通的第一步。

`变量声明`：在`JavaScript`中，我们使用三个关键字来声明变量：`var`、`let`和`const`。每个关键字都有其特定的作用域和用途。

```jsjavascript

var name = "John"; // Global or function scope

let age = 25; // Block scope

const city = "São Paulo"; // Constant, cannot be reassigned

```

`代码注释`：注释对于提高代码的可读性和理解性至关重要。在`JavaScript`中，我们可以使用两个斜杠来进行单行注释，或使用斜杠和星号进行多行注释。

```jsjavascript

// This is a one-line comment

/*

This is a comment

multi-line

*/

```

`基本结构`：`JavaScript`使用大括号来分组语句并定义代码块，如`函数`、`循环`和`条件语句`。

```jsjavascript

if (age > 18) {

console.log("You are of legal age");

}

```

`原始数据类型`

`原始数据类型`是`JavaScript`中的基本构建块。它们表示最简单的值且不可变，即不能直接更改。

`数字`：表示数值，包括整数和小数。

```jsjavascript

let integer = 10;

let decimal = 10.5;

```

`字符串`：用于表示文本的字符序列。它们可以用单引号、双引号或反引号来界定。

```jsjavascript

let greeting = "Hello, world!";

let phrase = 'JavaScript is amazing!';

let template = `My age is ${age}`;

```

`布尔值`：表示真或假的值。

```jsjavascript

let true = true;

let false = false;

```

`空`和`未定义`：`空`是一个故意为空的值，而`未定义`表示一个变量已经声明但尚未初始化。

```jsjavascript

let empty = null;

let semValor;

```

`符号`：一种独特且不可变的数据类型，通常用作对象属性的唯一标识符。

```jsjavascript

let symbol1 = Symbol('description');

let symbol2 = Symbol('description');

```

`运算符和表达式`

`运算符`是指示值应如何组合或比较的符号。`表达式`是值和运算符的组合，结果为最终值。

`算术运算符`：用于执行基本的数学运算。

```jsjavascript

let sum = 10 + 5; // Addition

let subtraction = 10 - 5; // Subtraction

let multiplication = 10 * 5; // Multiplication

let division = 10 / 5; // Division

let modulo = 10 % 3; // Rest of Division

let exponentiation = 2 ** 3; // Exponentiation

```

`赋值运算符`：用于将值赋给变量。

```jsjavascript

let x = 10;

x += 5; // Equivale a x = x + 5

x -= 3; // Equivale a x = x - 3

x *= 2; // Equivale a x = x * 2

x /= 4; // Equivale a x = x / 4

x %= 2; // Equivale a x = x % 2

x **= 3; // Equivale a x = x ** 3

```

`比较运算符`：用于比较值并返回布尔值。

```jsjavascript

let equals = 10 == '10'; // True, as it only compares value

let strictlyEqual = 10 === '10'; // False, as it compares value and type

let different = 10 != '10'; // False, as it only compares value

let strictlyDifferent = 10 !== '10'; // True, as it compares value and type

let major = 10 > 5; // TRUE

let minor = 10 < 5; // Fake

let greaterOrEqual = 10 >= 10; // TRUE

let smallerOrEqual = 10 <= 10; // TRUE

```

`逻辑运算符`：用于组合布尔表达式。

```jsjavascript

let e = true && false; // And of course, it returns false

let ou = true || false; // Or logical, returns true

let no = !true; // Logical negation, returns false

```

`三元运算符`：一种简洁的方式来执行条件操作。

```jsjavascript

let result = age >= 18 ? "Of legal age": "Minor";

```

`按位运算符`：直接对操作数的位进行操作。

```jsjavascript

let andBitwise = 5 & 1; // E bit a bit

let orBitwise = 5 | 1; // Ou bit a bit

let xorBitwise = 5^1; // Or bitwise exclusive

let notBitwise = ~5; // Bitwise negation

let shiftLeft = 5 << 1; // Shift left

let shiftRight = 5 >> 1; // Shift right

```

`控制结构`：用于指导代码执行的流程。

`条件语句`：`if`、`else if`、`else`

```jsjavascript

if (age < 18) {

console.log("Minor");

} else if (age === 18) {

console.log("You are exactly 18 years old");

} else {

console.log("Of legal age");

}

```

`切换`：当您有多个条件需要检查时，它是`if-else`的替代方案。

```jsjavascript

let him = 3;

switch (dia) {

case 1:

console.log("Monday");

break;

case 2:

console.log("Tuesday");

break;

case 3:

console.log("Wednesday");

break;

default:

console.log("Invalid day");

}

```

`循环`：`for`、`while`、`do-while`

```jsjavascript

for (let i = 0; i < 5; i++) {

console.log(i);

}

let counter = 0;

while (contador < 5) {

console.log(contador);

counter++;

}

let num = 0;

do {

console.log(num);

num++;

} while (num < 5);

```

`函数`：`函数`是可以定义一次并多次重用的代码块。在`JavaScript`中可以通过多种方式声明它们。

`声明的函数`：

```jsjavascript

function greeting(name) {

return `Hello, ${name}!`;

}

console.log(greeting("João"));

```

`匿名函数`：

```jsjavascript

let saudacaoAnonima = function(nome) {

return `Hello, ${name}!`;

};

console.log(saudacaoAnonima("Maria"));

```

`箭头函数`：

```jsjavascript

let greetingArrow = (name) => `Hello, ${name}!`;

console.log(saudacaoArrow("Pedro"));

```

`函数`对于模块化代码和避免不必要的重复至关重要。它们还允许逻辑的封装，使代码更有组织，维护起来更容易。

在这一章中，我们将探索`JavaScript`的基础知识，从其基本语法到原始数据类型、运算符和表达式。理解这些概念对推进你的`JavaScript`学习和开发旅程至关重要。这些元素在构建稳健且高效的应用程序中发挥着重要作用。随着我们继续前进，我们将以这些基础为基础，探索更高级和复杂的主题。保持你的好奇心和学习热情，我们将一起把每一个挑战变成成长和创新的机会。
