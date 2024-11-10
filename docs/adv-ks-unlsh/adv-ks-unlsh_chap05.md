## 原型

`Inheritance`是一个通用的面向对象编程概念，允许对象继承其他对象的方法和属性。这减少了代码重复并促进了不同对象之间的代码共享。

与传统的面向对象编程语言（如Java或C#）不同，JavaScript处理继承的方式不同。JavaScript中的对象是`linked`到其他对象，这种链接允许一个对象使用其所链接的另一个对象的功能。

JavaScript中对象之间的链接形成了一条链。这条链被称为“`prototype chain`”。可以想象一下作用域链，每个作用域都链接到另一个作用域，直到我们达到全局作用域。原型链类似：一个对象链接到另一个对象。这个其他对象又链接到另一个对象，形成对象之间的链。

原型链允许对象之间共享属性，这就是JavaScript中的继承概念，称为“`prototypal inheritance`”。在原型继承中，从其他对象继承属性的对象称为这些对象的“`prototype`”。

当我们在JavaScript中创建一个对象字面量时，它默认链接到内置的`Object.prototype`对象。

```js
1 const obj = {};

```

在上面的代码示例中，`Object.prototype`对象是`obj`对象的`prototype`。

### 对象是如何链接的？

JavaScript中的对象有一个隐藏的内部槽`[[Prototype]]`。当一个对象被创建时，它通过将另一个对象的引用保存到新创建对象的`[[Prototype]]`内部槽中，与另一个对象链接。保存于内部槽中的其他对象将作为新创建对象的“原型”。

在上面的代码示例中，`obj`对象的`[[Prototype]]`槽包含对`Object.prototype`对象的引用。因此，`obj.[[Prototype]]`给我们提供了`obj`对象的原型，即`obj`所链接并继承属性的对象。但由于`[[Prototype]]`是JavaScript无法访问的内部槽，稍后在本课程中，我们将看到如何访问任何对象的原型。

### “`prototype`”属性

在我们对原型继承的讨论中，你可能注意到“`prototype`”这个术语在两个不同的上下文中使用：一个作为属性，即`Object.prototype`，另一个作为用于描述与另一个对象共享属性的对象的通用术语。这些名称的冲突在许多人刚开始学习JavaScript中的原型继承时造成了混淆。

由于函数在JavaScript中也是对象，因此它们可以像任何其他对象一样拥有属性。属性名称“`prototype`”是函数的属性之一。箭头函数没有这个属性。

函数的`prototype`属性指向一个对象，该对象在使用“new”关键字作为“构造函数”调用该函数时用作其他对象的“原型”。这里，`prototype`这个术语在两个上下文中使用：

+   函数上的`prototype`属性

+   当一个对象与其他对象链接并共享其属性时，它被称为“原型”。

以下代码示例显示了名为“prototype”的属性存在于函数上：

```js
1 function Car(name, model) {
2   this.name = name;
3   this.model = model;
4 }
5 
6 console.log(Object.getOwnPropertyNames(Car));
7 
8 // [ "prototype", "length", "name" ]

```

你可以在下面的Replit中运行上述代码：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/prototypal-inheritance-example1” />`

你可能能从上面的代码中看出，`Car`函数意图作为构造函数使用。然而，它实际上只是一个普通函数。`prototype`属性只有在我们将函数作为构造函数调用时才有用，即使用`new`关键字。

任何添加到`Car.prototype`对象的属性将由从`Car`构造函数创建的所有实例共享。`Car.prototype`函数将作为所有`Car`构造函数实例的“原型”。

最初，任何函数的`prototype`属性指向的对象仅包含一个名为“constructor”的属性。这个“constructor”属性的值是对构造函数的引用。在`Car.prototype`对象的情况下，`Car.prototype.constructor`指向`Car`构造函数。

```js
1 // Car.prototype
2 {
3   constructor: <Car function>
4 }

```

以下代码示例验证了`Car.prototype.constructor`指向`Car`函数：

```js
1 function Car(name, model) {
2   this.name = name;
3   this.model = model;
4 }
5 
6 console.log(Car.prototype.constructor === Car); // true

```

你可以在下面的Replit中运行上述代码：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/prototypal-inheritance-example2” />`

:::note

[`constructor`属性](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/constructor)在我们编写的JavaScript代码中很少使用，如果有的话。

