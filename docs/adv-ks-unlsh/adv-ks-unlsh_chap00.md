## `什么是 JavaScript`

### `课程概述`

`JavaScript 可以说是全球使用最广泛的编程语言，学习 JavaScript 的内容丰富。然而，互联网并不是所有内容都能很好地解释 JavaScript 的复杂或令人困惑的概念。`

`本课程旨在教授 JavaScript 中不易掌握的不同概念，特别是对于初学者而言。像闭包、强制类型转换、JavaScript 的异步特性等主题，都是大多数初学者难以理解的主题。本课程的目标是提供对这些令人困惑主题的深入、易于理解的解释。`

`即使是那些已经使用 JavaScript 几年的人，可能也需要帮助理解本课程中涵盖的一些概念，或者他们的理解可能存在一些空白。本课程的目标是填补这些空白。`

`本课程不仅将提供易于理解的 JavaScript 基础主题解释，如提升、强制类型转换、事件循环等，还将以易于学生理解的方式涵盖高级主题，如 Promise 和 async-await 语法。`

`在本课程结束时，学生将对课程中涵盖的概念有深入理解。他们将通过对大多数 JavaScript 初学者难以掌握的主题有扎实理解而在 JavaScript 上表现更好。学生将能够更好地调试 JavaScript 代码，并通过对基础但复杂的 JavaScript 主题有深入理解而避免常见的陷阱。`

### `先决条件`

`本课程假设学生对 JavaScript 和编程有基本了解。假设学生理解变量、循环、对象、数组、函数等主题。`

### `运行代码示例`

`你可以从购买本书的同一地方下载代码示例。`

`如果你在查找或下载代码示例时遇到任何问题，请通过电子邮件联系我们：[us@fullstack.io](mailto:us@fullstack.io)。`

### `本课程适合谁？`

`本课程适合以下人群：`

+   `在深入理解 JavaScript 方面感到挣扎`

+   `理解从基础到高级的 JavaScript 概念，但希望填补在成为优秀 JavaScript 开发者的关键主题（如闭包、强制类型转换、事件循环、异步 JavaScript、Promise 等）中的理解空白`

+   `希望深入理解 JavaScript 并提高 JavaScript 的工作能力`

+   `希望提高 JavaScript 调试能力并为求职面试做准备，因为本课程将提供对 JavaScript 语言更深刻的理解`

+   `希望巩固对 JavaScript 基础主题的理解`

+   `希望避免因对 JavaScript 复杂主题缺乏理解而带来的挫折`

+   `希望在 JavaScript 工作中表现出色`

这门课程不同于在线文章/博客和许多`JavaScript`视频课程，它们要么未能深入、易懂地解释`JavaScript`主题，导致初学者难以理解，要么没有涵盖成为优秀`JavaScript`开发者所必需的所有主题（从基础到高级）。

这门课程将基础但令人困惑的`JavaScript`主题结合在一起，旨在为学生提供扎实的理解，并覆盖理解`JavaScript`的深度所需的所有关键主题。

`JavaScript`目前是使用最广泛的编程语言。随着现代前端框架和像`Node.js`这样的平台的兴起，似乎`JavaScript`在可预见的未来将是最常用的编程语言。

它是网页的编程语言，最常用于为网页添加交互性。借助像`Node.js`这样的技术，我们可以在浏览器环境之外编写`JavaScript`，软件开发者现在可以通过学习一门编程语言来编写全栈应用程序。

那么，这门我们今天所知的编程语言是如何产生的呢？让我们简要回顾一下它的历史。

### `JavaScript`的历史

在网页浏览器的早期，网页只能是静态的，没有动态行为或交互性。简单的表单输入验证等功能需要服务器支持。由于当时互联网速度有限，仅为输入验证而进行一次往返到服务器的请求是非常不理想的。

需要一种客户端脚本语言，以便为网页添加交互性。1995年，一位来自`Netscape`的软件开发者开始研发这种语言，最初称为“`mocha`”，后来更名为“`LiveScript`”。

这门语言本应成为`Netscape Navigator 2`浏览器的一部分，但在浏览器发布前，`LiveScript`被更名为“`JavaScript`”。

当`Netscape`发布其`Netscape Navigator 3`浏览器时，`Microsoft`推出了其网页浏览器`Internet Explorer 3`，其中包含了`Microsoft`对`JavaScript`语言的实现。

