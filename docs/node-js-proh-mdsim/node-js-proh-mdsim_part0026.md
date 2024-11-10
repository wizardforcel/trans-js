# 第6章：JavaScript 对象

在第5章中，我们探讨了 JavaScript 数组，它使我们能够存储和操作元素集合。现在，让我们深入了解 JavaScript 对象，这是该语言中的另一个基本概念。对象使我们能够表示复杂的数据结构，并将相关数据组织成键值对。

# 6.1 对象简介

在 JavaScript 中，对象是一种复合数据类型，它允许我们以结构化的方式存储和操作数据。对象是由多个属性组成的集合，每个属性包含一个键和值。键用于标识并访问对应的值。对象通常用来表示现实世界中的实体，例如一个人、一辆车或一本书。

# 6.2 创建对象

在 JavaScript 中，有多种方法可以创建对象。一种常见的方式是使用对象字面量，我们在花括号`{}`中定义属性及其值。以下是一个示例：

```jsjavascript

var person = {

name: "John Doe",

age: 30,

profession: "Web Developer"

};

```

在这个示例中，我们创建了一个名为`person`的对象，包含三个属性：`name`、`age`和`profession`。属性名称作为键，后跟冒号`:`，并指定对应的值。

创建对象的另一种方法是使用`new`关键字和`Object()`构造函数。以下是一个示例：

```jsjavascript

var car = new Object();

car.make = "Toyota";

car.model = "Camry";

car.year = 2022;

```

在这个示例中，我们使用`Object()`构造函数创建一个名为`car`的对象，并使用点表示法为其分配属性。

# 6.3 访问对象属性

我们可以使用点表示法或方括号表示法来访问对象的属性。点表示法涉及使用对象名称后跟一个点`.`和属性名称。以下是一个示例：

```jsjavascript

console.log(person.name);     // Output: "John Doe"

console.log(car.make);        // Output: "Toyota"

```

在这个示例中，我们使用点表示法访问`person`对象的`name`属性和`car`对象的`make`属性。

方括号表示法涉及使用方括号`[]`并将属性名称指定为字符串。以下是一个示例：

```jsjavascript

console.log(person['age']);    // Output: 30

console.log(car['year']);      // Output: 2022

```

在这个示例中，我们使用括号符号访问`person`对象的`age`属性和`car`对象的`year`属性。

# 6.4 修改对象属性

JavaScript中的对象是可变的，这意味着我们可以在创建后修改它们的属性。我们可以使用点符号或括号符号重新赋值给一个属性。以下是一个示例：

```jsjavascript

person.age = 35;

car['year'] = 2023;

```

在这个示例中，我们修改了`person`对象的`age`属性和`car`对象的`year`属性。

# 6.5 添加和删除对象属性

我们可以通过简单地为一个之前不存在的属性赋值来向对象添加新的属性。类似地，我们可以使用`delete`关键字删除属性。以下是一个示例：

```jsjavascript

person.gender = "Male";

delete car.model;

```

在这个示例中，我们向`person`对象添加了`gender`属性，并从`car`对象中删除了`model`属性。

# 6.6 对象方法

除了属性，JavaScript中的对象还可以包含方法。方法是与对象相关联的函数，可以通过点符号调用。

JavaScript中的方法是与对象关联的函数，可以使用对象的属性执行操作或计算。让我们看一个示例：

```jsjavascript

var calculator = {

add: function (a, b) {

return a + b;

},

subtract: function (a, b) {

return a - b;

}

};

console.log(calculator.add(5, 3));       // Output: 8

console.log(calculator.subtract(10, 4)); // Output: 6

```

在这个示例中，我们创建了一个名为`calculator`的对象，包含两个方法：`add`和`subtract`。这些方法可以通过点符号调用，后跟括号`()`，并传入所需的参数。

# 6.7 对象遍历

我们可以使用多种技术遍历对象的属性。一种常见的方法是使用`for...in`循环，它允许我们遍历对象的可枚举属性。以下是一个示例：

```jsjavascript

for (var key in person) {

console.log(key + ": " + person[key]);

}

```

在这个示例中，我们遍历`person`对象的属性，并记录下属性名（`key`）及其对应的值（`person[key]`）。

# 6.8 对象原型和继承

JavaScript 是一种基于原型的语言，这意味着对象可以从其他对象继承属性和方法。这个概念被称为继承。对象可以有一个原型对象，它作为它继承的属性和方法的蓝图。

在 JavaScript 中，继承是通过原型链实现的。对象具有一个内部的`[[Prototype]]`属性，指向它们的原型对象。如果在对象中找不到某个属性或方法，JavaScript 会在对象的原型中查找。这个链条会继续，直到找到该属性或方法，或者直到原型链的末尾。

6.9 结论

在本章中，我们探讨了 JavaScript 对象，这是该语言中的一个核心概念。对象使我们能够表示复杂的数据结构，使用键值对组织相关数据，并定义执行数据操作的方法。我们学习了如何使用对象字面量和`Object()`构造函数创建对象，如何通过点符号和括号符号访问和修改对象属性，如何添加和删除属性，定义对象方法，并使用 `for...in` 循环遍历对象属性。

在下一章，我们将深入探讨 JavaScript 事件和事件处理，了解如何响应用户交互并创建动态互动的 Web 应用程序。准备好提升你 JavaScript 程序的交互性吧！