:::

让我们在 `Car.prototype` 对象上添加一个属性：

```js
1 Car.prototype.start = function () {
2   console.log("starting the engine of " + this.name);
3 };
4 
5 const honda = new Car("honda", "1996");
6 const toyota = new Car("toyota", "2000");
7 
8 honda.start(); // starting the engine of honda
9 toyota.start(); // starting the engine of toyota

```

你可以在下面的 Replit 中运行以上代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/prototypal-inheritance-example3" />`

当一个函数使用 `new` 关键字被调用时，创建新对象的步骤之一是将新创建对象的 `[[Prototype]]` 内部插槽指向函数的 `prototype` 属性所引用的对象。因此，新创建的对象可以访问构造函数的 `prototype` 属性所引用的对象上定义的属性。

### 获取任何对象的原型

`Object` 函数有一个静态方法名为 [`getPrototypeOf`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/getPrototypeOf)，可以用来获取任何对象的原型。它返回对象的内部 `[[Prototype]]` 属性的值。

对于在前一个代码示例中创建的 `honda` 对象，`Object.getPrototypeOf` 函数返回 `Car.prototype` 对象，因为 `Car.prototype` 对象是所有 `Car` 构造函数实例的原型。

```js
 1 function Car(name, model) {
 2  this.name = name;
 3  this.model = model;
 4 }
 5 
 6 Car.prototype.start = function () {
 7  console.log("starting the engine of " + this.name);
 8 };
 9 
10 const honda = new Car("honda", "1996");
11 
12 console.log(Object.getPrototypeOf(honda) === Car.prototype); // true

```

你可以在下面的 `Replit` 中运行以上代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/prototypal-inheritance-example4" />`

现在我们知道什么是原型继承，让我们探索原型链。

### `Object.prototype` - 所有对象的父级

在原型继承层次结构的顶部是 `Object.prototype` 对象。它是所有对象的根对象或父对象。当我们创建一个对象字面量时，它的原型是 `Object.prototype` 对象。

```js
1 const obj = {};
2 
3 console.log(Object.getPrototypeOf(obj) === Object.prototype);
4 // true

```

你可以在下面的 `Replit` 中运行以上代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/prototype-chain-example1" />`

我们没有在 `obj` 对象上定义任何属性。但我们仍然可以调用一些方法。

```js
1 const obj = {};
2 
3 console.log(obj.toString()); // [object Object]

```

你可以在下面的 `Replit` 中运行以上代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/prototype-chain-example2" />`

我们没有在 `obj` 对象上定义一个名为 `toString` 的方法；它是如何在上面的代码示例中可访问的？你猜对了：它是在 `Object.prototype` 对象上定义的，并且由于 `Object.prototype` 是 `obj` 的原型，因此在 `Object.prototype` 上定义的属性会被 `obj` 继承，其中 `toString` 就是其中之一。

以这种方式创建的对象是 `Object` 构造函数的实例。我们也可以如下定义 `obj`：

```js
1 const obj = new Object();

```

这有相同的效果：它创建一个空对象。正如前一课中讨论的那样，函数有一个指向对象的原型属性，当该函数作为“构造函数”调用时，该对象充当所有实例的“原型”。因此，`Object.prototype` 对象作为通过 `new Object()` 或对象字面量表示法创建的所有对象的“原型”。

在这一点上，你可能会问：`toString`不是可以在所有对象上调用吗？是的，可以；一些对象从`Object.prototype`对象继承它，而其他对象，例如数组，则从它们的原型继承，即`Array.prototype`对象，这覆盖了在`Object.prototype`中定义的`toString`实现。

一些对象直接链接到`Object.prototype`对象，而另一些则间接链接。例如，数组是间接链接的。每个数组实例直接链接到`Array.prototype`对象，而`Array.prototype`对象又链接到`Object.prototype`对象。这形成了一条以`Object.prototype`对象为终点的原型链。

```js
1 const arrayPrototype = Object.getPrototypeOf([]);
2 const prototypeOfArrayPrototype = Object.getPrototypeOf(arrayPrototype);
3 
4 console.log(arrayPrototype === Array.prototype);
5 // true
6 console.log(prototypeOfArrayPrototype === Object.prototype);
7 // true

```

你可以在下面的`Replit`中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/prototype-chain-example3" />`

