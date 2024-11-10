## 迭代器与生成器

像数组这样的内置对象可以使用`[for…of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)`循环进行迭代。与其使用简单的`for`循环逐个访问数组值、在每次迭代后递增索引，并且还要知道何时结束迭代以避免访问超出边界的索引，使用`for...of`循环，所有这一切都为我们处理好了。我们无需担心索引或循环终止条件。

```js
1 const arr = [1, 2, 3];
2 
3 for (const num of arr) {
4   console.log(num);
5 }

```

这是一个Replit，您可以在其中运行上述代码：

<ReplitEmbed src=”https://replit.com/@newlineauthors/iterators-example1” />

`for...of`循环如何帮助我们迭代数组？它如何知道何时结束迭代？

要理解这一点，我们需要了解以下两个概念：

+   可迭代对象

+   迭代器

### 可迭代对象

可迭代对象是实现了[可迭代协议](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#the_iterable_protocol)的对象。根据可迭代协议，如果一个对象定义了可以被`for...of`循环用于迭代该对象中值的迭代行为，那么该对象就是可迭代的。该对象可以实现一个由`[Symbol.iterator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol/iterator)`表示的属性所引用的方法；这是定义迭代行为的众所周知的符号之一。众所周知的符号在与符号相关的模块中讨论过。

在数组的情况下，这个方法在`Array.prototype`对象中定义。这个方法定义了适合数组的迭代行为。其他对象也可以实现这个方法，以定义适合它们的迭代行为。

`Symbol.iterator`返回什么可以被像`for...of`循环这样的构造用于迭代一个对象？它返回一个迭代器对象。

### 迭代器

迭代器是实现了[迭代器协议](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#the_iterator_protocol)的对象。根据迭代器协议，如果一个对象实现了一个名为`next`的方法，该方法接受零个或一个参数，并返回一个具有以下属性的对象，那么该对象就是一个迭代器：

+   `done`：指示迭代器是否可以生成或返回另一个值。如果可以，其值为`false`，否则为`true`。`true`值等同于在`next`方法返回的对象中省略此属性。

+   `value`：迭代器对象返回的值。如果`done`属性的值为`true`，此属性可以省略或其值可以为`undefined`。

以下是具有上述属性的迭代器对象的示例：

```js
1 { value: 45, done: false }
2 
3 // or
4 
5 { value: undefined, done: true }

```

当我们使用``for...of``循环迭代数组时，它会在内部从数组获取迭代器，并持续调用其``next``方法，直到迭代器返回所有值。使用``for...of``循环时，我们间接使用了迭代器。我们也可以直接使用迭代器。数组是可迭代的，我们知道可迭代对象实现了返回包含``next``方法的迭代器对象的``Symbol.iterator``方法。以下代码示例展示了我们如何获取数组迭代器并直接使用它来获取数组中的值：

```js
 1 const arr = [2, 4, 6, 8, 10];
 2 
 3 // get the array iterator object
 4 const arrayIterator = arr[Symbol.iterator]();
 5 
 6 // get the first iterator result object
 7 let result = arrayIterator.next();
 8 
 9 // keep getting new iterator result objects
10 // until the "done" property of the iterator
11 // result object is false
12 while (!result.done) {
13   console.log(result.value);
14   result = arrayIterator.next();
15 }
16 
17 /*
18 2
19 4
20 6
21 8
22 10
23 */

```

这是一个您可以运行上述代码的Replit：

<ReplitEmbed src=”https://replit.com/@newlineauthors/iterators-example2” />

每个[内置迭代器对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Iterator#description)提供定义可迭代对象特定迭代行为的迭代器。以下是直接使用``Map``对象的迭代器的示例：

```js
 1 const myMap = new Map();
 2 myMap.set("a", 1);
 3 myMap.set("b", 2);
 4 myMap.set("c", 3);
 5 
 6 // get the array iterator object
 7 const mapIterator = myMap[Symbol.iterator]();
 8 
 9 // get the first iterator result object
10 let result = mapIterator.next();
11 
12 // keep getting new iterator result objects
13 // until the "done" property of the iterator
14 // result object is false
15 while (!result.done) {
16   console.log(result.value);
17   result = mapIterator.next();
18 }
19 
20 /*
21 ["a", 1]
22 ["b", 2]
23 ["c", 3]
24 */

```

这是一个您可以运行上述代码的Replit：

<ReplitEmbed src=”https://replit.com/@newlineauthors/iterators-example3” />

对于``Map``对象，迭代器结果对象上的``value``属性的值是包含在数组中的键值对。您可以使用[``Map.prototype.values()``](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map/values)获取一个仅返回``Map``中值的迭代器，或者使用[``Map.prototype.keys()``](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map/keys)获取一个返回``Map``中所有键的迭代器。

### 迭代器原型

每个迭代器对象都继承自相应的迭代器原型对象。例如，数组迭代器从数组迭代器原型对象继承。同样，字符串迭代器从字符串迭代器原型对象继承。所有迭代器原型对象都继承自``Iterator.prototype``对象。

```js
 1 const arr = [2, 4, 6, 8, 10];
 2 
 3 // get the array iterator object
 4 const arrayIterator = arr[Symbol.iterator]();
 5 
 6 // this is the prototype object shared by all array iterators
 7 const arrayIteratorPrototype = Object.getPrototypeOf(arrayIterator);
 8 
 9 console.log(Object.getOwnPropertyNames(arrayIteratorPrototype));
10 // ["next"]

```

这是一个Replit，你可以运行上述代码：

<ReplitEmbed src="https://replit.com/@newlineauthors/iterators-example4" />

上述代码示例展示了一种获取数组迭代器原型对象的方法，它还显示了`next`方法是从数组迭代器原型对象继承的。如果我们获取数组迭代器原型对象的原型，我们将得到``Iterator.prototype``对象，所有迭代器原型对象共享该对象。

```js
 1 const arr = [2, 4, 6, 8, 10];
 2 
 3 // get the array iterator object
 4 const arrayIterator = arr[Symbol.iterator]();
 5 
 6 // this is the prototype object shared by all array iterators
 7 const arrayIteratorPrototype = Object.getPrototypeOf(arrayIterator);
 8 
 9 // this is the Iterator.prototype object shared by all iterator prototypes
10 const iteratorPrototype = Object.getPrototypeOf(arrayIteratorPrototype);

```

:::info 我们无法直接访问``Iterator.prototype``对象，因为它是一个所有内置迭代器继承的隐藏全局对象。

:::

``Iterator.prototype``对象本身就是一个可迭代对象，这意味着它实现了可迭代协议。但它实现的``Symbol.iterator``方法仅仅返回调用此方法的迭代器。这意味着任何迭代器对象本身都是可迭代的，意味着我们可以将其与``for...of``循环等构造函数一起使用。

```js
 1 const arr = [1, 2, 3];
 2 
 3 const arrayIterator = arr[Symbol.iterator]();
 4 
 5 // use the array iterator object instead of the array
 6 for (const num of arrayIterator) {
 7  console.log(num);
 8 }
 9 
10 /*
11 1
12 2
13 3
14 */

```

这是一个Replit，你可以运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/iterators-example6" />`

### 创建自定义可迭代对象

到此为止，我们已经了解了足够多关于可迭代对象和迭代器的知识，可以创建自定义可迭代对象。要创建一个自定义可迭代对象，我们需要实现返回包含`next`方法的迭代器对象的`Symbol.iterator`方法。让我们考虑一个学生对象的例子，我们希望使其可迭代，以便可以轻松使用`for...of`循环打印它们的属性。

```js
1 function Student(name, age, id, courses) {
2   this.name = name;
3   this.age = age;
4   this.id = id;
5   this.courses = courses;
6 }

```

这是将用于创建学生对象的`Student`构造函数。为了使所有学生对象可迭代，我们需要在`Student.prototype`对象中实现`Symbol.iterator`方法，如下所示：

```js
 1 Student.prototype[Symbol.iterator] = function () {
 2  // "this" refers to the student object on which this method is called
 3  const currentStudent = this;
 4  const studentProps = Object.getOwnPropertyNames(currentStudent);
 5  let propIndex = 0;
 6 
 7  const studentIterator = {
 8    next: () => {
 9      if (propIndex < studentProps.length) {
10         const key = studentProps[propIndex];
11         const value = currentStudent[key];
12         propIndex++;
13         const formattedValue = `${key.padStart(7)} => ${value}`;
14 
15         return {
16           value: formattedValue,
17           done: false
18         };
19       }
20 
21       return {
22         value: undefined,
23         done: true
24       };
25     }
26   };
27 
28   return studentIterator;
29 };

```

现在，如果我们尝试遍历任何学生实例，我们将得到在学生迭代器的`next`方法中定义的格式化值，如下所示：

```js
 1 const jack = new Student("Jack", 20, "21A", ["Maths", "Biology", "Physics"]);
 2 
 3 for (const val of jack) {
 4  console.log(val);
 5 }
 6 
 7 /*
 8   name => Jack
 9    age => 20
10      id => 21A
11 courses => Maths,Biology,Physics
12 */

```

这是一个Replit，你可以运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/iterators-example9" />`

我们可以根据任何逻辑定义迭代行为，并以我们希望的方式格式化迭代器结果对象中返回的值。这使我们能够灵活地为任何适合特定对象或相关对象组的对象定义迭代行为。

请记住，每个迭代器原型对象，例如数组迭代器原型对象，都是从`Iterator.prototype`对象继承的，但`studentIterator`对象则不是。因此，学生迭代器对象不可迭代。

```js
1 const jack = new Student("Jack", 20, "21A", ["Maths", "Biology", "Physics"]);
2 
3 const studentIterator = jack[Symbol.iterator]();
4 
5 for (const val of studentIterator) {
6   console.log(val);
7 }
8 
9 // ERROR...

```

这是一个Replit，你可以运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/iterators-example10" />`

我们可以通过显式设置`Iterator.prototype`对象与我们的`studentIterator`对象之间的原型链链接来解决这个问题，或者更简单的方法是直接在`studentIterator`对象中实现`Symbol.iterator`方法，使其可迭代：

```js
 1 Student.prototype[Symbol.iterator] = function () {
 2  // code omitted to keep code example short
 3 
 4  const studentIterator = {
 5    next() {
 6      // code omitted to keep code example short
 7    },
 8    [Symbol.iterator]() {
 9      return this;
10     }
11   };
12 
13   return studentIterator;
14 };

```

现在，`studentIterator`对象是可迭代的，因此如果我们想，可以用`for...of`循环使用它。

我们还可以对上述代码示例进行一个改进。我们已经在`Student.prototype`对象中定义了`Symbol.iterator`方法，但它是[可枚举的](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Enumerability_and_ownership_of_properties)，这并不理想。我们可以通过使用[Object.defineProperty](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)方法将其设置为不可枚举，如下所示：

```js
1 Object.defineProperty(Student.prototype, Symbol.iterator, {
2   value: function () {
3     // copy the code inside the Symbol.iterator method from above
4   },
5   configurable: true,
6   writable: true
7 });

```

生成器是JavaScript中的特殊函数，它们可以在执行的不同点暂停其执行，然后从暂停的地方恢复。就像迭代器一样，生成器函数可以用于生成可以被`for...of`循环等结构消费的值序列。实际上，生成器函数返回一个生成器对象，而生成器对象是一个迭代器。因此，我们可以像使用其他迭代器一样使用生成器函数的返回值。

以下是一个生成器函数的示例，该函数生成从0到10的奇数：

```js
 1 function* odds() {
 2  for (let i = 1; i <= 10; i += 2) {
 3    yield i;
 4  }
 5 }
 6 
 7 for (const num of odds()) {
 8  console.log(num);
 9 }
10 
11 /*
12 1
13 3
14 5
15 7
16 9
17 */

```

这是上述代码运行的Replit示例：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/generators-example1” />`

请注意上述生成器函数中的以下两点：

+   `function*`语法将一个函数标记为生成器函数。在`*`和`function`之间的空格也是有效语法：`function *`。

+   `yield`关键字生成一个值。`yield`关键字右侧的值是我们在调用从生成器函数返回的迭代器对象的`next`方法时得到的。`yield`关键字还标记了生成器函数暂停的地方。

### 无限序列

生成器函数也可以用于创建无限序列，如下所示：

```js
 1 function* randomNumberGenerator(max) {
 2  while (true) {
 3    yield Math.floor(Math.random() * max);
 4  }
 5 }
 6 
 7 const randomNumGen = randomNumberGenerator(10);
 8 
 9 // log 10 random numbers
10 for (let i = 0; i < 10; i++) {
11   console.log(randomNumGen.next().value);
12 }

```

这是上述代码运行的Replit示例：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/generators-example2” />`

上述代码示例仅记录了10个随机数，但可以使用生成器生成无限个随机数。这是可能的，因为生成器函数是惰性评估的；它们的执行会被暂停，直到请求新的值。

在上述代码示例中，我们使用`next`方法消费生成器。注意，调用生成器函数并不会执行它；相反，它返回一个生成器对象。生成器对象既是一个迭代器也是一个可迭代对象。因此，我们可以像迭代器一样使用它，通过调用其上的`next`方法。对生成器对象调用`next`方法返回生成器所生成的值。对`next`方法的多次调用将继续返回生成器所生成的值，直到生成器对象停止生成值。在此时，我们得到一个`done`属性设置为`true`的对象。然而，上述生成器函数可以无限生成值。

### 实现迭代器

由于生成器函数返回一个迭代器对象，生成器函数使得编写迭代器变得方便。我们可以使用生成器函数重写上一课中的学生迭代器示例，如下所示：

```js
 1 function Student(name, age, id, courses) {
 2  this.name = name;
 3  this.age = age;
 4  this.id = id;
 5  this.courses = courses;
 6 }
 7 
 8 Student.prototype[Symbol.iterator] = function* () {
 9  // "this" refers to the student object on which this method is called
10   const currentStudent = this;
11   const studentProps = Object.getOwnPropertyNames(currentStudent);
12 
13   for (let i = 0; i < studentProps.length; i++) {
14     const key = studentProps[i];
15     const value = currentStudent[key];
16     const formattedValue = `${key.padStart(7)} => ${value}`;
17 
18     yield formattedValue;
19   }
20 };
21 
22 const jack = new Student("Jack", 20, "21A", ["Maths", "Biology", "Physics"]);
23 
24 for (const val of jack) {
25   console.log(val);
26 }
27 
28 /*
29    name => Jack
30     age => 20
31      id => 21A
32 courses => Maths,Biology,Physics
33 */

```

这是上述代码运行的Replit示例：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/generators-example3” />`

比较上一课中`Symbol.iterator`方法的实现与新的使用生成器函数实现学生迭代器的方法。代码更简单、简洁且易于阅读。生成器函数确实使得实现迭代器变得容易。

作为额外的好处，生成器函数返回的迭代器对象是自动可迭代的；因此，学生迭代器是可迭代的，而不需要我们手动设置原型链链接或在迭代器对象中实现``Symbol.iterator``方法。

### 消费值

虽然简单的迭代器仅产生值，但生成器也可以消费值。我们可以使用``next``方法向生成器传递一个值。传递给生成器的值成为``yield``表达式的值。考虑以下生成器消费值的代码示例：

```js
1 function* myGenerator() {
2   const name = yield "What is your name?";
3   yield `Hello ${name}!`;
4 }
5 
6 const gen = myGenerator();
7 console.log(gen.next().value); // What is your name?
8 console.log(gen.next("John").value); // Hello John!

```

这是上述代码在Replit中的运行示例：

<ReplitEmbed src=``https://replit.com/@newlineauthors/generators-example4`` />

第一次``next``方法调用生成第一个值，即``What is your name?``。此时，生成器函数暂停。``yield``表达式的值将根据我们如何再次调用``next``方法来计算。如果我们在第二次调用``next``方法时传递一个参数，该参数将成为``yield``表达式的值。在上述代码示例中，提供的参数是字符串``John``，所以第一次``yield``表达式的值是``John``，并且这被保存在生成器函数内部的``name``常量中。

第二次``next``方法调用为第一次``yield``表达式提供了一个值，并导致生成器函数生成下一个值，在上述代码示例中也是一个字符串。第二个``yield``值是使用``name``常量的值计算得出的。因此，我们从生成器函数获得``Hello John!``作为第二个值。

:::note 我们没有向第一次``next``方法调用传递任何参数；这是因为传递给第一次``next``方法调用的任何值都会被忽略。第一次``next``方法调用无法为第一次``yield``表达式提供值。第一次``yield``表达式的值将由第二次``next``方法调用提供；同样，第二次``yield``表达式的值可以由第三次``next``方法调用提供，以此类推。 :::

下面是一个生成器的示例，它无限生成随机数，并允许我们传递随机数应该生成的范围的上限。我们传递的数字不包含在范围内。

```js
 1 function* generatorRandomNumber(limit) {
 2  while (true) {
 3    const randomNumber = Math.floor(Math.random() * limit);
 4    limit = yield randomNumber;
 5  }
 6 }
 7 
 8 const randomNumGenerator = generatorRandomNumber(10);
 9 
10 console.log(randomNumGenerator.next());
11 console.log(randomNumGenerator.next(20));
12 console.log(randomNumGenerator.next(40));
13 console.log(randomNumGenerator.next(60));
14 console.log(randomNumGenerator.next(80));
15 console.log(randomNumGenerator.next(100));

```

这里是上述代码运行的Replit：

<ReplitEmbed src=``https://replit.com/@newlineauthors/generators-example5`` />

### 委托给其他迭代器

关于生成器的另一个很酷的功能是，它们允许我们将生成值的责任委托给其他迭代器，例如生成器。要委托责任，我们需要使用``yield*``操作符。这个操作符接受任何迭代器，并从中生成值，直到迭代器完成。以下是使用``yield*``操作符将生成偶数或奇数的责任委托给各自的生成函数的示例：

```js
 1 function* evens() {
 2  yield 2;
 3  yield 4;
 4  yield 6;
 5 }
 6 
 7 function* odds() {
 8  yield 1;
 9  yield 3;
10   yield 5;
11 }
12 
13 function* printNums(isEven) {
14   if (isEven) {
15     yield* evens();
16   } else {
17     yield* odds();
18   }
19 }
20 
21 for (const num of printNums(false)) {
22   console.log(num);
23 }
24 
25 // 1
26 // 3
27 // 5

```

这里是上述代码运行的Replit：

<ReplitEmbed src=”https://replit.com/@newlineauthors/generators-example6” />

`printNums`生成器根据`isEven`参数的值将生成值的责任委托给另外两个生成函数之一。

### 进一步阅读

+   [生成器 (MDN 文章)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Generator)

+   [yield* (MDN 文章)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/yield*)

我们在本模块的第一课中学习了可迭代对象和迭代器。可迭代对象是实现可迭代协议的对象，而迭代器是实现迭代器协议的对象。我们学习的迭代器是同步的。

JavaScript也有异步迭代器，其工作方式类似于同步迭代器。同步迭代器包含一个名为`next`的方法，当调用时，返回一个具有两个属性：`done`和`value`的对象。异步迭代器也包含一个名为`next`的方法，但它返回的是一个承诺，而不是返回具有之前提到的属性的对象。

对象实现`Symbol.iterator`方法以实现可迭代协议。对象可以通过实现[Symbol.asyncIterator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol/asyncIterator)方法来实现[异步可迭代协议](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#the_async_iterator_and_async_iterable_protocols)。

以下是使用异步迭代器从API获取用户的示例：

```js
 1 function fetchUsers(userCount) {
 2  // keep max user count to 10
 3  if (userCount > 10) {
 4    userCount = 10;
 5  }
 6 
 7  const BASE_URL = "https://jsonplaceholder.typicode.com/users";
 8  let userId = 1;
 9 
10   const userAsyncIterator = {
11     async next() {
12       if (userId > userCount) {
13         return { value: undefined, done: true };
14       }
15 
16       const response = await fetch(`${BASE_URL}/${userId++}`);
17 
18       if (response.ok) {
19         const userData = await response.json();
20         return { value: userData, done: false };
21       } else {
22         throw new Error("failed to fetch users");
23       }
24     },
25     [Symbol.asyncIterator]() {
26       return this;
27     }
28   };
29 
30   return userAsyncIterator;
31 }
32 
33 async function getData() {
34   const usersAsyncIterator = fetchUsers(3);
35 
36   let userIteratorResult = await usersAsyncIterator.next();
37 
38   while (!userIteratorResult.done) {
39     console.log(userIteratorResult.value);
40     userIteratorResult = await usersAsyncIterator.next();
41   }
42 }
43 
44 getData();

```

这里有一个Replit，展示了上述代码的运行效果：

<ReplitEmbed src="https://replit.com/@newlineauthors/async-iterators-example1" />

在上述代码示例中，我们直接使用异步迭代器，而不是使用像`for...of`循环这样的结构。稍后在本模块中，我们将看到如何使用循环消费异步迭代器。

请注意在上述代码示例中，`fetchUsers`函数中的`userAsyncIterator`对象实现了`Symbol.asyncIterator`方法，以实现异步可迭代协议。我们在关于迭代器的课程中讨论到，每个内置迭代器都继承自`Iterator.prototype`对象，并且本身也是可迭代的。为了使我们的自定义迭代器也成为可迭代的，我们可以使我们的迭代器继承自`iterator.prototype`对象，或者可以在我们的迭代器对象中实现`Symbol.iterator`方法以使其成为可迭代的。类似地，异步迭代器继承自`AsyncIterator.prototype`对象，这也是一个隐藏的全球对象，就像`Iterator.prototype`对象一样。我们可以使`userAsyncIterator`对象继承自`AsyncIterator.prototype`以使其成为可迭代的，或者可以实现`Symbol.asyncIterator`方法，如上面的代码示例所示。

简而言之，同步迭代器和异步迭代器之间的主要区别在于，异步迭代器的`next`方法返回一个承诺。接下来，我们将讨论异步生成器，正如常规生成器一样，它们可以帮助我们轻松实现`async`迭代器。

#### 进一步阅读

+   [`AsyncIterator (MDN 文章)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/AsyncIterator)

与同步迭代器和异步迭代器之间的区别类似，常规生成器和异步生成器之间的主要区别在于，异步生成器`yield`一个承诺。

`async`生成器是`async`函数和生成器的结合。因此，我们可以在`async`生成器内部使用`await`和`yield`关键字。调用一个`async`生成器会返回一个[`AsyncGenerator`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/AsyncGenerator)对象，该对象实现了`async`迭代器和`async`可迭代协议。`AsyncGenerator`对象的`next`方法返回一个承诺。

让我们将上节课的`async`迭代器示例重写为使用`async`生成器：

```js
 1 async function* fetchUsers(userCount) {
 2  // keep max user count to 10
 3  if (userCount > 10) {
 4    userCount = 10;
 5  }
 6 
 7  const BASE_URL = "https://jsonplaceholder.typicode.com/users";
 8 
 9  for (let userId = 1; userId <= userCount; userId++) {
10     const response = await fetch(`${BASE_URL}/${userId}`);
11 
12     if (response.ok) {
13       const userData = await response.json();
14       yield userData;
15     } else {
16       throw new Error("failed to fetch users");
17     }
18   }
19 }
20 
21 async function getData() {
22   const usersAsyncGenerator = fetchUsers(3);
23 
24   let userGeneratorResult = await usersAsyncGenerator.next();
25 
26   while (!userGeneratorResult.done) {
27     console.log(userGeneratorResult.value);
28     userGeneratorResult = await usersAsyncGenerator.next();
29   }
30 }
31 
32 getData();

```

这是上述代码的一个`Replit`：

`<ReplitEmbed src="https://replit.com/@newlineauthors/async-generators-example1" />`

:::info 在`fetchUsers`函数内部，我们可以简单地`yield` `response.json()`，而不是等待`response.json()`的结果并随后`yield` `userData`对象。这也会有效，因为从`async`函数返回一个承诺会将`async`函数的承诺解析为其主体内部返回的承诺。相同的原理在这里适用：如果我们`yield`一个承诺，`async`生成器的承诺将被解析为其内部`yield`的承诺。

:::  

`async`生成器使实现`async`迭代器变得非常简单，这就是您通常实现`async`迭代器的方式。

### `for await…of`循环

到目前为止，我们通过调用`next`方法直接消费了异步迭代器。`for...of`循环帮助我们迭代可迭代对象，而它有一个对应的循环，即[`for await…of`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for-await...of)循环，帮助我们迭代异步可迭代对象。以下代码示例展示了我们如何重写`getData`函数以使用`for await...of`循环：

```js
1 async function getData() {
2   for await (const user of fetchUsers(3)) {
3     console.log(user);
4   }
5 }

```

`for await...of`循环只能在可以使用`await`关键字的上下文中使用，即在`async`函数和模块内部。

#### 进一步阅读

+   [`async function* (MDN 文章)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function*)