这就带来了一个问题：现在存在两个不同的`JavaScript`语言实现。需要一个负责推动`JavaScript`语言发展的标准机构。

### `JavaScript`语言的标准化

多个版本的`JavaScript`问题促使`Netscape`将`JavaScript`语言提交给标准组织`Ecma International`。

`JavaScript`被标准化为“`ECMAScript`”，其标准为[`ECMA-262`](https://www.ecma-international.org/publications-and-standards/standards/ecma-262/)。

如前一课所述，`JavaScript`的最初名称是`Mocha`，后来更改为`LiveScript`，在`Netscape Navigator 2`浏览器发布之前，名称被改为`JavaScript`。

那么，为什么在`JavaScript`的名称中使用`Java`这个词呢，当时已经有一门流行的编程语言叫做`Java`？

是否这两种语言彼此相关的问题几乎在每一个已经熟悉其中一种语言并接触到另一种语言的人心中都会出现。

这只是一个`营销策略`。当时Java非常流行，而`Netscape`希望利用`Java`语言的热度。这就是`Netscape`将语言名称从`LiveScript`更改为`JavaScript`的原因。

除了语法和当然名称上的一些相似之处，这两种语言实际上是非常不同的。

### `Ecma International`，`TC39`

`JavaScript`由标准组织`Ecma International`标准化为`ECMAScript`。

在`Ecma International`内，负责开发`JavaScript`语言的人是`技术委员会39`（`TC39`）的一部分。这个委员会由来自`JavaScript`社区的不同利益相关者组成。大多数成员来自`Google`、`Microsoft`等大公司。

其他人也可以成为`TC39`的一部分，并在`JavaScript`语言的发展中做出贡献。有关任何人如何参与或成为`TC39`会议成员的详细信息，可以在[`TC39网站`](https://tc39.es/)上找到。

`TC39`还有一个[`GitHub账户`](https://github.com/tc39)，该账户托管与他们的工作相关的多个代码库。代码库包括`TC39`会议的记录、针对`JavaScript`语言的不同提案、`TC39`工作方式的详细信息等。

### `提案流程`

`TC39`有一个明确的流程，通过这个流程，提案在可以被纳入`ECMAScript`规范并最终成为`JavaScript`语言的一部分之前被审议。

每个提案经过以下五个阶段：

![过程阶段](images/module_01----lesson_01.04----public----assets----proposal-stages.png)

`过程阶段`

#### `阶段0`

第一阶段代表某人的想法，他们认为这个想法值得成为`JavaScript`语言的一部分。

并不是所有在这个阶段的提案都能进入下一个阶段，但能够进入的提案都是那些获得足够兴趣并且有`TC39`委员会成员愿意在这个想法上工作的提案。在这个阶段获得足够兴趣的提案将在`TC39`会议上进行讨论。如果讨论顺利，提案将进入下一个阶段。

#### `阶段1`

此阶段的提案由社区（包括非委员会成员）讨论和发展，如果提案仍然有足够的兴趣，并被认为在加入规范时会有潜在的好处，初步规范语言和`API`将在`TC39`会议中开发和讨论。如果一切顺利，提案将移至下一个阶段。

#### `阶段2`

在这个阶段，API、语法等被精炼并使用正式规范语言更详细地描述。这个阶段可能会开发polyfills和Babel插件，以便在实际中实验提案的解决方案。

一旦提案被描述得足够详细，就可以考虑进入下一个阶段。

#### `阶段3`

此阶段的提案几乎准备好纳入ECMAScript规范。

要将提案移至最终阶段，需要满足以下两个标准：

+   `一系列测试`

+   `两个通过测试的提案兼容实现`

一旦满足上述条件，并且委员会达成共识，认为提案准备好成为ECMAScript规范的一部分，它将移至下一个阶段。

#### `阶段4`

在这个阶段，提案已完成，并准备纳入ECMAScript规范，并最终添加到JavaScript语言中。

会生成一个对`ecma262` GitHub仓库的拉取请求，以将其纳入规范。一旦拉取请求获得批准，提案就成为规范的一部分，并准备在仍需实现的JavaScript引擎中实施。

有关此过程的更多细节，请参考[`过程文档`](https://tc39.es/process-document/)，该文档在TC39网站上解释了提案经过的各个阶段。

### 跟踪即将推出的功能。

最近几年对JavaScript语言的补充完全改变了JavaScript，使其成为一门编程语言，有时，跟上语言新补充的步伐可能会很困难。

跟上新变化是一回事，但我们如何跟踪可能成为未来JavaScript一部分的变化呢？

这个问题的答案在[`TC39的GitHub仓库`](https://github.com/tc39)中，该仓库包含了处于提案过程各个阶段的[`会议记录`](https://github.com/tc39/notes)和[`提案`](https://github.com/tc39/proposals)。

会议记录和提案仓库是跟踪即将变化的绝佳地方，通常`TC39` GitHub仓库对跟踪TC39委员会的工作非常有用。

### ECMAScript是如何版本化的？

ECMAScript 版本 5，也称为“ES5”，于2009年发布，在那之前，ECMAScript规范是通过其`版本`编号来引用的，但随着第六版ECMAScript的引入，也称为“ES6”，TC39在语言名称中添加了`年份`编号。

随着第六版在2015年发布，它被称为“ECMAScript 2015”，简称“ES2015”。后续版本也使用发布年份命名，例如“ES2016”等。

你还会看到这些版本被称为“`ES6`”、“`ES7`”等，这种命名方式也是可以使用的。你选择哪一种取决于你的偏好。在大多数情况下，你会看到两种类型的名称可以互换使用。

在撰写本文时，`ECMAScript 2023`是最新的`ECMAScript`版本。

由于`JavaScript`的执行方式，许多人将其视为一种“解释”语言，但仅将`JavaScript`称为“解释”语言并不完全正确。

对于编译语言，编译器通常会编译源代码并生成一个二进制可执行文件，这个文件可以被分发和执行。

另一方面，对于解释语言，解释器不会产生可执行输出文件；与编译器不同，编译器提前编译源代码，解释器则是实时读取并执行代码。

对于`JavaScript`而言，`JavaScript`引擎不会输出可执行文件，这也是它被视为解释语言的原因之一。

然而，`JavaScript`代码被*编译*成一种称为`字节码`的中间形式，然后由虚拟机执行。虚拟机`解释`字节码，但现代`JavaScript`引擎不仅仅是解释字节码；它们包括被称为“`即时编译 (JIT) 编译器`”的组件，将字节码编译成本地机器码，这种机器码的执行速度快于字节码。

### `JIT 编译器`

“`即时编译 (JIT)`”是一种被许多现代`JavaScript`引擎使用的技术，以提高`JavaScript`代码的执行速度。

`JavaScript`代码被转换成字节码，然后`JavaScript`引擎执行这些字节码。然而，现代`JavaScript`引擎进行许多优化以提高`JavaScript`代码的性能。这些优化是在引擎执行代码时收集的信息基础上进行的。

优化性能的一种方法是将字节码编译成机器码，机器码执行速度快于字节码。`JavaScript`引擎识别代码中的“热”部分来实现这一点——即频繁执行的部分。

这些“热”代码部分随后被编译成本地机器码，并且这段机器码在执行时会替代相应的字节码。

那么，`JIT`编译器与像`C++`这样的传统编译器有何不同？与传统编译器提前编译代码不同，`JIT`编译器在代码执行时实时编译代码。

尽管`JavaScript`代码仍以源代码格式分发而非可执行格式，但它会被编译成字节码，并可能编译成本地机器码。

所以，回到问题上：`JavaScript`是编译语言还是解释语言？可以安全地说它既是*编译的*也是*解释的语言*。

`我们不一定需要理解我们编写的JavaScript代码是如何被执行的细节，但要对语言有良好的理解，重要的是要基本了解我们的JavaScript代码如何转变为机器能够理解和执行的内容。`

`理解代码执行过程中涉及的不同因素也很重要；例如“` **执行上下文** `”、“` **调用栈** `”等概念对于理解JavaScript语言的运行时行为以及能够高效地进行调试至关重要。`

### `JavaScript 引擎`

`要执行JavaScript代码，我们需要另一个被称为` **JavaScript 引擎** `的软件。这个引擎包含所有必要组件，将代码转换为机器可执行的内容。`

`不同的浏览器厂商通常会创建JavaScript引擎；每个主要厂商都开发了一个在其浏览器中执行JavaScript代码的引擎。`

`下表显示了一些主要浏览器及其JavaScript引擎。`

| `浏览器` | `引擎` |
| --- | --- |
| `---` | `---` |
| `谷歌 Chrome` | `V8` |
| `Edge` | `Chakra` |
| `Mozilla Firefox` | `Spider Monkey` |
| `Safari` | `JavaScriptCore` |

`虽然每个JavaScript引擎在执行JavaScript代码时采取的步骤有所不同，但每个引擎采取的主要步骤或多或少是相同的，我们将尝试通过理解Google Chrome的` `V8` `引擎，来对代码如何被转换和执行进行高层概述。`

`以下图像展示了V8引擎执行管道的高层概览：`

![process stages](images/module_01----lesson_01.08----public----assets----v8-execution-pipeline.png)

`过程阶段`

`JavaScript引擎是复杂的软件，包含许多步骤和组件，用于转换和执行JavaScript代码，但上述图像展示了V8引擎执行管道的简化版本。`

`:::note 请注意，负责V8引擎的团队正在不断改进它；因此，上述图中显示的简化执行管道可能在未来会发生变化。 :::`

`让我们通过理解该管道每一步发生的事情，来更好地了解上述执行管道的工作原理。`

#### `源代码`

`在JavaScript引擎开始工作之前，源代码需要从某个来源下载。这可以是来自网络、缓存，或者是预先获取代码的服务工作者。`

`引擎本身没有下载代码的能力。浏览器完成此操作，然后将其传递给引擎，后者可以开始转换并最终执行它。`

#### `解析器`

下载源代码后，下一步是将其转化为`tokens`。将此步骤视为识别代码的不同部分；例如，单词“function”是一个被识别为“关键字”的`token`。其他的`tokens`可能包括字符串、运算符等。将代码划分为`tokens`的过程由“扫描器”完成，这个过程被称为“`tokenization`”。

以下的`JavaScript`代码：

```js
1 function add(num1, num2) {
2   return num1 + num2;
3 }

```

它可以如下进行标记：

```js
 1 [
 2  { type: "keyword", value: "function" },
 3  { type: "identifier", value: "add" },
 4  { type: "openRoundParen", value: "(" },
 5  { type: "identifier", value: "num1" },
 6  { type: "identifier", value: "num2" },
 7  { type: "closeRoundParen", value: ")" },
 8  { type: "openCurlyParen", value: "{" },
 9  { type: "keyword", value: "return" },
10   { type: "identifier", value: "num1" },
11   { type: "addOperator", value: "+" },
12   { type: "identifier", value: "num2" },
13   { type: "closeCurlyParen", value: "}" }
14 ];

```

一旦生成了`tokens`，解析器使用它们生成一个[抽象语法树（AST）](https://en.wikipedia.org/wiki/Abstract_syntax_tree)，一组表示源代码结构的对象。

[AST Explorer](https://astexplorer.net/)是一个很酷的网站，你可以用它来可视化`AST`。请将上面的代码粘贴到`AST Explorer`中，探索生成的`AST`。

#### `解释器`

`字节码生成器`使用解析器生成的`AST`来生成字节码。这个生成的字节码由`字节码解释器`接收，然后进行解释。

`V8`也会将生成的字节码通过一些优化器，这些优化器执行一些优化以确保字节码在`字节码解释器`中高效执行。

#### `编译器`

在字节码被执行时，`JavaScript`引擎收集关于正在执行的代码的信息。引擎随后使用这些信息进一步优化代码。

例如，`JavaScript`引擎可以识别正在频繁执行的代码部分，也称为代码的“热点”部分。这些“热点”部分的代码随后被编译为本地机器代码，以确保这些部分尽可能快地执行。

然而，优化后的本地机器代码有时必须被去优化回由`字节码生成器`生成的字节码，因为代码的编写方式。

回退到字节码的需求源于`JavaScript`是一种[动态类型](https://developer.mozilla.org/en-US/docs/Glossary/Dynamic_typing)语言。动态特性意味着我们可以用不同类型的值调用特定的`JavaScript`函数。

考虑以下代码：

```js
1 function print(obj) {
2   console.log(obj);
3 }

```

上述函数可以与不同“形状”的对象调用。

```js
1 print({ a: 1, b: 2, c: 3 });
2 print({ a: 1, c: 3 });
3 print({ b: 2 });

```

这意味着如果`print`函数多次被调用，且对象具有以下形状：

```js
1 { a: 1, b: 2, c: 3 }

```

如果它被编译为本地机器代码，但如果同一个函数与一个*不同*形状的对象被调用，`JavaScript`引擎就不能使用优化过的机器代码，而必须回退到字节码。

优化后的本地机器代码是使用在执行JavaScript代码时收集的信息生成的。本地机器代码需要进行某些检查，以确保在生成本地机器代码时所做的假设没有被违反。如果检查失败，JavaScript引擎必须执行字节码，而不是本地机器代码。这个过程称为`反优化`。

##### 参考文献：

以下资源可用于了解更多关于JavaScript代码执行的信息：

+   [理解V8 JavaScript引擎 - (Lydia Hallie的freeCodeCamp演讲)](https://www.youtube.com/watch?v=xckH5s3UuX4)

+   [JavaScript是如何工作的：V8引擎背后的秘密 - (freeCodeCamp博客)](https://www.freecodecamp.org/news/javascript-under-the-hood-v8/)

+   [V8的点火究竟做了什么？ - (stackoverflow帖子)](https://stackoverflow.com/questions/54957946/what-does-v8s-ignition-really-do)

+   [Ignition - V8的解释器 - (youtube视频)](https://www.youtube.com/watch?v=r5OWCtuKiAk)

+   [超快解析，第1部分：优化扫描器 - (V8博客)](https://v8.dev/blog/scanner)

+   [V8 JavaScript引擎中的反优化检查开销 - (加州大学计算机工程系论文)](https://masc.soe.ucsc.edu/docs/iiswc16.pdf)

每当执行任何JavaScript代码时，都会在一个环境中执行。这里所说的“环境”指的是所有可被代码访问的，有助于其执行的内容。例如，`this`的值、当前作用域中的变量、函数参数等。这个环境被称为`执行上下文`。每次执行任何JavaScript代码之前，都会创建一个执行上下文。

:::note

理解执行上下文的概念为理解其他JavaScript概念奠定了基础，例如`提升`、`闭包`等。这些主题将在后面的章节中讨论。

:::

### 执行上下文的类型

以下是我们将讨论的两种主要执行上下文类型：

+   全局执行上下文

+   函数执行上下文

:::info

还有第三种类型的执行上下文，是为在[`eval`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval)函数内执行代码而创建的。然而，由于安全问题，不鼓励使用`eval`函数，因此我们将只讨论上述提到的执行上下文类型。

:::

#### 全局执行上下文

全局执行上下文是在每次加载JavaScript代码以供执行时创建的基本上下文。全局代码，即不在函数内部的代码，在全局执行上下文中执行。

全局上下文包含全局变量、函数等。它还包含`this`的值和对外部环境的引用，在全局执行上下文的情况下，外部环境为`null`。

#### 函数执行上下文

每次调用JavaScript函数时，都会为该函数的执行创建一个新的执行上下文。与全局执行上下文类似，函数执行上下文包含：

+   变量和函数在函数内部声明。

+   当前函数调用中`this`的值。

+   对外部环境的引用。

函数执行上下文还包含传递给函数的参数。

### 执行上下文阶段

执行上下文有以下两个阶段：

+   创建阶段

+   执行阶段

#### 创建阶段

正如名称所示，执行上下文（全局和函数）是在创建阶段创建的。

在这个阶段，变量声明和对函数的引用被保存为键值对，存放在执行上下文中。`this`的值和对外部环境的引用也在此阶段设置。

在创建阶段，变量的值并未被赋值。然而，引用函数的变量在此阶段确实会引用函数。用`var`声明的变量在此阶段被赋值为`undefined`，而用`let`声明的变量或用`const`声明的常量则保持未初始化状态。

:::info

在全局上下文中，没有外部环境，因此对外部环境的引用被设置为`null`；而在函数上下文中，`this`的值取决于函数的调用方式，因此`this`的值被适当地设置。

:::

##### 词法和变量环境

在创建阶段，将创建以下两个组件：

+   词法环境

+   变量环境

词法和变量环境是用于内部存储变量、函数、对外部环境的引用以及`this`的值的结构。

词法环境和变量环境之间的区别在于，变量环境仅包含用`var`关键字声明的变量的键值映射，而函数声明和用`let`或`const`声明的变量则位于词法环境内。

考虑以下代码：

```js
1 let name = "Jane Doe";
2 var age = 20;
3 
4 function introduce(name, age) {
5   console.log("Hello, I am " + name + " and I am " + age + " years old");
6 }

```

上述代码在创建阶段的执行上下文可以概念上可视化为下图所示：

![全局执行上下文](images/module_01----lesson_01.09----public----assets----gec-creation-phase.png)

全局执行上下文

#### 执行阶段

正如前面提到的，在创建阶段之后，执行上下文中的不同变量尚未被赋予各自的值。赋值将在执行阶段进行，代码最终被执行。

##### 参考文献

以下资源可用于进一步了解JavaScript中的执行上下文：

+   [理解JavaScript中的执行上下文和执行栈 - (博客)](https://blog.bitsrc.io/understanding-execution-context-and-execution-stack-in-javascript-1c9ea8642dd0)

+   [JavaScript执行上下文 – JS背后的工作原理 - (freeCodeCamp博客)](https://www.freecodecamp.org/news/execution-context-how-javascript-works-behind-the-scenes/)

+   [JavaScript幕后揭秘 - 执行上下文 - (YouTube视频)](https://www.youtube.com/watch?v=Fd9VaW0M7K4)

调用栈是JavaScript引擎内部用于跟踪当前正在执行的代码片段的结构。调用栈只是一个[栈](https://en.wikipedia.org/wiki/Stack_(abstract_data_type))数据结构，通过跟踪当前执行的代码来帮助执行JavaScript代码。你也可以将JavaScript中的调用栈视为执行上下文的集合。

在执行任何JavaScript代码之前，创建一个全局执行上下文并将其压入调用栈。可以通过浏览器开发者工具中的调试器轻松可视化。

![全局执行上下文被压入调用栈](images/module_01----lesson_01.10----public----assets----global-execution-context.png)

全局执行上下文被压入调用栈

:::note

`debugger`关键字简单地创建一个断点，强制调试器在包含`debugger`关键字的行上停止。我们将在后面的章节中讨论调试。

::::

请注意，在上述图像中，在执行`console.log`语句之前，调用栈中有一个名为“global”的东西。这是一个全局执行上下文，在执行代码之前创建并压入调用栈。

:::note

标签“global”并不重要，不同的浏览器可能使用不同的标签来表示调用栈中的全局执行上下文。例如，Google Chrome浏览器中的调试器显示“(anonymous)”而不是“global”。上述屏幕截图是在Firefox浏览器中拍摄的。

::::

在将全局执行上下文压入调用栈后，在执行代码期间遇到的任何函数调用都会导致调用栈中更多条目的添加。对于每个函数调用，在该函数开始执行之前都会向调用栈添加一个新的条目，一旦函数执行结束，该条目就会从栈中弹出。考虑以下代码：

考虑以下代码：

```js
 1 function bar() {
 2  console.log("hello world");
 3 }
 4 
 5 function baz() {
 6  bar();
 7 }
 8 
 9 function foo() {
10   baz();
11 }
12 
13 foo();

```

在执行上述代码之前，全局执行上下文被压入调用栈。

![调用栈](images/module_01----lesson_01.10----public----assets----callstack-1.png)

调用栈

一旦调用`foo`函数，一个新的条目被添加到调用栈中以执行`foo`函数。

![调用栈](images/module_01----lesson_01.10----public----assets----callstack-2.png)

调用栈

`foo`函数包含对`baz`函数的调用。因此，另一个条目被压入调用栈以进行`baz`函数调用。

![调用栈](images/module_01----lesson_01.10----public----assets----callstack-3.png)

调用栈

`baz`函数包含对`bar`函数的调用。因此，另一个条目被推入`bar`函数调用的调用栈。

![调用栈](images/module_01----lesson_01.10----public----assets----callstack-4.png)

调用栈

请注意，调用栈中的顶部元素代表当前正在执行的代码片段。一旦`bar`函数执行结束，它在调用栈中的条目将被移除。最终，代码执行完成，调用栈变为空。

您可以在下面的`Replit`中运行上述代码，以查看调用栈的实际效果：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/Lesson-9-callstack” />`

### `堆栈溢出`

“`堆栈溢出`”是每个软件开发人员都熟悉的术语，无论是因为每个软件开发人员最喜欢的网站[stackoverflow](https://stackoverflow.com/)，还是因为无限递归导致的堆栈溢出错误。

我们将在调用栈的上下文中讨论“`堆栈溢出`”这个术语。调用栈的大小是固定的，并且可以包含有限数量的条目。

那么，如果我们创建一个只是调用自己的函数，会发生什么呢？

```js
1 function foo() {
2   foo();
3 }

```

还记得调用函数时会发生什么吗？一个新条目被添加到调用栈中。在上述仅调用自身且永不完成执行的函数的情况下，我们只是不断在调用栈中添加新条目，而从未移除任何条目。这就是无限递归，这会导致一个称为`stack overflow`的错误。当调用栈填满到其限制，并且无法再容纳更多条目时，就会抛出此错误。

网络上有很多资源声称原始值在栈上分配，而对象在堆上分配，但现实并非如此简单。

官方的`ECMAScript`规范没有说明JavaScript引擎应该如何为不同类型的值分配内存，或者在程序不再需要内存时如何释放内存。因此，不同的JavaScript实现可以自由选择如何处理JavaScript中的内存管理。

因此，我们不应该简单地相信原始值存储在栈上，而对象存储在堆上，而应该理解，JavaScript中的内存分配是一个实现细节，不同的JavaScript引擎可能以不同的方式处理内存，因为语言规范并未规定JavaScript中的内存应该如何处理。

在`V8`引擎中，几乎所有内容都是存储在堆上的。以下引用来自[官方V8博客](https://v8.dev/blog/pointer-compression#value-tagging-in-v8)，它揭示了关于JavaScript中内存分配的常见误解。

> 在`V8`中，JavaScript值被表示为对象并分配在`V8`堆上，无论它们是对象、数组、数字还是字符串。这使我们能够将任何值表示为指向对象的指针。

这并不意味着我们应该假设所有东西都在堆上分配。JavaScript引擎可能会在堆上分配*大部分*值，但也可能利用栈进行优化，存储的临时值可能不会持续超过函数调用。

JavaScript引擎是复杂的软件，经过了大量优化。假设它们都仅仅遵循*原始值在栈上而对象在堆上*的简单规则是不合理的。

你应该从这节课中得到的最重要的观点是，不同的JavaScript引擎可能会以不同的方式处理内存，而“原始值在JavaScript中简单地在栈上”是一种`misconception`。

##### 进一步阅读

+   [JavaScript内存模型揭秘 - (博客)](https://www.zhenghao.io/posts/javascript-memory)

+   [JavaScript变量是如何分配的 - (博客)](https://www.zhenghao.io/posts/javascript-variables)

+   [JavaScript函数调用结果的内存分配在哪里？栈还是堆？ - (stackoverflow帖子)](https://stackoverflow.com/questions/67356107/where-does-javascript-allocate-memory-for-the-result-of-a-function-call-stack-o)

### 自动垃圾收集

与C等其他语言不同，在这些语言中，程序员负责在不再需要时释放内存，JavaScript通过自动处理内存使程序员的工作变得更轻松。

不再需要的内存会被JavaScript引擎自动释放，这个过程称为`garbage collection`。现代JavaScript引擎包括一个垃圾收集器，负责确定哪些内存部分不再需要并可以释放。一旦确定了这些内存块，这些块就会被垃圾收集器释放。

不同的算法用于确定哪些内存块不再需要并符合垃圾收集的条件。目前，现代JavaScript引擎使用[标记-清除算法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Memory_Management#mark-and-sweep_algorithm)。

该算法确定哪些内存块是“不可达”的；这些内存块被认为符合垃圾收集的条件。这个算法是对[引用计数算法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Memory_Management#reference-counting_garbage_collection)的改进，但它有其局限性。

Java语言也有自动垃圾收集的机制，但在Java中，程序员可以手动触发垃圾收集过程，而JavaScript程序员对垃圾收集没有这样的控制级别。有些人可能会把这视为一种限制，但毫无疑问，自动垃圾收集确实对程序员避免在不自动处理内存的语言中经常遇到的内存泄漏非常有帮助。
