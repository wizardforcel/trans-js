# # 第三章：控制流与循环

在第二章中，我们已经对 JavaScript 中的数据类型和变量有了扎实的理解。现在，到了使用条件语句和循环来控制代码流的时刻。控制流使我们能够根据特定条件做出决策并执行相应的代码块，而循环则提供了一种重复执行任务直到条件满足的机制。通过掌握控制流和循环，你将解锁 JavaScript 的全部潜力，并能够构建更具动态性和互动性的应用程序。让我们深入了解吧！

## 条件语句：在代码中做出决策

条件语句使我们能够在代码中创建决策逻辑。根据条件的真假，特定的代码块会被执行。JavaScript 提供了三种类型的条件语句：`if`、`if...else` 和 `switch`。

### `if` 语句：

`if` 语句是最基本的条件语句形式。如果指定的条件为 `true`，则执行该代码块。

```jsjavascript

// Example 1: Using the if statement

let age = 25;

if (age >= 18) {

console.log("You are an adult.");

}

```

在示例 1 中，代码检查 `age` 是否大于或等于 18。如果为真，它打印 "You are an adult."

### `if...else` 语句：

`if...else` 语句允许我们在条件为 `true` 时执行一个代码块，在条件为 `false` 时执行另一个代码块。

```jsjavascript

// Example 2: Using the if...else statement

let isRaining = true;

if (isRaining) {

console.log("It's raining. Don't forget your umbrella!");

} else {

console.log("No rain. Have a great day!");

}

```

在示例 2 中，代码检查 `isRaining` 是否为 `true`。如果为真，它打印 "It's raining. Don't forget your umbrella!"；否则，它打印 "No rain. Have a great day!"

### `else if` 语句：

`else if` 语句允许我们在决策过程中添加多个条件。

```jsjavascript

// Example 3: Using the else if statement

let time = 14;

if (time < 12) {

console.log("Good morning!");

} else if (time < 18) {

console.log("Good afternoon!");

} else {

console.log("Good evening!");

}

```

在示例 3 中，代码检查 `time` 的值，并根据一天中的时间打印不同的问候语。

### `switch` 语句：

`switch` 语句提供了一种处理多个条件的替代方式。

```jsjavascript

// Example 4: Using the switch statement

let day = "Monday";

switch (day) {

case "Monday":

console.log("It's the beginning of the week.");

break;

case "Friday":

console.log("It's almost the weekend!");

break;

default:

console.log("It's a regular day.");

}

```

在示例 4 中，代码检查 `day` 的值，并根据星期几打印不同的消息。

## 循环：重复执行代码

循环在编程中至关重要，因为它们使我们能够反复执行某段代码，直到满足特定条件为止。JavaScript 提供了多种类型的循环，包括 `for` 循环、`while` 循环、`do...while` 循环和 `for...of` 循环。

### `for` 循环：

`for` 循环适用于当你知道要执行的迭代次数时。

```jsjavascript

// Example 5: Using the for loop

for (let i = 1; i <= 5; i++) {

console.log("Iteration: " + i);

}

```

在示例 5 中，`for` 循环会执行大括号中的代码五次，因为 `i` 从 1 开始，并在每次迭代时增加 1，直到达到 5。

### `while` 循环：

`while` 循环用于当你希望重复执行某个代码块，直到某个特定条件变为 `false`。

```jsjavascript

// Example 6: Using the while loop

let count = 0;

while (count < 5) {

console.log("Count: " + count);

count++;

}

```

在示例 6 中，`while` 循环会在 `count` 变为 5 之前执行大括号中的代码，因为它在每次迭代时都会增加 1。

### `do...while` 循环：

`do...while` 循环与 `while` 循环类似，但它确保在检查条件之前，循环体内的代码至少执行一次。

```jsjavascript

// Example 7: Using the do...while loop

let i = 0;

do {

console.log("Value of i: " + i);

i++;

} while (i < 5);

```

在示例 7 中，`do...while` 循环会至少执行一次大括号中的代码，因为条件是在第一次迭代后才检查的。

### `for...of` 循环：

`for...of` 循环用于遍历可迭代对象的元素，例如数组和字符串。

```jsjavascript

// Example 8: Using the for...of loop

let fruits = ["apple", "banana", "orange"];

for (let fruit of fruits) {

console.log(fruit);

}

```

在示例 8 中，`for...of` 循环遍历 `fruits` 数组并打印每一个水果。

### `break` 和 `continue` 语句：

`break` 语句允许你在满足特定条件时提前退出循环。`continue` 语句允许你跳过当前迭代的其余部分并进入下一次迭代。

```jsjavascript

// Example 9: Using the break and continue statements

for (let i = 1; i <= 10; i++) {

if (i === 5) {

break; // Exit the loop when i is 5

}

if (i === 3) {

continue; // Skip the rest of the current iteration when i is 3

}

console.log("Value of i: " + i);

}

```

在示例 9 中，`break` 语句用于在 `i` 等于 5 时退出循环，而 `continue` 语句用于在 `i` 等于 3 时跳过当前迭代的其余代码。

## 实践中的控制流和循环

现在我们已经理解了条件语句和循环，接下来让我们探索一些它们的实际应用示例。

### 示例 10：查找偶数

让我们编写一个程序，找出1到10之间的所有偶数。

```jsjavascript

// Example 10: Finding even numbers

for (let i = 1; i <= 10; i++) {

if (i % 2 === 0) {

console.log(i + " is an even number.");

}

}

```

输出：

```js

2 is an even number.

4 is an even number.

6 is an even number.

8 is an even number.

10 is an even number.

``

`

In Example 10, the `for` loop iterates from 1 to 10, and the `if` statement checks if the current value of `i` is even (i.e., divisible by 2). If it's even, it prints the number and a message.

### Example 11: Sum of Numbers

Let's write a program that calculates the sum of numbers from 1 to 100.

```javascript

// 示例11：数字之和

let sum = 0;

for (let i = 1; i <= 100; i++) {

sum += i;

}

console.log("1到100的数字之和是: " + sum);

```js

Output:

```

1到100的数字之和是: 5050

```js

In Example 11, the `for` loop calculates the sum of numbers from 1 to 100 and stores the result in the `sum` variable.

### Example 12: Countdown Timer

Let's write a program that creates a countdown timer.

```javascript

// 示例12：倒计时器

let countDownFrom = 10;

while (countDownFrom >= 0) {

console.log(countDownFrom);

countDownFrom--;

}

console.log("时间到！");

```js

Output:

```

10

9

8

7

6

5

4

3

2

1

0

时间到！

```

在示例12中，`while`循环创建了一个从10开始的倒计时器，并在每次迭代中减少`countDownFrom`的值，直到它达到0。

## 结论

恭喜！在本章中，我们探讨了JavaScript中的控制流和循环。我们学习了如何使用条件语句（`if`，`if...else`，`else if`，和`switch`）在代码中做出决策，以及如何使用不同类型的循环（`for`，`while`，`do...while`，和`for...of`）来重复执行代码，直到满足某些条件。我们还看到了如何在实际场景中应用控制流和循环的实际示例。

控制流和循环是JavaScript中强大的工具，它们使我们能够创建动态和交互式应用程序。掌握这些知识，你就离成为一名熟练的JavaScript程序员不远了。
