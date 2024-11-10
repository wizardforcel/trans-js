# # 第五章：对象与原型

在第四章中，我们探讨了函数和作用域，这是 JavaScript 编程的基本构建块。现在，我们将深入研究对象和原型，这是 JavaScript 的另一个基础概念。对象允许我们将相关数据和函数组织在一起，提供了一种更加有序的方式来表示现实世界中的实体。原型支持对象继承，促进了代码的重用并保持清晰的结构。理解对象和原型对于成为一名熟练的 JavaScript 开发者至关重要。让我们深入了解对象和原型的世界吧！

## 对象：将数据和函数捆绑在一起

在 JavaScript 中，对象是复合数据类型，允许我们表示具有属性（数据）和与之关联的方法（函数）的实体。对象提供了一种出色的方式来将相关数据和行为组织在一起，使代码更加结构化和易读。

### 对象字面量：

创建对象的最简单方法是使用对象字面量，用大括号 `{}` 表示。

```jsjavascript

// Example 1: Object literal

const person = {

name: "John Doe",

age: 30,

occupation: "Software Engineer",

greet: function() {

console.log("Hello, I am " + this.name);

}

};

```

在示例 1 中，我们定义了一个 `person` 对象，具有 `name`、`age` 和 `occupation` 属性，并且包含一个方法 `greet()` 用于打印问候语。

### 访问对象属性：

我们可以使用点符号或方括号符号访问对象属性。

```jsjavascript

// Example 2: Accessing object properties

console.log(person.name); // Output: "John Doe"

console.log(person["age"]); // Output: 30

```

在示例 2 中，我们使用点符号访问 `name` 属性，并使用方括号符号访问 `age` 属性。

### 添加和修改对象属性：

我们可以在运行时向对象添加新属性或修改现有属性。

```jsjavascript

// Example 3: Adding and modifying object properties

person.location = "New York";

person.age = 31;

console.log(person); // Output: { name: 'John Doe', age: 31, occupation: 'Software Engineer', greet: [Function] }

```

在示例 3 中，我们添加了 `location` 属性并修改了 `person` 对象的 `age` 属性。

### 对象方法：

对象也可以包含方法，即与对象关联的函数。

```jsjavascript

// Example 4: Object methods

person.sayHello = function() {

console.log("Hello, I am " + this.name);

};

person.sayHello(); // Output: "Hello, I am John Doe"

```

在示例 4 中，我们向 `person` 对象添加了一个新的方法 `sayHello()` 并调用它来打印问候语。

## 原型：继承和共享行为

原型在 JavaScript 面向对象特性中起着重要作用。它们允许对象从其他对象继承属性和方法，从而实现代码的重用和清晰的继承结构。

### 原型链：

JavaScript 中的每个对象都有一个原型，原型是另一个对象，从中继承属性和方法。这形成了一个原型链，称为原型链。

```jsjavascript

// Example 5: Prototype chain

const parent = {

parentProp: "I am from parent"

};

const child = {

childProp: "I am from child"

};

Object.setPrototypeOf(child, parent);

console.log(child.childProp); // Output: "I am from child"

console.log(child.parentProp); // Output: "I am from parent"

```

在示例 5 中，我们创建了两个对象，`parent` 和 `child`。通过使用 `Object.setPrototypeOf()`，我们将 `child` 的原型设置为 `parent`，从而形成了原型链。现在，`child` 可以访问 `parent` 的属性。

### `__proto__` 属性：

JavaScript 中的每个对象都有一个 `__proto__` 属性，该属性指向其原型。

```jsjavascript

// Example 6: The __proto__ property

const parent = {

parentProp: "I am from parent"

};

const child = {

childProp: "I am from child"

};

child.__proto__ = parent;

console.log(child.childProp); // Output: "I am from child"

console.log(child.parentProp); // Output: "I am from parent"

```

在示例 6 中，我们将 `child` 的 `__proto__` 属性设置为 `parent`，从而创建了原型链。

### 使用原型创建对象：

我们可以通过构造函数或类来创建具有共享原型的对象。

```jsjavascript

// Example 7: Creating objects with prototypes (using constructors)

function Person(name, age) {

this.name = name;

this.age = age;

}

Person.prototype.sayHello = function() {

console.log("Hello, I am " + this.name);

};

const john = new Person("John Doe", 30);

john.sayHello(); // Output: "Hello, I am John Doe"

```

在示例 7 中，我们定义了一个构造函数 `Person` 来创建 `Person` 对象。我们向 `Person` 的原型添加了一个方法 `sayHello()`，所有 `Person` 对象都可以访问该方法。

### ES6 类：

随着 ES6 的引入，JavaScript 提供了一种更直观的方法，使用类来创建具有共享原型的对象。

```jsjavascript

// Example 8: Creating objects with prototypes (using classes)

class Animal {

constructor(name) {

this.name = name;

}

makeSound() {

console.log(this.name + " makes a sound");

}

}

const cat = new Animal("Cat");

cat.makeSound(); // Output: "Cat makes a sound"

```

在示例 8 中，我们定义了一个类 `Animal`，它有一个构造函数和一个方法 `makeSound()`。然后，我们基于这个类创建了一个对象 `cat`。

### 使用原型的继承：

我们可以通过将一个对象的原型设置为另一个对象，从而实现继承，建立父子关系。

```jsjavascript

// Example 9: Inheritance with prototypes

function Shape() {}

Shape.prototype.draw = function() {

return "Drawing a shape";

};

function Circle(radius) {

this.radius = radius;

}

Circle.prototype = Object.create(Shape.prototype);

Circle.prototype.constructor = Circle;

Circle.prototype.draw = function() {

return "Drawing a circle with radius " + this.radius;

};

const circle = new Circle(5);

console.log(circle.draw()); // Output: "Drawing a circle with radius 5"

```

在示例 9 中，我们创建了一个 `Shape` 构造函数和一个 `Circle` 构造函数。我们将 `Circle` 的原型设置为 `Shape` 的实例，从而建立了继承关系。然后，我们重写了 `Circle` 原型的 `draw()` 方法。

## 结论：

在本章中，我们探讨了 JavaScript 中的对象和原型。对象使我们能够将相关数据和函数捆绑在一起，提供了一种更结构化的方式来表示代码中的实体。我们学习了如何使用对象字面量创建对象，添加属性和方法，并访问它们。此外，我们还研究了原型，它使对象继承成为可能，允许对象共享行为和属性，从而提高代码的可重用性。

理解对象和原型是掌握 JavaScript 面向对象功能的关键。通过对象，我们可以高效地组织数据和行为，而原型则使我们能够建立清晰的继承关系，并在对象之间共享代码。