上述代码演示的原型链可以在下面的图像中可视化：

![array prototype chain](images/module_06----lesson_06.02----public----assets----prototype-chain-array.png)

数组原型链

`Array.prototype`对象包含可以在每个数组上调用的方法，例如`map`、`filter`等。`Object.prototype`对象包含所有对象可用的方法，例如`toString`方法。

就像JavaScript遍历作用域链以查找当前作用域中无法找到的标识符的声明一样，JavaScript遍历原型链以查找当前对象中无法找到的属性。原型链必须在某处结束。否则，JavaScript将继续遍历一个无尽的链；它在`Object.prototype`对象处结束。访问`Object.prototype`的原型返回`null`。

```js
1 console.log(Object.getPrototypeOf(Object.prototype));
2 // null

```

你可以在下面的Replit中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/prototype-chain-example4" />`

字符串的原型链类似于数组的原型链，只是用`String.prototype`对象代替了`Array.prototype`对象，后者作为所有字符串实例的原型。这个`String.prototype`对象又链接到`Object.prototype`对象，而`Object.prototype`对象作为`String.prototype`对象的原型。

### “Function”函数

尽管听起来令人困惑，但确实有一个名为[Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function)的函数。JavaScript中的函数是对象，并且是这个“Function”构造函数的实例。`Function.prototype`对象提供所有函数可访问的属性；例如，像`bind`、`apply`等方法。

`Function.prototype`对象作为函数的原型，包括`Object`函数。即使是`Function`函数，`Function.prototype`对象所属的函数，也继承自`Function.prototype`对象的属性，因为`Function`毕竟只是一个函数。因此，让它继承自`Function.prototype`对象是有意义的，这个对象包含了函数的公共属性。

```js
1 console.log(Object.getPrototypeOf(Object) == Function.prototype);
2 // true
3 
4 console.log(Object.getPrototypeOf(Function) == Function.prototype);
5 // true

```

你可以在下面的Replit中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/prototype-chain-example5" />`

上述描述的原型链可以在以下图像中可视化：

![array prototype chain](images/module_06----lesson_06.02----public----assets----function-prototype-chain.png)

数组原型链

由于`Object.prototype`对象是根或父对象，它是原型链的一部分，直接链接到`Function.prototype`对象。

`__proto__`属性被定义在`Object.prototype`对象上。它是一个getter和setter，用于返回或设置对象的原型。换句话说，它返回或设置对象的内部`[[Prototype]]`属性的值。

尽管可以使用此属性来设置和获取对象的原型，但不鼓励这样做。此属性已被弃用，并提供了更好的替代方案来获取和设置对象的原型。

```js
1 const user = { name: "John Doe" };
2 
3 console.log(user.__proto__);
4 // logs Object.prototype object

```

你可以在下面的Replit中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/proto-property-example1" />`

上面的代码示例展示了如何将`__proto__` 属性用作`getter`来获取`user`对象的原型。它也可以用作`setter`来设置对象的`[[Prototype]]`内部属性的值。同样，使用它是不被鼓励的，还有更好的替代方案。我们可以使用[`setPrototypeOf`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/setPrototypeOf) 方法来设置原型。

上述代码示例中`user`对象的原型是`Object.prototype`对象。因此，`user`对象可以访问`__proto__` 属性。作为`__proto__` 属性，当用作getter时，仅仅暴露了对象内部`[[Prototype]]` 属性的值；在`user`的情况下，它返回`Object.prototype`对象。

### `__proto__` 的问题

避免使用`__proto__` 属性来获取或设置对象原型的理由有多个。

如前所述，`__proto__` 属性已经被弃用，存在更好的替代方案来设置和获取对象的原型。这个属性直到2015年才被标准化，因此在此之前，它作为JavaScript语言的非标准特性存在。尽管`__proto__` 属性现在是ECMAScript规范的一部分，但该属性并不是为了推广或鼓励其使用而被ECMAScript规范标准化；相反，它之所以被标准化是因为它已经在多个浏览器中运行的JavaScript引擎中存在。

`__proto__` 属性的另一个问题是它可能并不适用于所有对象。你可能会问这怎么可能。难道所有对象不直接或间接继承自`Object.prototype`对象吗？它可能不可用的原因是，我们可以创建不继承任何其他对象的对象（我们将在下一节讨论这一点）。

