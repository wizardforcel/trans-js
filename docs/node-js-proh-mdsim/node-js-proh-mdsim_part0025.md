# 第5章：JavaScript 数组

在第4章中，我们探讨了 JavaScript 函数，它们允许我们将代码组织成可重用的代码块。现在，让我们深入了解 JavaScript 数组，这是一种强大的数据结构，能够让我们存储和操作元素集合。

# 5.1 数组简介

在 JavaScript 中，数组是一种数据结构，允许我们在单个变量中存储多个值。数组是有序的、索引化的集合，每个值都被分配一个从 0 开始的唯一索引。数组可以包含任何数据类型的元素，例如数字、字符串、对象，甚至其他数组。它们提供了各种方法和属性，可以高效地对存储的数据进行操作。

# 5.2 创建数组

在 JavaScript 中有两种常见的创建数组的方式：使用数组字面量和`Array`构造函数。

# 5.2.1 数组字面量

数组字面量是创建数组最简单和最常用的方式。它们通过将以逗号分隔的值列表放在方括号`[]`内来实现。以下是一个示例：

```jsjavascript

var fruits = ['apple', 'banana', 'orange'];

```

在这个示例中，我们创建了一个名为`fruits`的数组，包含三个元素：`'apple'`、`'banana'` 和 `'orange'`。

# 5.2.2 使用 Array 构造函数

JavaScript 还提供了`Array`构造函数来创建数组。我们可以使用`new`关键字后跟`Array()`来创建一个空数组，或者将值传递到括号内，用以初始化数组中的特定元素。以下是一些示例：

```jsjavascript

var emptyArray = new Array();

var numbers = new Array(1, 2, 3, 4, 5);

```

在第一个示例中，我们创建了一个名为`emptyArray`的空数组。在第二个示例中，我们创建了一个名为`numbers`的数组，包含五个元素：`1`、`2`、`3`、`4` 和 `5`。

# 5.3 访问数组元素

我们可以通过索引来访问数组中的单个元素。索引从`0`开始，表示第一个元素，每个后续元素的索引依次递增`1`。我们使用方括号`[]`并在其中指定索引。以下是一个示例：

```jsjavascript

var fruits = ['apple', 'banana', 'orange'];

console.log(fruits[0]);   // Output: 'apple'

console.log(fruits[1]);   // Output: 'banana'

console.log(fruits[2]);   // Output: 'orange'

```

在这个示例中，我们通过各自的索引访问并打印`fruits`数组中的元素。

# 5.4 修改数组元素

JavaScript中的数组是可变的，这意味着我们可以在创建数组后修改其元素。我们可以使用赋值运算符`=`将新值赋给特定的索引。下面是一个例子：

```jsjavascript

var fruits = ['apple', 'banana', 'orange'];

fruits[1] = 'grape';

console.log(fruits);   // Output: ['apple', 'grape', 'orange']

```

在这个例子中，我们修改`fruits`数组中索引`1`的元素，将其从`'banana'`改为`'grape'`。

# 5.5 数组长度

数组的`length`属性允许我们确定它包含的元素数量。我们可以通过点表示法（`array.length`）访问此属性。下面是一个例子：

```jsjavascript

var fruits = ['apple', 'banana', 'orange'];

console.log(fruits.length);   // Output: 3

```

在这个例子中，我们获取并打印`fruits`数组的长度，它是`3`。

# 5.6 数组方法

JavaScript提供了多种内建的数组方法，可以让我们高效地对数组执行各种操作。让我们来探索一些常用的数组方法：

# 5.6.1 `push()`和`pop()`

`push()`方法将一个或多个元素添加到数组的末尾，而`pop()`方法移除数组的最后一个元素并返回它。下面是一个例子：

```jsjavascript

var fruits = ['apple', 'banana', 'orange'];

fruits.push('grape');

console.log(fruits);       // Output: ['apple', 'banana', 'orange', 'grape']

var removedFruit = fruits.pop();

console.log(fruits);       // Output: ['apple', 'banana', 'orange']

console.log(removedFruit); // Output: 'grape'

```

在这个例子中，我们使用`push()`将元素`'grape'`添加到`fruits`数组的末尾，然后使用`pop()`移除最后一个元素`'grape'`并将其存储在`removedFruit`变量中。

# 5.6.2 `shift()`和`unshift()`

`shift()`方法移除数组中的第一个元素并返回它，而`unshift()`方法将一个或多个元素添加到数组的开头。下面是一个例子：

```jsjavascript

var fruits = ['apple', 'banana', 'orange'];

fruits.shift();

console.log(fruits);       // Output: ['banana', 'orange']

fruits.unshift('grape', 'kiwi');

console.log(fruits);       // Output: ['grape', 'kiwi', 'banana', 'orange']

```

在这个例子中，我们使用`shift()`移除`fruits`数组中的第一个元素`'apple'`，然后使用`unshift()`将元素`'grape'`和`'kiwi'`添加到数组的开头。

# 5.6.3 `slice()`

`slice()`方法提取数组的一部分并返回一个包含选定元素的新数组。它接受两个参数：起始索引（包含）和结束索引（不包含）。下面是一个例子：

```jsjavascript

var fruits = ['apple', 'banana', 'orange', 'grape', 'kiwi'];

var slicedFruits = fruits.slice(1, 4);

console.log(slicedFruits);   // Output: ['banana', 'orange', 'grape']

```

在这个例子中，我们使用`slice(1, 4)`从`fruits`数组中提取从索引`1`（包含）到索引`4`（不包含）之间的元素。

# 5.6.4 `concat()`

`concat()` 方法将两个或多个数组合并，并返回一个新的数组。它不会修改原始数组。以下是一个示例：

```jsjavascript

var fruits = ['apple', 'banana'];

var moreFruits = ['orange', 'grape', 'kiwi'];

var combinedFruits = fruits.concat(moreFruits);

console.log(combinedFruits);   // Output: ['apple', 'banana', 'orange', 'grape', 'kiwi']

```

在这个示例中，我们使用 `concat()` 方法将 `fruits` 数组与 `moreFruits` 数组合并，并将结果存储在 `combinedFruits` 变量中。

5.7 结论

在本章中，我们探讨了 JavaScript 数组，这是一种强大的数据结构，可以让我们存储和操作元素集合。我们学习了如何使用数组字面量和 `Array` 构造函数创建数组，如何访问和修改数组元素，如何获取数组的长度，以及如何使用各种数组方法，如 `push()`、`pop()` 和 `slice()`。数组提供了一种灵活且高效的方式来处理 JavaScript 中的数据集合。

在下一章中，我们将深入探讨 JavaScript 对象，这是该语言中的另一个重要概念。对象让我们能够表示复杂的数据结构，并将相关数据组织成键值对。准备好探索 JavaScript 对象的世界，解锁它们的全部潜力吧！
