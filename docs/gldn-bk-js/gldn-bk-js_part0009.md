# 第六章

JavaScript中的函数式编程

让我们深入探讨一种越来越受到重视的编程范式：函数式编程。这个编程风格强调使用纯函数、数据不可变性和函数组合来创建更可预测和可维护的代码。我们将涵盖一等公民函数、高阶函数、柯里化和函数组合的概念，这些都是充分利用现代JavaScript的基础。

一等公民函数的概念

在JavaScript中，函数是一等公民，这意味着它们被视为语言的一等公民。这意味着函数可以分配给变量，可以作为参数传递给其他函数，并且可以由其他函数返回。这个概念是函数式编程的基础。

分配函数给变量：

```jsjavascript

const saudacao = function(nome) {

return `Hello, ${name}!`;

};

console.log(greeting("João"));

```

在上述示例中，匿名函数被分配给变量`greeting`，我们可以像调用其他函数一样调用它。

将函数作为参数传递：

```jsjavascript

const execute = function(function, value) {

return function(value);

};

const saudacao = function(nome) {

return `Hello, ${name}!`;

};

console.log(run(greetings, "Maria"));

```

在这里，我们将`greeting`函数作为参数传递给`execute`函数，然后`execute`使用给定的值调用`greeting`。

函数返回：

```jsjavascript

const criarSaudacao = function(saudacao) {

return function(nome) {

return `${greeting}, ${name}!`;

};

};

const hello = createGreeting("Hello");

console.log(ola("Pedro"));

```

在上述示例中，`createSaudacao`返回一个新函数，当调用时，它将初始问候与给定的名字结合在一起。返回函数的能力是函数式编程中的一个强大工具。

高阶函数

高阶函数是可以接受其他函数作为参数或返回它们的函数。它们是函数式编程中的主要构建块之一。

高阶函数的示例：

```jsjavascript

const map = function(arr, function) {

const result = [];

for (let i = 0; i < arr.length; i++) {

result.push(function(arr[i]));

}

return result;

};

const numbers = [1, 2, 3, 4, 5];

const dobrar = function(x) {

return x * 2;

};

console.log(map(numbers, double)); // [2, 4, 6, 8, 10]

```

在这里，`map`是一个高阶函数，它将`double`函数应用于`numbers`数组的每个元素，返回一个包含双倍值的新数组。

另一个示例是`filter`方法，它根据由函数提供的条件过滤数组中的元素：

```jsjavascript

const filter = function(arr, function) {

const result = [];

for (let i = 0; i < arr.length; i++) {

if (function(arr[i])) {

result.push(arr[i]);

}

}

return result;

};

const ePar = function ( x ) {

return x % 2 === 0;

};

console.log(filter(numbers, ePar)); // [2, 4]

```

在上述示例中，`filtering`是一个高阶函数，它将`ePar`函数应用于`numbers`数组的每个元素，并返回一个只包含偶数的新数组。

柯里化和函数组合

柯里化是将一个接受多个参数的函数转换为一系列每个只接受一个参数的函数的技术。这使得您能够创建更具体和可重用的函数。

柯里化示例：

```jsjavascript

const soma = function(a) {

return function(b) {

return a + b;

};

};

const soma5 = soma(5);

console.log(soma5(3)); // 8

console.log(soma(5)(3)); // 8

```

在上述示例中，`sum`是一个返回另一个函数的函数。`sum(5)`返回一个将5加到给定参数上的函数。这使得您能够以优雅的方式创建部分应用的函数。

函数组合是将简单函数组合以构造更复杂函数的实践。在JavaScript中，函数组合可以手动完成或使用诸如`Ramda`或`lodash`等库。

手动组合函数的示例：

```jsjavascript

const compor = function(f, g) {

return function(x) {

return f(g(x));

};

};

const adicionar1 = function(x) {

return x + 1;

};

const multiplicar2 = function(x) {

return x * 2;

};

const add1Multiply2 = compose(multiply2, add1);

console.log(add1Multiply2(5)); // 12

```

在上述示例中，`compose`是一个将`add1`和`multiply2`组合成一个新函数的函数，该新函数首先加1，然后将结果乘以2。

函数式编程的好处

函数式编程提供了几个好处，包括：

1\. 更可预测的代码：`纯函数`始终对相同参数产生相同结果且没有副作用，使代码更可预测且更易于理解。

2\. 测试的便利性：因为`纯函数`不依赖于外部状态，所以它们更易于测试。

3\. 代码重用：小而具体的函数可以以多种方式组合，从而促进代码重用。

4\. 简化竞争：不可变性和缺乏副作用减少了与竞争相关的问题。

在`JavaScript`中应用函数式编程

让我们在一个实际示例中应用所讨论的概念。假设我们有一个用户列表，我们想要筛选出活跃用户，将他们的名字映射到一个新列表，最后统计我们有多少活跃用户。

```jsjavascript

const users = [

{ name: "Alice", active: true },

{ name: "Bob", active: false },

{ name: "Carol", active: true },

{ name: "Dave", active: false }

];

const filterAssets = function(users) {

return users . filter ( function ( user ) {

return user.active;

});

};

const mapNomes = function(users) {

return users . map ( function ( user ) {

return user.name;

});

};

const contar = function(arr) {

return arr.length;

};

const activeUsers = filteractive(users);

const nomesAstivos = mapearNames(usuariosAtivos);

const numberOfAsset = count(namesAsset);

console.log(namesActivos); // ["Alice", "Carol"]

console.log(numeroDeAtivos); // 2

```

在这个例子中，我们使用了`高阶函数`（`filter`和`map`）和`函数组合`，对用户列表进行一系列转换。这种编程风格使代码更易于阅读和维护。

我们探讨`JavaScript`中函数式编程的基础，包括`一等公民函数`、`高阶函数`、`柯里化`和`函数组合`。这些概念不仅使您的代码更优雅和模块化，还更易于理解和维护。通过采用函数式编程实践，您可以创建更强大、错误更少的`JavaScript`应用程序。随着我们的深入，我们将继续在这些概念的基础上构建，探索更复杂的应用和先进的`JavaScript`编程实践。准备好转变您的编码方式，发现高效且创新的问题解决新方法。