到目前为止，我们已经看到内置对象，如`Object.prototype`，自动被设置为对象的原型。我们如何将自己的对象用作其他对象的原型呢？例如，我们有以下对象，希望将其用作某个其他对象的原型：

```js
1 const propertyPrinter = {
2   printOwnPropertyNames: function () {
3     // "this" refers to the object on which
4     // this function is called
5     for (let prop of Object.getOwnPropertyNames(this)) {
6       console.log(prop);
7     }
8   }
9 };

```

我们如何将这个对象用作另一个对象的原型？我们可以使用`setPrototypeOf` 方法：

```js
 1 const propertyPrinter = {
 2  printOwnPropertyNames: function () {
 3    // "this" refers to the object on which
 4    // this function is called
 5    for (let prop of Object.getOwnPropertyNames(this)) {
 6      console.log(prop);
 7    }
 8  }
 9 };
10 
11 const user = {
12   firstName: "John",
13   lastName: "Doe",
14   age: 25
15 };
16 
17 // set the prototype of the "user" object
18 Object.setPrototypeOf(user, propertyPrinter);
19 
20 // prototype methods are now accessible
21 user.printOwnPropertyNames();
22 // firstName
23 // lastName
24 // age

```

你可以在下面的Replit中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/Custom-prototypes-example2" />`

被弃用的`__proto__` 属性也可以用于实现相同的结果，但由于它已被弃用，我们将讨论另一种显式设置对象原型的选项。

### `Object.create` 方法

`Object.create`方法用于创建一个新对象，其原型为作为第一个参数传入的另一个对象。此方法让我们可以显式设置对象的原型。上面的代码示例可以用`Object.create`重写，如下所示：

```js
 1 // create a new object and set "propertyPrinter"
 2 // object as its prototype
 3 const user = Object.create(propertyPrinter);
 4 
 5 user.firstName = "John";
 6 user.lastName = "Doe";
 7 user.age = 25;
 8 
 9 // prototype methods are accessible
10 user.printOwnPropertyNames();
11 // firstName
12 // lastName
13 // age

```

你可以在下面的Replit中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/Custom-prototypes-example3" />`

### 空原型对象

所有对象最终都继承自`Object.prototype`对象，因为它位于原型链的顶部，是所有对象的父对象。然而，我们可以创建不从任何对象继承属性的对象。我们只需将`null`作为内部`[[Prototype]]`属性的值，使用上述讨论的方法设置即可。

```js
1 const obj = Object.create(null);
2 
3 console.log(obj.toString());
4 // Error: toString not defined

```

你可以在下面的Replit中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/Custom-prototypes-example4" />`

上述示例中的`obj`对象没有原型。如果其原型没有显式设置为`null`，其原型将是`Object.prototype`对象，它将继承`toString`方法，但正如上面的代码示例所示，`obj`并没有访问`toString`方法的权限。

