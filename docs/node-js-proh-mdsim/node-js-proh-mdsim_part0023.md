# 第3章：JavaScript 控制流语句

在第2章中，我们学习了JavaScript的语法、运算符和表达式。现在，让我们来探索控制流语句，这些语句可以让我们控制代码的执行流程。控制流语句使我们能够基于特定条件做出决策并重复执行操作。理解控制流对于创建动态和交互式的JavaScript程序至关重要。

# 3.1 条件语句

条件语句用于根据特定条件执行不同的代码块。它们通过做出决策来控制执行流程。JavaScript提供了几种条件语句，包括`if`语句、`if...else`语句和`switch`语句。

# 3.1.1 `if`语句

`if`语句是最简单的条件语句。如果给定的条件为真，它会执行一段代码块。以下是`if`语句的基本语法：

```jsjavascript

if (condition) {

// code to be executed if the condition is true

}

```

让我们来看一个例子：

```jsjavascript

var age = 18;

if (age >= 18) {

console.log("You are eligible to vote.");

}

```

在这个例子中，如果`age`变量大于或等于18，将显示消息"你有资格投票"。

# 3.1.2 `if...else`语句

`if...else`语句允许我们在条件为真时执行一段代码块，在条件为假时执行另一段代码块。以下是语法：

```jsjavascript

if (condition) {

// code to be executed if the condition is true

} else {

// code to be executed if the condition is false

}

```

让我们修改之前的例子，加入`if...else`语句：

```jsjavascript

var age = 16;

if (age >= 18) {

console.log("You are eligible to vote.");

} else {

console.log("You are not eligible to vote yet.");

}

```

在这种情况下，如果`age`变量小于18，将显示消息"你还没有资格投票"。

# 3.1.3 `switch`语句

`switch`语句用于根据不同的条件执行不同的操作。它会评估一个表达式，并执行与该表达式值匹配的相应案例。以下是语法：

```jsjavascript

switch (expression) {

case value1:

// code to be executed if the expression matches value1

break;

case value2:

// code to be executed if the expression matches value2

break;

default:

// code to be executed if the expression doesn't match any case

break;

}

```

让我们来看一个例子：

```jsjavascript

var day = "Monday";

switch (day) {

case "Monday":

console.log("It's the first day of the week.");

break;

case "Tuesday":

console.log("It's the second day of the week.");

break;

// ... more cases ...

default:

console.log("It's an unknown

day.");

break;

}

In this example, if the value of the `day` variable is "Monday," the message "It's the first day of the week" will be displayed. If the value is "Tuesday," the message "It's the second day of the week" will be displayed. If the value doesn't match any of the cases, the default message "It's an unknown day" will be displayed.

# 3.2 Looping Statements

Looping statements allow us to repeat a block of code multiple times. They are useful when we want to perform a task repeatedly or iterate over a collection of data. JavaScript provides several looping statements, including the `for` loop, the `while` loop, and the `do...while` loop.

# 3.2.1 The for Loop

The `for` loop is commonly used when we know the number of iterations in advance. It consists of three parts: initialization, condition, and update. Here's the syntax:

```javascript

for (initialization; condition; update) {

// 每次迭代时执行的代码

}

```js

Let's see an example of a `for` loop:

```javascript

for (var i = 1; i <= 5; i++) {

console.log(i);

}

```js

In this example, the loop will iterate five times, and the numbers 1 to 5 will be displayed.

# 3.2.2 The while Loop

The `while` loop is used when we don't know the exact number of iterations in advance. It continues to execute a block of code as long as the specified condition is true. Here's the syntax:

```javascript

while (condition) {

// 每次迭代时执行的代码

}

```js

Let's see an example of a `while` loop:

```javascript

var i = 1;

while (i <= 5) {

console.log(i);

i++;

}

```js

In this example, the loop will iterate five times, similar to the previous `for` loop example.

# 3.2.3 The do...while Loop

The `do...while` loop is similar to the `while` loop but guarantees that the code block is executed at least once before checking the condition. Here's the syntax:

```javascript

do {

// 每次迭代时执行的代码

} 当 (condition);

```js

Let's see an example of a `do...while` loop:

```javascript

var i = 1;

do {

console.log(i);

i++;

} 当 (i <= 5);

```

在这个例子中，循环将执行五次，就像之前的例子一样。

3.3 结论

在本章中，我们探讨了 JavaScript 控制流语句，包括条件语句和循环语句。我们学习了如何使用 `if` 和 `switch` 语句做出决策，以及如何使用 `for`、`while` 和 `do...while` 循环重复代码。理解控制流对于创建动态和互动的 JavaScript 程序至关重要。

在下一章，我们将深入探讨 JavaScript 函数，它们使我们能够将代码组织成可重用的模块并执行特定任务。准备好学习如何编写高效且模块化的 JavaScript 代码吧！
