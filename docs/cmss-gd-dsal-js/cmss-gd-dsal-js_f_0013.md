# 第1章

数据结构的重要性

当人们第一次学习编程时，他们的关注点是——而且应该是——让他们的代码正确运行。他们的代码用一个简单的标准来衡量：代码是否真的能工作？

随着软件工程师经验的增长，他们开始学习更多关于代码质量的层面和细微差别。他们了解到，可能有两个代码片段都完成相同的任务，但其中一个比另一个更好。

代码质量有许多衡量标准。一个重要的衡量标准是代码的可维护性。代码的可维护性涉及代码的可读性、组织性和模块化等方面。

然而，高质量代码的另一个方面是代码效率。例如，你可以有两个代码片段，它们都实现相同的目标，但一个比另一个运行得更快。

看看这两个函数，它们都打印从 `2` 到 `100` 的所有偶数：

| ​  | `function`​ `printNumbersVersionOne()` { |
| --- | --- |
| ​  | `let`​ `number = 2;` |
| ​  |  |
| ​  | `while`​ (`number <= 100`) { |
| ​  | `// 如果数字是偶数，打印它:`​ |
| ​  | `if`​ (`number % 2 === 0`) { |
| ​  | `console.log(number);` |
| ​  | } |
| ​  |  |
| ​  | `number += 1;` |
| ​  | } |
| ​  | } |
| ​  | `function`​ `printNumbersVersionTwo()` { |
| ​  | `let`​ `number = 2;` |
| ​  |  |
| ​  | `while`​ (`number <= 100`) { |
| ​  | `console.log(number);` |
| ​  |  |
| ​  | `// 将数字增加 2，这在定义上是下一个偶数:`​ |
| ​  | `number += 2;` |
| ​  | } |
| ​  | } |

你认为这两个函数中哪个运行得更快？

如果你说是 `版本 2`，那么你在正确的思路上。`版本 1` 最终循环了 `100` 次，而 `版本 2` 只循环了 `50` 次。因此，第一个版本的步骤是第二个版本的两倍。

这本书是关于编写高效代码的。能够编写快速运行的代码是成为更优秀软件开发者的重要方面。

编写快速代码的第一步是理解数据结构是什么，以及不同的数据结构如何影响我们代码的速度。所以让我们深入探讨一下。