`null`原型对象可能看起来毫无用处，但在某些情况下却非常有用。例如，这些对象可以防止诸如[原型污染](https://learn.snyk.io/lessons/prototype-pollution/javascript/)攻击，这种攻击可能会向对象的原型链添加一些属性，从而改变代码执行的正常流程。

考虑以下简化的示例：

```js
1 const user = {};
2 
3 // malicious code adding "isAdmin"
4 // property in the prototype object
5 Object.prototype.isAdmin = true;
6 
7 if (user.isAdmin) {
8   console.log("grant access");
9 }

```

你可以在下面的Replit中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/Custom-prototypes-example5" />`

如果`user`对象的原型是`null`，恶意代码将不会对我们的代码产生影响。

```js
 1 const user = Object.create(null);
 2 
 3 // malicious code adding "isAdmin"
 4 // property in the prototype object
 5 Object.prototype.isAdmin = true;
 6 
 7 if (user.isAdmin) {
 8  console.log("grant access");
 9 } else {
10   console.log("access denied");
11 }

```

你可以在下面的Replit中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/Custom-prototypes-example6" />`

在像`Java`或`C#`这样的传统面向对象语言中，我们可以扩展或继承一个类来重用其功能。扩展一个类会创建父子关系，其中子类扩展父类。这促进了代码的重用性。

直到2015年，JavaScript才没有类。相反，使用构造函数。要从构造函数继承，JavaScript开发人员显式地通过使用`Object.create`方法创建两个不同构造函数的原型属性之间的链接。以下代码示例展示了一个构造函数如何扩展另一个构造函数以重用某些功能：

```js
 1 function Person(name, age) {
 2  this.name = name;
 3  this.age = age;
 4 }
 5 
 6 Person.prototype.introduce = function () {
 7  console.log(`My name is ${this.name} and I am ${this.age} years old`);
 8 };
 9 
10 function Student(name, age, id) {
11   // delegate the responsibility of initializing
12   // "name" and "age" properties to the Person
13   // constructor
14   Person.call(this, name, age);
15   this.id = id;
16 }
17 
18 // set "Person.prototype" object as the prototype
19 // of the "Student.prototype" object
20 Student.prototype = Object.create(Person.prototype);
21 
22 // set the constructor property on the
23 // newly created Student.prototype object
24 Student.prototype.constructor = Student;
25 
26 const mike = new Student("Mike", 20, 222);
27 mike.introduce();

```

这是一个Replit嵌入，用于运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/ES6-classes-and-prototypes-example1" />`

在上面的代码示例中，有以下三点值得注意：

+   `Person.call(...)`在`Student`构造函数内部被调用，以*委托*将`name`和`age`属性的添加和初始化的责任交给新创建的`Student`实例或对象。

+   `Object.create`用于创建`Student.prototype`对象，并将`Person.prototype`设置为新创建对象的原型。

+   通常，函数的“prototype”属性所指的对象具有一个指向该函数的`constructor`属性。由于由`Object.create`方法创建的对象没有`constructor`属性，因此我们显式地将`constructor`属性添加到新创建的`Student.prototype`对象。

`Student.prototype`对象与`Person.prototype`对象之间的链接允许`Student`的实例使用在`Person.prototype`对象上定义的属性。

下图有助于可视化我们的代码示例创建的原型链：

![构造函数原型链](images/module_06----lesson_06.05----public----assets----constructor-function-prototype-chain.png)

构造函数原型链

尽管上述代码有效，但由于在两个构造函数之间正确设置原型链接需要多个步骤，这使得代码容易出错。想象一下，如果有多个构造函数需要这样链接，很容易忘记设置原型链接所需的任何步骤。理想情况下，我们希望有一种更声明式的方法来实现相同的结果。一种声明式解决方案将允许我们在不显式创建`Student.prototype`和`Person.prototype`对象之间的链接的情况下获得相同的结果。

### ES2015类

从2015年起，JavaScript引入了类。它们提供了一种更不易出错的声明式编写代码的方法。类带有[`extends`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/extends)关键字，有助于在类之间创建父子关系。上述代码示例可以使用类重写，如下所示：

```js
 1 class Person {
 2  constructor(name, age) {
 3    this.name = name;
 4    this.age = age;
 5  }
 6 
 7  introduce() {
 8    console.log(`My name is ${this.name} and I am ${this.age} years old`);
 9  }
10 }
11 
12 class Student extends Person {
13   constructor(name, age, id) {
14     // delegate the responsibility of initializing
15     // "name" and "age" properties to the parent class
16     super(name, age);
17     this.id = id;
18   }
19 }

```

上述代码给出的结果与构造函数的结果相同。它也创建了相同的原型链接。我们可以通过以下比较来验证这一点：

```js
1 console.log(Object.getPrototypeOf(mike) === Student.prototype);
2 // true
3 console.log(Object.getPrototypeOf(Student.prototype) === Person.prototype);
4 // true
5 console.log(Object.getPrototypeOf(Person.prototype) === Object.prototype);
6 // true

```

这里需要提到的一件重要事情是，类仅仅是传统构造函数的语法糖。在底层，我们仍在使用构造函数，但类允许我们以更声明的方式编写代码。

`extends`关键字做的另一件事是，除了在`Student.prototype`和`Person.prototype`对象之间设置链接外，它还链接构造函数。它通过将`Person`类设置为`Student`类的原型来实现这一点。以下代码验证了`extends`关键字为我们在幕后设置的第二个原型链。

```js
1 console.log(Object.getPrototypeOf(Student) === Person);
2 // true

```

`extends`关键字设置的两个原型链服务于两个不同的目的：

+   ``Student.prototype ---> Person.prototype``允许继承实例属性。

+   ``Student ---> Person``允许继承静态属性。
