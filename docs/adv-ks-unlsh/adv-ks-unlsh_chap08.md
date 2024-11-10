## `异步 JavaScript`

在本模块中，我们将涵盖`JavaScript`中的异步编程。我们将学习异步编程意味着什么，以及在`JavaScript`中传统上是如何做到的。我们还将讨论传统处理异步代码的方法存在的问题，以及`ES2015`中引入的承诺如何改变我们处理异步代码的方式。我们将详细讨论承诺，并学习简化使用承诺的`async-await`语法。

### 异步是什么意思？

在编程的上下文中，“异步”意味着程序启动一个潜在的长时间运行任务，并可以在该任务在后台执行时自由进行其他任务。关键点在于，程序不必等待长时间运行的任务完成；它可以自由执行其他任务。一旦任务完成，程序将收到通知并呈现任务的结果。

由于传统同步编程存在的问题，因此需要异步编程。在同步程序中，每条指令都是按顺序一个接一个地执行的。指令按程序中出现的顺序执行。因此，同步程序更容易推理，但它们也存在异步编程所解决的问题。

同步程序的问题在于，一个潜在的长时间运行任务会阻塞程序的执行，直到其完成。这会导致性能差、用户体验差以及资源利用效率低等问题。

尽管异步程序解决了同步程序所呈现的问题，但异步程序也带来了自己的一系列挑战，如错误处理、管理共享状态和资源、协调程序不同部分之间的关系等。

### `异步 JavaScript`

在我们深入探讨如何在`JavaScript`中编写异步代码以及它如何在幕后处理之前，让我们先退一步，看看如果我们执行一些长时间运行的代码（如以下示例中的循环），我们在`JavaScript`中面临的问题。

```js
 1 function block() {
 2  const start = new Date();
 3 
 4  while (new Date() - start < 3000) {
 5    // simulate long running operation
 6    // that takes approximately 3 seconds
 7  }
 8 }
 9 
10 console.log("Before long running operation");
11 // gets logged immediately
12 
13 block();
14 
15 console.log("After long running operation");
16 // gets logged after approximately 3 seconds

```

你可以在这个`Replit`中查看上面的代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/overview-example1">`

`JavaScript`是一种单线程语言，这有其优缺点。`JavaScript`开发者通常不必担心多线程程序所带来的问题，比如[`竞争条件`](https://stackoverflow.com/questions/34510/what-is-a-race-condition)和[`死锁`](https://stackoverflow.com/questions/34512/what-is-a-deadlock)。然而，单线程的限制在上面的代码示例中显而易见。

上面的代码示例旨在模拟一些大约需要3秒钟才能完成的长时间运行的代码。在这3秒钟内，执行我们JavaScript代码的主线程被阻塞；在这3秒钟内没有其他代码执行。如果这段JavaScript代码附加到HTML文件并在浏览器中执行，UI将冻结，直到循环结束。

要查看冻结的UI效果，可以尝试将上述JavaScript代码添加到一个名为`index.js`的文件中，并将其附加到包含以下HTML的HTML文件中：

```js
1 <h1>hello world</h1>
2 <button onclick="alert('hello')">Click</button>

```

您可以在这个Replit中看到上面的代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/overview-example2">`

在初始页面加载时，您会注意到按钮在几秒钟内不可点击。UI会保持冻结，直到JavaScript代码执行完成，特别是长时间运行的循环。

这在Web应用程序中提供了糟糕的用户体验。单线程对我们在主线程中使用JavaScript所能做的施加了严格的限制。

现在，JavaScript引擎足够强大，能够以非常好的速度执行代码；引擎旨在高度优化JavaScript代码，以尽可能高效地执行它。不过，仍然需要注意，主线程不应被任何可能需要很长时间才能使延迟变得明显的代码阻塞。

:::info

JavaScript还允许我们在另一个线程中执行一些代码，与主线程独立，使用`[网络工作者](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API)`。

::::

接下来，让我们讨论使用回调编写异步代码的传统方式。我们还将讨论使用回调时的问题。

使用回调函数处理异步代码一直是JavaScript中编写异步代码的传统方式。回调函数是作为参数传递给另一个函数的函数，旨在在某个异步操作完成后调用。接收回调函数作为参数的函数通常会使用异步操作的结果或在异步操作失败时的错误来调用回调函数。

类似HTTP请求的操作是异步的，但它们并不是由JavaScript处理的。我们编写的代码启动异步操作；在客户端JavaScript的情况下，实际的异步操作由浏览器处理，而在NodeJS运行时的情况下，则由后台线程或操作系统本身处理。

简单来说，异步操作在后台（JavaScript领域之外）进行，而与此同时，其他事情可以在主线程（JavaScript领域）中执行。

当异步操作完成时，我们的JavaScript代码会收到通知，导致执行我们在启动异步操作时提供的回调函数。

这就是JavaScript如何绕过单线程限制的方式。异步操作实际上是由运行时（`浏览器`、`NodeJS`等）处理的。与此同时，JavaScript可以做其他事情。

以下代码示例展示了通过发送HTTP请求到一个假REST API来使用回调函数：

```js
 1 function fetchUser(url) {
 2  const xhr = new XMLHttpRequest();
 3 
 4  xhr.addEventListener("load", function () {
 5    // check if the operation is complete
 6    if (xhr.readyState === 4) {
 7      if (xhr.status === 200) {
 8        // Request succeeded
 9        const data = JSON.parse(xhr.responseText);
10         console.log(data);
11       } else {
12         // Request failed
13         const error = new Error("Failed to fetch todo");
14         console.log(error);
15       }
16     }
17   });
18 
19   xhr.open("GET", url);
20   xhr.send();
21 }
22 
23 fetchUser("https://jsonplaceholder.typicode.com/todos/1");

```

您可以在下面的Replit中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/callbacks-example1" />`

传递给`addEventListener`方法的回调函数处理HTTP请求的结果。

不同的DOM事件，例如点击事件，也使用回调函数异步处理。回调作为事件处理程序注册，并在事件触发时稍后调用。

```js
1 const submitBtn = document.getElementById("submit");
2 
3 submitBtn.addEventListener("click", function (event) {
4   // code to handle the click event
5 });

```

同样，不同的定时器函数如 `setTimeout` 也提供了一个回调函数，旨在在指定时间过后被调用。

```js
1 setTimeout(function () {
2   console.log("logged after 2 seconds");
3 }, 2000);

```

你可以在下面的 Replit 中运行上面的代码：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/callbacks-example3” />`

一个常见的误解是提供给 `setTimeout` 的回调函数会在指定的时间过后立即被调用。我们在调用 `setTimeout` 时指定的时间是调用提供的回调函数后**最少**需要的时间。

在上面的代码示例中，我们指定了 2 秒（`2000` 毫秒）作为回调函数应该被调用的时间。但是，回调函数不会在正好 2 秒后被调用。想象一下，如果我们还有一个运行时间较长的循环，约需 4 秒才能完成。正如我们在上一课中讨论的，JavaScript 是单线程的，因此一个长时间运行的循环会阻塞主线程，这意味着提供给 `setTimeout` 的回调函数在循环结束之前无法执行。以下代码示例演示了这种情况：

```js
1 setTimeout(function () {
2   console.log("logged after approximately 4 seconds instead of 2");
3 }, 2000);
4 
5 const start = new Date();
6 
7 // takes approximately 4 seconds to execute
8 while (new Date() - start < 4000) {}

```

你可以在下面的 Replit 中运行上面的代码：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/callbacks-example4” />`

上面的代码示例显示 `setTimeout` 的回调或提供给 `setInterval` 函数的回调可能不会在指定时间后被调用；其他代码可能会阻塞它们的调用。

JavaScript 是单线程的；主线程一次只能执行一件事。目前，正在执行的代码无法中断以执行其他代码，比如上面代码示例中的 `setTimeout` 的回调函数。

回调函数是 JavaScript 中异步代码的核心。使用回调函数是可行的，但也带来了一些问题。

### 回调函数的问题

使用传统的回调方法处理异步代码会出现多种问题，使得有效使用回调变得困难。

#### 回调地狱

想象一下，如果多个异步操作需要按顺序启动，因为每个操作依赖于上一个操作的结果。为了解决这种情况，我们必须嵌套回调，这根据异步操作的数量，可能导致代码难以阅读和维护。以下代码示例展示了这一点：

```js
1 asyncOperation1((result1) => {
2   asyncOperation2(result1, (result2) => {
3     asyncOperation3(result2, (result3) => {
4       asyncOperation4(result3, (result4) => {
5         // ...more nested callbacks and operations
6       });
7     });
8   });
9 });

```

这被称为 `回调地狱` 或 `厄运金字塔`，因为每一层的嵌套创建了一个看起来像金字塔的结构。

看上面的代码示例，很容易想象，随着更多操作被添加到异步操作序列中，代码会变得越来越难以阅读。不仅难以阅读，而且难以维护和重构。请注意，上面的代码示例不包括任何错误处理；将其添加到上面的代码中，你将得到以下结果：

```js
 1 asyncOperation1((error1, result1) => {
 2  if (error1) {
 3    // handle error
 4  } else {
 5    asyncOperation2(result1, (error2, result2) => {
 6      if (error2) {
 7        // handle error
 8      } else {
 9        asyncOperation3(result2, (error3, result3) => {
10           if (error3) {
11             // handle error
12           } else {
13             asyncOperation4(result3, (error4, result4) => {
14               if (error4) {
15                 // handle error
16               } else {
17                 // ...more nested asynchronous operations and callbacks
18               }
19             });
20           }
21         });
22       }
23     });
24   }
25 });

```

上述代码符合其名称：“`Callback Hell`”。没有人愿意处理这样的代码。很难推理。在本模块的后续课程中，我们将看到如何使用`promises`和`async-await`语法重写相同的代码，使其更易读和易维护。

#### 错误处理

使用回调编写错误处理代码，如上所示，体验并不愉快。如上代码所示，我们需要在每个回调中处理错误，这可能导致错误处理逻辑的重复。没有一个中央地方可以捕获和处理所有异步操作的错误。

在本课程中，我们讨论了如何使用回调在JavaScript中编写异步代码。尽管有更好的替代方法，如`promises`和`async-await`来解决上述回调的问题，但回调仍然普遍使用。尽管`promises`解决了回调的问题，但它们仍然使用回调，但以一种更可管理的方式，帮助我们避免“回调地狱”。

我们已经知道，JavaScript语言是单线程的。在主线程上运行时间长的代码可以阻塞线程；在浏览器的情况下，阻塞主线程意味着浏览器无法响应用户交互，并且无法渲染UI的更改。这就是为什么当某些长时间运行的代码阻塞主线程时屏幕会冻结。在`NodeJs`的情况下，在应用服务器的上下文中，阻塞主线程意味着服务器无法处理进入的`HTTP`请求，直到主线程解除阻塞。

要解决JavaScript代码执行的单线程限制，在上一课程中已经讨论过，任何异步操作都在后台处理，与此同时，主线程可以做其他事情。

像`HTTP`请求这样的异步操作由浏览器在后台处理，当`HTTP`请求完成时，我们的`JavaScript`代码会使用我们在开始`HTTP`请求时提供的回调执行。同样，其他异步操作（如`NodeJS`中的文件处理）也是如此。每个`NodeJS`中的异步操作都由`NodeJS`的内部线程池或操作系统本身处理。

如果我们将主线程视为“JavaScript世界”，那么异步操作实际上发生在JavaScript世界之外。一旦操作完成，要重新回到JavaScript世界，就需要使用回调，这些回调被调用以执行`JavaScript`代码，以响应操作成功完成或失败。

简而言之，我们编写的代码在主线程上执行，仅仅是启动异步操作。主线程不需要等待操作完成，而是可以自由地做其他事情。异步操作在执行我们`JavaScript`代码的环境的后台中处理。这个环境可以是浏览器或像`NodeJS`这样的运行时。但是，如何将执行从后台带回到执行我们代码的主线程呢？这就是`event loop`进入画面的地方。

### 什么是事件循环？

`JavaScript`中的事件循环是一个抽象概念，旨在使其他人更容易理解。本课将旨在创建对事件循环的扎实理解。

事件循环帮助以非阻塞的方式执行异步操作。当后台中的异步操作完成以执行我们在启动异步操作时提供的`JavaScript`回调时，需要将其推入调用堆栈。

`The call stack`是一个堆栈数据结构，用于跟踪当前正在执行的代码。每个函数调用都作为一个堆栈帧被添加到堆栈中。当函数执行结束时，该帧会从堆栈中弹出。

让我们通过以下代码示例理解事件循环：

```js
 1 setTimeout(() => {
 2  console.log("hello world");
 3 }, 2000);
 4 
 5 console.log("after setTimeout");
 6 
 7 // output:
 8 // ------
 9 // after setTimeout
10 // hello world

```

您可以在下面的`Replit`中运行上面的代码：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/event-loop-example1” />`

上面的代码在`setTimeout`的回调中记录“after setTimeout”在“hello world”之前。以下步骤解释了上面的代码是如何执行的：

1.  要执行代码，会创建一个任务并将其推入调用堆栈。这通常被称为“全局执行上下文”。

1.  一旦代码执行开始，第一件事就是调用`setTimeout`函数，传入一个将在大约2秒后被调用的回调。调用`setTimeout`会在后台启动一个计时器，该计时器将在我们代码示例中的2秒后到期。在此期间，主线程继续执行代码，而不是等待计时器到期。这就是为什么“after setTimeout”在“hello world”之前被记录的原因。

1.  接下来，执行`console.log`，在控制台上记录“after setTimeout”。

1.  此时，我们代码的同步执行已结束。因此，为执行代码而创建的任务（步骤 1）从调用栈中弹出。现在，JavaScript 准备好执行任何已调度的回调。这个点很重要：`在代码的同步执行结束之前，无法调用任何异步回调`。请记住，主线程一次只能执行一件事，并且当前执行的代码不能被中断。

1.  在同步执行结束后，假设此时定时器已经到期（实际上，我们的代码执行将在2秒之前结束）。一旦定时器到期，一个任务被排入`任务队列`以执行`setTimeout`的回调。`任务队列`是不同任务排队的地方，直到它们可以被推入调用栈并执行。

1.  `事件循环`是处理`任务队列`中任务并将每个任务推送到调用栈以执行的实体。任务按照它们在`任务队列`中排队的顺序进行处理。在我们的例子中，`任务队列`中只有一个任务。这个任务被推入调用栈，但`事件循环`只有在调用栈为空时才会将任务推入调用栈。在我们的例子中，调用栈为空，因此可以执行`setTimeout`的回调。因此，“hello world”被记录在控制台上。

`事件循环`的作用，如上述步骤所述，是在调用栈为空且`任务队列`中有一个或多个等待执行的任务时处理`任务队列`中的任务。因此，`事件循环`是一个允许异步代码以非阻塞方式在JavaScript中执行的实体。可以将`事件循环`视为一个不断检查是否有等待执行的任务的循环。

`事件循环`连接了两个世界：“JavaScript世界”，即我们的代码执行的地方，以及“后台世界”，即异步操作实际执行的地方。

上述步骤可以在以下图像中可视化：

![函数参数作用域](images/module_09----lesson_09.03----public----assets----__event-loop-visualization.gif)

`函数参数作用域`

花时间准确理解幕后发生的事情。定时器故意显示为超过2秒，以便使可视化更易于理解。在查看图像之前理解上述步骤，将使理解我们的代码示例的执行变得容易。

任何用户交互，例如点击事件，都需要调度一个任务；定时函数的回调执行（如`setTimeout`）也是如此。任务会被排入`任务队列`，直到`事件循环`处理它们。`任务队列`也被称为`事件队列`或`回调队列`。

事件循环在每个单独的轮次中处理一个任务，通常称为“事件循环滴答”或简称“滴答”。下一个任务在事件循环的下一个轮次或滴答中处理。浏览器可以选择在任务之间渲染UI更新。

事件循环可以有多个任务源，浏览器在事件循环的每个滴答中决定从哪个源处理任务。另一个队列被称为`微任务队列`，我们将在本模块稍后讨论。事件循环也处理微任务，但事件循环处理任务和微任务的方式有所不同。差异将在我们讨论微任务队列时变得清晰。

在本课中，我们讨论了事件循环是什么以及任务是如何处理的：每个事件循环的每个“滴答”处理一个任务。

#### 可视化事件循环的工具

以下是一个很好的工具，可以使用我们的代码可视化事件循环的工作原理：

+   [`放大镜`](http://latentflip.com/loupe)

#### 深入阅读

以下资源被推荐以进一步加深我们对事件循环的理解：

+   [`事件循环 (MDN)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Event_loop)`

+   [`事件循环到底是什么？| Philip Roberts（youtube视频）](https://www.youtube.com/watch?v=8aGhZQkoFbQ)`

+   [`Jake Archibald 关于网页浏览器事件循环、setTimeout、微任务、requestAnimationFrame（youtube视频）](https://www.youtube.com/watch?v=cCOL7MC4Pl0)`

在`ES2015`中引入的承诺改变了我们处理JavaScript中异步代码的方式。承诺旨在解决我们在回调中讨论的问题。

承诺代表一个对象，它充当一个通常由异步操作产生的值的`占位符`。换句话说，承诺对象代表异步操作的成功完成或失败。在初学者中普遍存在一个误解，认为承诺使我们的代码异步；实际上并非如此。将承诺视为一种通知机制，它通知我们某个`已经`是异步操作的成功或失败。承诺封装异步操作，并允许我们在异步操作成功完成或失败时执行代码。这就是承诺所做的一切。没有更多，没有更少。它的唯一目的是观察异步操作，并在该操作完成时通知我们。

在学习如何创建承诺对象之前，让我们首先了解如何使用内置的`fetch`函数处理承诺，该函数允许我们从浏览器中运行的JavaScript代码发出HTTP请求。

当调用`fetch`函数时，函数不会使调用代码等待HTTP请求完成，而是返回一个承诺对象。我们可以将回调函数与返回的承诺对象关联，以便在HTTP请求完成时执行代码。我们仍然使用回调与承诺，但在本模块之前的课程中讨论的与回调相关的问题在使用承诺时不存在。与回调相比，承诺提供了一种干净且结构化的方式来处理JavaScript中的异步操作。

```js
1 const p1 = fetch(/* some url */);

```

`fetch`函数返回的承诺可以看作是`fetch`函数`承诺`我们在HTTP请求未来某个时间完成时提供一个值。在此期间，主线程可以自由执行其他操作。

我们可以对返回的承诺做什么？我们可以在网络请求完成时注册与承诺对象的回调。我们可以注册不同的回调以处理网络请求的成功或失败。

### 承诺状态

承诺在其生命周期中可以处于以下三种状态之一：

+   `pending`：承诺通常在创建时的初始状态。这表示与承诺关联的异步操作正在进行中。

+   `fulfilled`：意味着与承诺关联的异步操作已成功完成。

+   `rejected`：意味着与承诺关联的异步操作失败了。

在承诺的生命周期中，它的状态从`pending`变为`fulfilled`或`rejected`。承诺的状态保存在名为`[[[PromiseState]]]`的隐藏内部插槽中（[链接](https://262.ecma-international.org/14.0/#table-internal-slots-of-promise-instances)）。

处于`pending`状态的承诺被视为`unsettled`。一旦承诺从`pending`状态转换为`fulfilled`或`rejected`状态，就被认为是`settled`。

### 承诺实例方法

我们可以在承诺实例上调用的三种实例方法：

+   `Promise.prototype.then()`

+   `Promise.prototype.catch()`

+   `Promise.prototype.finally()`

#### `then` 方法

`then`方法用于注册一个回调函数，该函数在承诺被满足时异步调用，即被承诺包装的异步操作成功完成时。此方法允许我们在异步操作成功完成时执行代码。考虑以下代码示例：

```js
1 const p1 = fetch(/* some url */);
2 
3 p1.then((response) => {
4   // code to execute if the promise fulfills
5 });

```

`then` 方法接受两个回调函数作为参数：`fulfillment handler`和`rejection handler`。`fulfillment handler`是第一个参数，如上面的代码示例所示。`rejection handler`是可选的第二个参数，如果调用`then`方法的承诺被拒绝，则会调用它。

```js
 1 const p1 = fetch(/* some url */);
 2 
 3 p1.then(
 4  (response) => {
 5    // code to execute if the promise fulfills
 6  },
 7  (error) => {
 8    // code to execute if the promise is rejected
 9  }
10 );

```

满足处理程序将异步操作的结果作为参数传递。换句话说，满足处理程序接收的是承诺被满足时的值。在HTTP请求的情况下，承诺以服务器响应作为满足，因此满足处理程序接收服务器响应作为参数。另一方面，如果承诺被拒绝，拒绝处理程序将接收拒绝原因作为参数。

#### `catch` 方法

我们在上一节中了解到，可以将拒绝处理程序作为第二个参数传递给`then`方法来处理承诺拒绝。还有另一种注册拒绝处理程序的选项，那就是通过`catch`方法。我们可以在承诺上调用`catch`方法来注册拒绝处理程序，而不是将拒绝处理程序传递给`then`方法。

```js
1 const p1 = fetch(/* some url */);
2 
3 p1.then((response) => {
4   // code to execute if the promise fulfills
5 });
6 
7 p1.catch((error) => {
8   // code to execute if the promise is rejected
9 });

```

`catch`方法类似于只使用拒绝处理程序调用的`then`方法，如下所示：

```js
1 p1.then(null, (error) => {
2   // code to execute if the promise is rejected
3 });

```

然而，使用`catch`方法注册拒绝处理程序比使用`then`方法的第二个参数更为常见。

#### `finally` 方法

想象一个场景，我们希望向服务器发送HTTP请求，而在请求进行时，我们向用户显示一个加载指示器以表明数据正在加载。当请求完成时，无论是成功还是失败，我们都希望隐藏加载指示器。为了实现这一点，我们必须在满足和拒绝处理程序中重复隐藏加载指示器的代码，如下所示的代码示例所示：

```js
 1 const p1 = fetch(/* some url */);
 2 
 3 p1.then((response) => {
 4  // hide the loading spinner
 5  document.getElementById("spinner").style.display = "none";
 6 });
 7 
 8 p1.catch((error) => {
 9  // hide the loading spinner
10   document.getElementById("spinner").style.display = "none";
11 });

```

我们希望避免代码重复，而`finally`方法可以帮助我们消除代码重复。`finally`方法允许我们在承诺满足或拒绝时执行代码。与`then`和`catch`方法一样，`finally`方法也接受一个回调函数，该函数在承诺满足和拒绝后异步调用。传递给`finally`方法的回调是执行代码的理想之地，无论异步操作是否失败或成功完成。我们可以将上述代码重构如下：

```js
 1 const p1 = fetch(/* some url */);
 2 
 3 p1.then((response) => {
 4  // code to execute if the promise fulfills
 5 });
 6 
 7 p1.catch((error) => {
 8  // code to execute if the promise is rejected
 9 });
10 
11 p1.finally(() => {
12   // hide the loading spinner
13   document.getElementById("spinner").style.display = "none";
14 });

```

与 `then` 和 `catch` 方法的回调不同，传递给 `finally` 方法的回调不接收任何参数。

### 创建 Promise

我们可以使用 `Promise` 构造函数创建新的 Promise 对象，如下所示：

```js
1 const p = new Promise((resolve, reject) => {
2   // initiate asynchronous operation...
3 });

```

`Promise` 构造函数接受一个回调函数作为参数，该参数被称为 `executor` 函数，并在 `同步` 模式下被调用以创建 Promise 对象。人们常常错误地假设执行函数中的任何代码都是异步执行的，但事实并非如此。执行函数是同步调用的，以创建 Promise 对象。执行函数中的代码应该是启动某个异步操作的任何代码。新创建的 Promise 对象将观察该异步操作。Promise 对象将通知我们执行函数内部启动的异步操作的成功或失败。

异步操作是如何与新创建的 Promise 关联的？通过执行函数作为参数接收的 `resolve` 和 `reject` 函数。参数可以使用不同的名称，但通常将它们命名为 `resolve` 和 `reject` 以明确其目的。`resolve` 函数用于解决或满足 Promise，而 `reject` 函数用于拒绝 Promise。让我们看一个具体的例子，以澄清如何创建一个 Promise 对象，它包装在异步操作周围，并根据异步操作的成功或失败进行解析或拒绝。

```js
 1 const p = new Promise((resolve, reject) => {
 2  const xhr = new XMLHttpRequest();
 3 
 4  xhr.addEventListener("load", function () {
 5    // check if operation is complete
 6    if (xhr.readyState === 4) {
 7      if (xhr.status === 200) {
 8        // Request succeeded
 9        const data = JSON.parse(xhr.responseText);
10         // call the resolve function with the data
11         // as an argument to fulfill the promise
12         // with the data
13         resolve(data);
14       } else {
15         // Request failed
16         const error = new Error("Failed to fetch todo");
17         // call the reject function with the rejection
18         // reason or an error as an argument
19         reject(error);
20       }
21     }
22   });
23 
24   const url = "https://jsonplaceholder.typicode.com/todos/1";
25   xhr.open("GET", url);
26   xhr.send();
27 });
28 
29 // register fulfillment handler
30 p.then((todo) => {
31   console.log(todo);
32 });
33 
34 // register rejection handler
35 p.catch((error) => {
36   console.log(error.message);
37 });

```

你可以在下面的 Replit 中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/promises-example9" />`

上面的代码示例展示了如何将一个 Promise 对象包装在异步操作中，并在异步操作成功或失败时进行解析或拒绝。针对 Promise 被满足或拒绝的情况，相应的处理程序（满足或拒绝）会异步调用。

重要的是要注意，Promise 不会被满足或拒绝，直到在执行函数中调用 `resolve` 或 `reject` 函数。因此，任何注册的满足或拒绝处理程序在 Promise 被解决之前都不会被调用。

上面的代码示例可能没有让你看到 Promise 是如何改善传统的使用回调处理异步代码的方法，但等到我们在本模块即将到来的课程中讨论 Promise 链和 `async-await` 语法时再说。这两个主题将帮助你理解 Promise 如何解决回调的两个主要问题：回调地狱和错误处理。

### 使用 Promise 与基于回调的 API

如果你注意到上一节的代码示例，我们只是将一个 Promise 包装在基于回调的 `XMLHttpRequest` API 周围。我们这样做是为了能够通过 Promise 与其进行交互。

与我们上面做的类似，我们可以将任何基于回调的 API 转换为基于 Promise 的 API。我们需要做的就是将基于回调的代码放入执行函数中，并在适当的位置调用 `resolve` 和 `reject` 函数来完成或拒绝该 Promise。以下是一个将 Promise 包裹在 `setTimeout` 周围以在代码中添加人为延迟的示例：

```js
 1 function timeout(delayInSeconds) {
 2  const delayInMilliseconds = delayInSeconds * 1000;
 3 
 4  return new Promise((resolve) => {
 5    setTimeout(() => resolve(), delayInMilliseconds);
 6  });
 7 }
 8 
 9 timeout(2).then(() => {
10   console.log("done"); // logged after 2 seconds
11 });

```

你可以在下面的 Replit 中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/promises-example10" />`

在上面的代码示例中，我们将 `setTimeout` 包裹在一个 Promise 中，以在代码中添加人为延迟。要在指定延迟（我们上面的代码中为 2 秒）后解析 Promise，我们在 `setTimeout` 的回调函数内调用 `resolve` 函数。请注意，我们没有调用或使用 `reject` 函数，因为我们不需要它来拒绝 Promise。我们只是希望在指定延迟后完成 Promise。

### 承诺规范

[Promises/A+](https://promisesaplus.com/) 是一个标准，定义了 JavaScript 中 Promise 的行为。它确保不同环境中 Promise 的不同实现符合规范中定义的标准行为，以确保不同环境中 Promise 行为的一致性。

### Promise 与 `thenable`

如果你阅读了承诺规范，你会发现多次提到“`thenable`”这个词。`thenable` 是任何定义了名为 `then` 方法的对象，但不是 Promise。它是一个通用术语，指具有名为 `then` 方法的对象。由于 Promise 具有名为 `then` 的方法，我们可以说所有的 Promise 都是 `thenables`，但反之不成立：并非每个 `thenable` 都是 Promise。

总结区别，`thenable` 是一个具有 `then` 方法的对象，而 `promise` 是一个具有符合 [Promises/A+](https://promisesaplus.com/) 规范的 `then` 方法的对象。

在上一课中，我们讨论了以下 Promise 的实例方法：

+   `Promise.prototype.then()`

+   `Promise.prototype.catch()`

+   `Promise.prototype.finally()`

我们讨论了这些方法各自可以让我们做什么，但我们没有讨论的是这些方法返回的内容。它们的返回值很重要，因为它允许进行承诺链式调用，这也是本课的主题。

每个 Promise 的实例方法返回一个新的 Promise，这使我们能够创建方法调用链，有效地创建异步操作链。承诺链式调用帮助解决我们在使用回调时面临的两个主要问题：“回调地狱”和错误处理。

以下代码示例展示了我们如何在 `fetch` 函数返回的 Promise 上注册完成和拒绝处理程序：

```js
 1 const p = fetch(/* some url */);
 2 
 3 // register a fulfillment handler
 4 p.then((response) => {
 5  // code...
 6 });
 7 
 8 // register a rejection handler
 9 p.catch((error) => {
10   // code...
11 });

```

由于每个 Promise 实例方法返回一个新的 Promise，我们可以将上述代码重写如下：

```js
1 fetch(/* some url */)
2   .then((response) => {
3     // code...
4   })
5   .catch((error) => {
6     // code...
7   });

```

重构后的代码实现了与第一个代码示例相同的结果，但从技术上讲，第一个代码示例与重构后的代码是不同的。在第一个代码示例中，拒绝处理程序是在`fetch`函数返回的`promise`上注册的，而在重构后的代码中，拒绝处理程序是在`then`方法返回的`promise`上注册的。重构后的代码中的`promise`链可以分成不同的部分，如下所示，以便更容易理解：

```js
1 const pFetch = fetch(/* some url */);
2 
3 const pThen = pFetch.then((response) => {
4   // code...
5 });
6 
7 const pCatch = pThen.catch((error) => {
8   // code...
9 });

```

注意已经注册了满足和拒绝处理程序的`promise`。满足处理程序是在`fetch`函数返回的`promise`上注册的，但与第一个代码示例不同，拒绝处理程序是在`then`方法返回的`promise`上注册的。那么，这是否意味着如果`fetch`函数返回的`promise`被拒绝，就没有注册处理拒绝的处理程序？不，注册在`pThen`的`promise`上的拒绝处理程序将处理拒绝。要理解它是如何工作的，我们必须理解`promise`链是如何工作的。

本节的进一步代码示例将使用以下函数，该函数模拟一个大约需要两秒钟才能完成的HTTP请求：

```js
 1 function fakeRequest(isSuccessRequest = true) {
 2  return new Promise((resolve, reject) => {
 3    setTimeout(() => {
 4      if (isSuccessRequest) {
 5        const data = { name: "John Doe", favouriteLanguage: "JavaScript" };
 6        resolve(data);
 7      } else {
 8        const error = new Error("request failed");
 9        reject(error);
10       }
11     }, 2000);
12   });
13 }

```

这个函数将使我们更容易理解`promise`链。该函数接受一个布尔参数，指定我们是否希望我们的假请求被满足或拒绝。该参数的默认值为`true`，因此如果我们希望请求失败，只需传递参数即可。在函数内部，返回一个包装在`setTimeout`中的`promise`，以模拟一个大约需要两秒钟才能完成的请求。在定时器到期后，`promise`会被满足或拒绝，具体取决于`isSuccessRequest`参数的值。

定义了`fakeRequest`函数后，让我们深入`promise`链的世界。

### `then` `promise`

在一个`promise`上调用`then`方法会在该`promise`上注册一个满足处理程序。`then`方法本身返回一个新的`promise`，该`promise`与调用`then`方法的原始`promise`不同。

```js
1 const pRequest = fakeRequest();
2 
3 const pThen = pRequest.then((response) => {
4   console.log(response);
5 });
6 
7 console.log(pThen === pRequest); // false

```

你可以在下面的Replit中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/promise-chaining-example5" />`

`then`方法返回的`promise`根据以下两个问题来满足或拒绝：

+   调用`then`方法的`promise`会发生什么？在我们的案例中，`then`方法是在`pRequest`的`promise`上调用的。

+   从传递给`then`方法的满足或拒绝处理程序返回的是什么？哪个处理程序会影响`then`方法返回的`promise`取决于在调用`then`方法的原始`promise`解决时哪个处理程序被调用。

记住上述两个问题，让我们讨论可能影响`then`方法返回的`promise`的不同场景：

#### 场景1：原始`promise`被满足

如果调用`then`方法的原始承诺被实现，则`then`方法返回的承诺取决于实现处理程序内部发生的事情。以下是实现处理程序可以执行的不同操作，这些操作会影响`then`方法返回的承诺：

+   如果注册了实现处理程序，并且它返回的值不是一个承诺或可then的对象，则`then`方法返回的承诺将以该返回值完成。

    ```js
     1 // pRequest will be fulfilled
     2 const pRequest = fakeRequest();
     3 
     4 const pThen = pRequest.then((response) => {
     5  console.log(response);
     6  return "success";
     7 });
     8 
     9 pThen.then((data) => {
    10   console.log(data); // success
    11 });

    ```

你可以在下面的Replit中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/promise-chaining-example6" />`

+   如果实现处理程序没有显式返回任何值，则`then`方法返回的承诺以`undefined`作为实现值完成。

    ```js
     1 // pRequest will be fulfilled
     2 const pRequest = fakeRequest();
     3 
     4 const pThen = pRequest.then((response) => {
     5  console.log(response);
     6 });
     7 
     8 pThen.then((data) => {
     9  console.log(data); // undefined
    10 });

    ```

你可以在下面的Replit中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/promise-chaining-example7" />`

+   如果在一个承诺上调用`then`方法但没有提供实现处理程序，则`then`方法返回的承诺将以与原始承诺相同的实现值完成。

    ```js
     1 // pRequest will be fulfilled
     2 const pRequest = fakeRequest();
     3 
     4 // fulfillment handler not provided
     5 const pThen = pRequest.then();
     6 
     7 pThen.then((data) => {
     8  // logs the value with which pRequest fulfilled
     9  console.log(data);
    10 });

    ```

你可以在下面的Replit中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/promise-chaining-example8" />`

+   如果实现处理程序抛出任何值或错误，则`then`方法返回的承诺将以抛出的值作为拒绝原因或值被拒绝。

    ```js
     1 // pRequest will be fulfilled
     2 const pRequest = fakeRequest();
     3 
     4 const pThen = pRequest.then((response) => {
     5  throw new Error("something bad happened");
     6 });
     7 
     8 pThen.catch((error) => {
     9  console.log(error.message); // something bad happened
    10 });

    ```

你可以在下面的Replit中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/promise-chaining-example9" />`

+   如果实现处理程序返回一个承诺，则`then`方法返回的承诺将被*解析*为实现处理程序返回的承诺。一个承诺被*解析为另一个承诺*意味着一个承诺（我们称之为`p1`）的命运取决于另一个承诺（我们称之为`p2`）。如果`p2`被实现，`p1`也将以相同的实现值被实现。如果`p2`被拒绝，`p1`也将以相同的拒绝值被拒绝。承诺`p1`将等待`p2`解决后再解决，最终与`p2`达到相同的命运。

    ```js
     1 // pRequest will be fulfilled
     2 const pRequest = fakeRequest();
     3 
     4 const pThen = pRequest.then((response) => {
     5  // return a promise that will be fulfilled
     6  return fakeRequest();
     7 });
     8 
     9 pThen.then((response) => {
    10   // logs the fulfillment value of
    11   // promise returned from the fulfillment
    12   // handler of pRequest promise
    13   console.log(response);
    14 });

    ```

你可以在下面的Replit中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/promise-chaining-example10" />`

在上面的代码示例中，`then`方法返回的承诺`pThen`通过`pRequest`承诺的实现处理程序返回的承诺被*解析*。

#### 场景 2：原始承诺被拒绝

如果调用`then`方法的原始承诺被拒绝，则`then`方法返回的承诺取决于以下场景：

+   如果只将实现处理程序传递给`then`方法，则`then`方法返回的承诺也将以与原始承诺被拒绝时相同的拒绝原因或值被拒绝。

    ```js
     1 // pRequest will get rejected
     2 const pRequest = fakeRequest(false);
     3 
     4 const pThen = pRequest.then((response) => {
     5  console.log(response);
     6 });
     7 
     8 pThen.catch((error) => {
     9  console.log(error.message); // request failed
    10 });

    ```

你可以在下面的Replit中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/promise-chaining-example11" />`

+   如果将拒绝处理程序传递给`then`方法，那么`then`方法返回的承诺将取决于拒绝处理程序内部发生的事情。这在履行处理程序的情况下工作类似：

    +   如果拒绝处理程序返回一个非承诺值，则`then`方法返回的承诺将以拒绝处理程序返回的值被兑现。

    +   如果拒绝处理程序没有明确返回任何值，那么`then`方法返回的承诺将以`undefined`作为满足值被兑现。

    +   如果在原始承诺上调用`then`方法，但没有提供拒绝处理程序，则`then`方法返回的承诺将以与原始承诺相同的拒绝值被拒绝。

    +   如果拒绝处理程序抛出任何值或错误，则`then`方法返回的承诺将以抛出的值作为拒绝原因或值被拒绝。

    +   如果拒绝处理程序返回一个承诺，则`then`方法返回的承诺将被解析为拒绝处理程序返回的承诺，就像之前讨论的履行处理程序的情况一样。

现在我们已经讨论了`then`方法返回的承诺在不同场景下是如何解决的，接下来我们将讨论`catch`方法返回的承诺。

### 捕获承诺

`catch`方法用于为调用它的承诺注册拒绝处理程序。与`then`方法一样，`catch`方法也返回一个新的承诺，并且与`then`方法的承诺一样，`catch`方法返回的承诺的解决情况取决于以下两个问题：

+   在调用`catch`方法的承诺上发生了什么？

+   传递给`catch`方法的拒绝处理程序返回了什么？

#### 场景 1：原始承诺被兑现

假设调用`catch`方法的原始承诺已经兑现。在这种情况下，使用`catch`方法注册的拒绝处理程序不会被调用，`catch`方法返回的承诺将以与原始承诺相同的满足值被兑现。

```js
 1 // pRequest will be fulfilled
 2 const pRequest = fakeRequest();
 3 
 4 const pCatch = pRequest.catch((error) => {
 5  console.log(error.message);
 6 });
 7 
 8 pCatch.then((data) => {
 9  // logs the fulfillment value with
10   // which pRequest promise fulfilled
11   console.log(data);
12 });

```

您可以在下面的Replit中运行上述代码：

<ReplitEmbed src="https://replit.com/@newlineauthors/promise-chaining-example12" />

#### 场景 2：原始承诺被拒绝

使用`catch`处理程序注册的拒绝处理程序在调用`catch`方法的原始承诺被拒绝时被调用。如果原始承诺被拒绝，那么`catch`方法返回的承诺，就像`then`方法返回的承诺一样，取决于拒绝处理程序内部发生的事情：

+   如果拒绝处理程序返回一个非承诺值，则`catch`方法返回的承诺将以拒绝处理程序返回的值被兑现。

    ```js
     1 // pRequest will get rejected
     2 const pRequest = fakeRequest(false);
     3 
     4 const pCatch = pRequest.catch((error) => {
     5  return "default value";
     6 });
     7 
     8 pCatch.then((data) => {
     9  console.log(data); // default value
    10 });

    ```

您可以在下面的Replit中运行上述代码：

<ReplitEmbed src="https://replit.com/@newlineauthors/promise-chaining-example13" />

+   如果拒绝处理程序没有显式返回任何值，则`catch`方法返回的承诺将以`undefined`作为满足值被兑现。

    ```js
     1 // pRequest will get rejected
     2 const pRequest = fakeRequest(false);
     3 
     4 const pCatch = pRequest.catch((error) => {
     5  console.log(error.message); // request failed
     6 });
     7 
     8 pCatch.then((data) => {
     9  console.log(data); // undefined
    10 });

    ```

您可以在下面的Replit中运行上述代码：

<ReplitEmbed src="https://replit.com/@newlineauthors/promise-chaining-example14" />

+   如果在原始承诺上调用`catch`方法，但未提供拒绝处理程序，则`catch`方法返回的承诺将以与原始承诺相同的拒绝值被拒绝。

    ```js
     1 // pRequest will get rejected
     2 const pRequest = fakeRequest(false);
     3 
     4 // rejection handler not registered
     5 const pCatch = pRequest.catch();
     6 
     7 pCatch.catch((error) => {
     8  // logs the rejection value of the
     9  // original pRequest promise
    10   console.log(error.message); // request failed
    11 });

    ```

    您可以在下面的Replit中运行上述代码：

<ReplitEmbed src="https://replit.com/@newlineauthors/promise-chaining-example15" />

+   如果拒绝处理程序抛出任何值或错误，则`catch`方法返回的承诺将以抛出的值作为拒绝原因或值被拒绝。

    ```js
     1 // pRequest will get rejected
     2 const pRequest = fakeRequest(false);
     3 
     4 const pCatch = pRequest.catch((error) => {
     5  throw error;
     6 });
     7 
     8 pCatch.catch((error) => {
     9  console.log(error.message); // request failed
    10 });

    ```

您可以在下面的Replit中运行上述代码：

<ReplitEmbed src="https://replit.com/@newlineauthors/promise-chaining-example16" />

+   如果拒绝处理程序返回一个承诺，则`catch`方法返回的承诺将解析为拒绝处理程序返回的承诺，这与之前讨论的满足处理程序的情况相同。

    ```js
     1 // pRequest will get rejected
     2 const pRequest = fakeRequest(false);
     3 
     4 const pCatch = pRequest.catch((error) => {
     5  // return a promise that will get fulfilled
     6  return fakeRequest();
     7 });
     8 
     9 pCatch.then((data) => {
    10   // logs the fulfillment value of
    11   // promise returned from the rejection
    12   // handler of pRequest promise
    13   console.log(data);
    14 });

    ```

您可以在下面的Replit中运行上述代码：

<ReplitEmbed src="https://replit.com/@newlineauthors/promise-chaining-example17" />

### `finally`承诺

`finally`方法用于注册一个回调函数，该函数在承诺解决后异步调用。无论调用`finally`方法的承诺是被满足还是被拒绝，传递给`finally`方法的回调都会被调用。与`then`和`catch`方法一样，`finally`方法也返回一个新的承诺，而`finally`方法返回的承诺的解决情况取决于以下两个问题：

+   调用`finally`方法的承诺会发生什么？

+   传递给`finally`方法的回调函数返回了什么？

#### 场景 1：原始承诺被兑现

假设调用`finally`方法的原始承诺已被兑现。在这种情况下，`finally`方法返回的承诺也将以与原始承诺相同的满足值被兑现，前提是满足以下条件：

+   `finally`回调不会抛出错误或值。

+   `finally`回调不会返回一个被拒绝的 promise 或一个最终被拒绝的 promise。

```js
 1 // pRequest will get fulfilled
 2 const pRequest = fakeRequest();
 3 
 4 const pFinally = pRequest.finally(() => {
 5  console.log("finally called");
 6 });
 7 
 8 pFinally.then((data) => {
 9  // logs the fulfillment value of
10   // the original pRequest promise
11   console.log(data);
12 });

```

这里是 Replit 中的代码：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/promise-chaining-example18” />`

注意，`finally`回调没有明确返回任何值，但`finally` promise 以原始`pRequest` promise 的履行值得到履行。这种行为与`then`和`catch`方法的行为不同；如果它们的回调隐式返回`undefined`，那么它们的 promise 将以值`undefined`得到履行。

#### 场景 2：原始 promise 被拒绝

假设调用`finally`方法的原始 promise 被拒绝。在这种情况下，`finally`方法返回的 promise 也会以与原始 promise 相同的拒绝值被拒绝，前提是满足之前提到的相同两个条件：

+   `finally`回调不会抛出错误或值。

+   `finally`回调不会返回被拒绝的 promise 或最终被拒绝的 promise。

```js
 1 // pRequest will get rejected
 2 const pRequest = fakeRequest(false);
 3 
 4 const pFinally = pRequest.finally(() => {
 5  console.log("finally called");
 6 });
 7 
 8 pFinally.catch((error) => {
 9  // logs the rejection value of
10   // the original pRequest promise
11   console.log(error.message);
12 });

```

下面是 Replit 中的代码：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/promise-chaining-example19” />`

#### 场景 3：遮蔽原始 promise 的结算

与`then`和`catch`方法不同，`finally`回调的返回值被忽略，`finally`方法返回的 promise 简单地与调用它的原始 promise 同样的命运；如果原始 promise 被满足，`finally` promise 也会被满足；如果原始 promise 被拒绝，`finally` promise 也会被拒绝。

然而，`finally`方法的前两个场景中提到的两个条件是这个规则的例外。如果`finally`回调抛出错误，`finally` promise 将以抛出的值被拒绝。

```js
 1 // pRequest will get rejected
 2 const pRequest = fakeRequest(false);
 3 
 4 const pFinally = pRequest.finally(() => {
 5  throw new Error("finally error");
 6 });
 7 
 8 pFinally.catch((error) => {
 9  console.log(error.message); // finally error
10 });

```

你可以在下面的 Replit 中运行上述代码：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/promise-chaining-example20” />`

`finally`方法的拒绝遮蔽了原始`pRequest` promise 的拒绝。如果`pRequest` promise 被满足，也会发生同样的情况。从`finally`回调中抛出错误会简单地拒绝`finally` promise，而不管原始 promise 发生了什么。

同样，从`finally`回调返回一个被拒绝的 promise 也会拒绝`finally` promise，而不管原始 promise 发生了什么。

```js
 1 // pRequest will get fulfilled
 2 const pRequest = fakeRequest();
 3 
 4 const pFinally = pRequest.finally(() => {
 5  // return a promise that will get rejected
 6  return fakeRequest(false);
 7 });
 8 
 9 pFinally.catch((error) => {
10   // logs the rejection value of the
11   // promise returned from the finally callback
12   console.log(error.message); // request failed
13 });

```

你可以在下面的 Replit 中运行上述代码：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/promise-chaining-example21” />`

### 理解 promise 链接

我们已经讨论了每个 promise 实例方法返回的 promise 可以拒绝或满足的每种场景。最后，我们可以理解 promise 链是如何工作的。我们将通过一系列示例来巩固我们的理解。

#### 示例 1

```js
 1 fakeRequest()
 2  .then((response) => {
 3    console.log(response);
 4    return "hello world";
 5  })
 6  .then((data) => {
 7    console.log(data);
 8    return "123";
 9  })
10   .catch((error) => {
11     console.log(error.message);
12   });

```

你可以在下面的 Replit 中运行上述代码：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/promise-chaining-example22” />`

你在上述代码示例中预期的输出是什么？请记住，每个实例方法返回一个新的 promise，它的满足或拒绝取决于两个因素：

+   调用该方法的原始 promise 会发生什么？

+   什么会发生在该方法的回调函数内部？

考虑到上述不同场景，这些场景可以使每个 promise 实例方法返回的 promise 被满足或拒绝，尝试通过猜测上述代码的输出测试你的理解。下面是对上述代码输出的解释：

1.  从承诺链的顶部开始，`fakeRequest`函数返回的承诺将被履行，从而调用其使用第一个`then`方法的首次调用注册的履行处理程序。因此，以下内容将在控制台上记录：

    ```js
    1 {
    2   favouriteLanguage: "JavaScript",
    3   name: "John Doe"
    4 }

    ```

1.  `fakeRequest`函数返回的承诺已解决。链中的下一个承诺是由第一个`then`方法调用返回的承诺。当原始承诺得到履行时，第一个`then`承诺现在依赖于其回调函数内部发生的事情。由于它返回字符串“hello world”，第一个`then`承诺将以“hello world”作为履行值来履行。

    结果是，它的履行处理程序被调用，该处理程序是使用第二个`then`方法调用注册的。第一个`then`承诺的履行处理程序将其履行值，即“hello world”，作为参数接收。这导致“hello world”被记录到控制台。目前的控制台输出如下所示：

    ```js
    1 {
    2  favouriteLanguage: "JavaScript",
    3  name: "John Doe"
    4 }
    5 
    6 "hello world"

    ```

1.  此时，承诺链中的两个承诺已解决。链中的下一个承诺是由第二个`then`方法返回的。与第一个`then`方法一样，第二个`then`方法返回的承诺依赖于其被调用的原始承诺，即第一个`then`方法返回的承诺。当原始承诺得到履行时，第二个`then`承诺现在依赖于其回调函数内部发生的事情。它的回调返回字符串“123”。因此，第二个`then`承诺以“123”作为其履行值来履行。

    但是没有为第二个`then`承诺注册履行处理程序；只有使用`catch`方法注册了拒绝处理程序。因此，没有履行处理程序会在响应第二个`then`方法的履行时被调用。承诺链移动到链中的最后一个承诺，即`catch`方法返回的承诺。

1.  `catch`方法返回的承诺是在第二个`then`方法返回的承诺上调用的。当第二个`then`承诺得到履行时，`catch`承诺也会以与第二个`then`承诺相同的履行值得到履行。但是，没有为`catch`承诺注册履行或拒绝处理程序，因此其履行被简单忽略。代码的最终输出如下所示：

    ```js
    1 {
    2  favouriteLanguage: "JavaScript",
    3  name: "John Doe"
    4 }
    5 
    6 "hello world"

    ```

#### 示例 2

```js
 1 fakeRequest()
 2  .then((response) => {
 3    console.log(response);
 4    return fakeRequest();
 5  })
 6  .then((data) => {
 7    console.log(data);
 8  })
 9  .catch((error) => {
10     console.log(error.message);
11   });

```

你可以在下面的 Replit 中运行上述代码：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/promise-chaining-example23” />`

以下是对上述代码生成的输出的解释：

1.  从承诺链的顶部开始，`fakeRequest`函数返回的承诺将被履行，从而调用其使用第一个`then`方法的首次调用注册的履行处理程序。因此，以下内容将在控制台上记录：

    ```js
    1 {
    2    favouriteLanguage: "JavaScript",
    3    name: "John Doe"
    4 }

    ```

1.  由`fakeRequest`函数返回的承诺已经完成。链中的下一个承诺是由第一个`then`方法调用返回的承诺。由于原始承诺已完成，第一个`then`承诺现在依赖于其回调函数内部发生的事情。由于它通过调用`fakeRequest`函数返回一个新承诺，第一个`then`承诺将被`resolved`为其回调函数返回的承诺。`then`承诺将在其回调函数返回的承诺完成之前等待其自身完成。

    返回自第一个`then`方法的回调函数的承诺将在大约两秒后完成。它完成后，`then`方法返回的承诺将以与其回调返回的承诺相同的完成值完成。因此，它的完成处理程序被调用，这是通过第二个`then`方法调用注册的。第一个`then`承诺的完成处理程序将其完成值作为参数接收，并在完成处理程序内部记录。到目前为止，控制台输出如下所示：

    ```js
    1 {
    2    favouriteLanguage: "JavaScript",
    3    name: "John Doe"
    4 }
    5 
    6 {
    7    favouriteLanguage: "JavaScript",
    8    name: "John Doe"
    9 }

    ```

1.  此时，承诺链中的两个承诺已完成。链中的下一个承诺是由第二个`then`方法返回的。与第一个`then`方法一样，第二个`then`方法返回的承诺依赖于其调用的原始承诺，即由第一个`then`方法返回的承诺。由于原始承诺已完成，第二个`then`承诺现在依赖于其回调函数内部发生的事情。它的回调隐式返回`undefined`。因此，第二个`then`承诺以`undefined`作为其完成值完成。

    但是没有为第二个`then`承诺注册完成处理程序；只有通过`catch`方法注册了拒绝处理程序。因此，没有完成处理程序在响应第二个`then`方法的完成时被调用。承诺链移动到链中的最后一个承诺，即由`catch`方法返回的承诺。

1.  `catch`方法返回的承诺是在由第二个`then`方法返回的承诺上调用的。由于第二个`then`承诺已完成，`catch`承诺也将以与第二个`then`承诺相同的完成值完成。但是没有为`catch`承诺注册完成或拒绝处理程序，因此其完成被简单忽略。代码的最终输出如下所示：

    ```js
    1 {
    2     favouriteLanguage: "JavaScript",
    3     name: "John Doe"
    4 }
    5 
    6 {
    7     favouriteLanguage: "JavaScript",
    8     name: "John Doe"
    9 }

    ```

#### 示例3

```js
1 fakeRequest(false)
2   .then((response) => {
3     console.log(response);
4   })
5   .catch((error) => {
6     console.log(error.message);
7   });

```

您可以在下面的Replit中运行上述代码：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/promise-chaining-example24” />`

下面是对上述代码生成的输出的解释：

1.  从承诺链的顶部开始，`fakeRequest`函数返回的承诺将被拒绝，但对此承诺没有注册拒绝处理程序；只注册了履行处理程序。因此，对于这个承诺不会调用拒绝处理程序。我们继续处理链中的下一个承诺。

1.  `fakeRequest`函数返回的承诺已经解决。链中的下一个承诺是由第一个`then`方法调用返回的承诺。由于原始承诺被拒绝，并且没有拒绝处理程序传递给`then`方法，`then`方法返回的承诺也将以与原始承诺相同的拒绝值被拒绝。因此，它的拒绝处理程序通过`catch`方法注册并被调用，在控制台上记录以下内容：

    ```js
    1 "request failed"

    ```

    第一个承诺被拒绝时的错误对象是与`then`方法返回的承诺被拒绝时的值相同。承诺链移动到链中的最后一个承诺，即由`catch`方法返回的承诺。

1.  此时，承诺链中的两个承诺已解决。链中的下一个承诺是由`catch`方法返回的承诺。由于`then`承诺被拒绝，`catch`方法返回的承诺依赖于其回调内部发生的事情。它的回调隐式返回`undefined`，导致`catch`承诺以`undefined`作为履行值完成。但是，`catch`承诺没有注册履行处理程序，因此其履行被简单忽略。代码的最终输出如下所示：

    ```js
    1 "request failed"

    ```

在上述代码示例中需要注意的一点是，`fakeRequest`函数返回的承诺的拒绝最终是由为`then`方法返回的承诺注册的拒绝处理程序处理的。这就是承诺链的一种优势。与回调不同，我们需要在每个回调中检查错误，使用承诺链，我们可以注册一个拒绝处理程序，它可以处理所有在它之前的承诺链中的拒绝。我们可以在承诺链中有多个`then`方法调用，而在承诺链的末尾仅有一个拒绝处理程序，通过`catch`方法注册。这使得在承诺链中管理错误处理变得简单。

#### 示例 4

```js
 1 fakeRequest()
 2  .then((response) => {
 3    return fakeRequest(false);
 4  })
 5  .catch((error) => {
 6    return { data: "default data" };
 7  })
 8  .then((data) => {
 9    console.log(data);
10   })
11   .then(() => {
12     throw new Error("error occurred");
13   })
14   .catch((error) => {
15     console.log(error.message);
16   });

```

你可以在下面的`Replit`中运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/promise-chaining-example25" />`

以下是上述代码产生的输出的解释：

1.  从承诺链的顶部开始，`fakeRequest`函数返回的承诺将被实现，导致调用通过第一次调用`then`方法注册的实现处理程序，将实现值作为参数传递给其实现处理程序。

1.  由`fakeRequest`函数返回的承诺已经解决。链中的下一个承诺是由第一个`then`方法调用返回的。由于原始承诺已被实现，第一个`then`承诺现在依赖于其回调函数内部发生的情况。由于它通过调用`fakeRequest`函数返回一个新承诺，第一个`then`承诺将被*解析*为其回调函数返回的承诺。`then`承诺将等待其回调函数返回的承诺解决后再解决自身。

    从第一个`then`方法的回调函数返回的承诺将在大约两秒后被拒绝。它一旦被拒绝，`then`方法返回的承诺也会以与其回调返回的承诺相同的拒绝值被拒绝。因此，其拒绝处理程序将被调用，该处理程序是通过第一次`catch`方法调用注册的。第一个`then`承诺的拒绝处理程序将其拒绝值作为参数接收。

1.  此时，承诺链中的前两个承诺已经解决。链中的下一个承诺是由第一个`catch`方法返回的。由于调用`catch`方法的承诺被拒绝，第一个`catch`承诺现在依赖于其回调函数内部发生的情况。它返回一个对象字面量。因此，第一个`catch`承诺以返回的对象作为其实现值。

    请注意，`catch`方法不一定必须位于承诺链的末尾；然而，`catch`方法通常放在承诺链的末尾。根据需求，`catch`方法可以放在链中的任何位置。在我们的代码示例中，它在第一个`then`方法之后被调用，以处理第一个`then`承诺的可能拒绝，通过返回默认数据并让链继续。如果第一个`then`承诺的拒绝没有被处理，所有在第一个`then`方法之后的`then`承诺也将以与第一个`then`承诺相同的拒绝值被拒绝，而拒绝最终将在最后一次`catch`方法调用中处理。

1.  此时，承诺链中的前三个承诺已经解决。链中的下一个承诺是由第二个`then`方法调用返回的。由于在其上调用第二个`then`方法的承诺（第一个`catch`承诺）已被实现，第二个`then`方法返回的承诺现在依赖于其回调函数内部发生的情况。其回调记录了第一个`catch`承诺的实现值并隐式返回`undefined`，导致第二个`then`承诺以`undefined`作为实现值被实现。以下是此时的控制台输出：

    ```js
    1 {
    2   data: "default data"
    3 }

    ```

1.  此时，承诺链中的前四个承诺已经解决。链中的下一个承诺是由第三个`then`方法调用返回的。由于在其上调用第三个`then`方法的承诺（第二个`then`承诺）已被实现，第三个`then`方法返回的承诺现在依赖于其回调函数内部发生的情况。它的回调抛出了一个错误，导致第三个`then`承诺以抛出的错误作为拒绝原因或值被拒绝。因此，最后一次`catch`方法注册的拒绝处理程序被调用，拒绝值作为参数传递。

1.  由于最后一个`catch`方法调用的promise（第三个`then` promise）被拒绝，最后一个`catch` promise依赖于其回调函数内部发生的事情。其回调记录了第三个`then` promise的拒绝值，并隐式返回`undefined`，导致最后一个`catch` promise以`undefined`作为完成值得到满足。但最后一个`catch` promise没有注册完成处理程序，因此其满足被简单忽略。代码的最终控制台输出如下所示：

    ```js
    1 {
    2   data: "default data"
    3 }
    4 
    5 "error occurred"

    ```

希望上面的示例，以及本节中对可以拒绝或满足每个promise实例方法返回的promise的不同场景的讨论，为理解promise链并在自己的代码中使用它们奠定了坚实的基础。

### `then`中的拒绝处理程序与`catch`

在上一节中提到，可以通过将第二个参数传递给`then`方法来注册拒绝处理程序，如下所示：

```js
1 fakeRequest().then(null, (error) => {
2   // handle error
3 });

```

在使用`then`方法注册拒绝处理程序时，有一点需要注意：如果`then`方法返回的promise被拒绝，那么传递给`then`方法的拒绝处理程序将不会被调用。以下代码示例展示了这一点：

```js
 1 fakeRequest().then(
 2  (response) => {
 3    // rejects the promise returned
 4    // by the "then" method
 5    throw new Error("error");
 6  },
 7  (error) => {
 8    // this callback is not invoked
 9    console.log(error.message);
10   }
11 );

```

只有当调用`then`方法的原始promise被拒绝时，使用`then`方法注册的拒绝处理程序才会被调用。因此，在上面的代码示例中，我们遇到了`unhandled promise rejection`，这在最坏的情况下可能导致程序终止。因此，在处理promise时，请始终记得处理代码中所有可能的promise拒绝。

在本节中，我们将讨论两个promise的[静态方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise#static_properties)的常见用例，并学习它们的实用性。其他promise静态方法也很有用，但在我看来，以下两个用例是最常见的：

+   发起并发请求

+   实现请求超时

### 并发请求

想象一个场景，我们希望同时发起多个HTTP请求，并等待它们的集体结果。我们不能使用如下的promise链，因为这样会按顺序执行每个请求。

```js
 1 const url1 = "https://jsonplaceholder.typicode.com/todos/1";
 2 const url2 = "https://jsonplaceholder.typicode.com/todos/2";
 3 const url3 = "https://jsonplaceholder.typicode.com/todos/3";
 4 
 5 function parseFetchResponse(response) {
 6  if (response.ok) {
 7    return response.json(); // returns a promise
 8  } else {
 9    throw new Error("request failed");
10   }
11 }
12 
13 fetch(url1)
14   .then(parseFetchResponse)
15   .then((data1) => {
16     console.log(data1);
17     // initiate second request
18     return fetch(url2);
19   })
20   .then(parseFetchResponse)
21   .then((data2) => {
22     console.log(data2);
23     // initiate third request
24     return fetch(url3);
25   })
26   .then(parseFetchResponse)
27   .then((data3) => {
28     console.log(data3);
29   })
30   .catch((error) => {
31     console.log(error.message);
32   });

```

你可以在下面的Replit中运行上述代码：

<ReplitEmbed src="https://replit.com/@newlineauthors/static-promise-methods-example1" />

由于上述代码中的每个请求都是独立的，因此我们希望发起[并发](https://en.wikipedia.org/wiki/Concurrent_computing)请求，而不是按顺序发起请求。这可以通过使用`Promise.all`方法实现。它允许我们一个接一个地开始每个请求，而无需等待一个请求完成后再开始另一个请求。因此，所有三个请求都是并发发起的，我们可以等待它们的集体结果。

`Promise.all`方法接收一个[可迭代对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols)作为输入，并返回一个promise，只有在所有传递给它的promise都完成后才会完成。该方法返回的promise的完成值是一个数组，包含了所有传递给该方法作为输入的promise的完成值。如果任何输入的promise被拒绝，该方法返回的promise也会被拒绝。我们可以按照如下方式重写上述代码示例，使用`Promise.all`方法：

```js
 1 const url1 = "https://jsonplaceholder.typicode.com/todos/1";
 2 const url2 = "https://jsonplaceholder.typicode.com/todos/2";
 3 const url3 = "https://jsonplaceholder.typicode.com/todos/3";
 4 
 5 function parseFetchResponse(response) {
 6  if (response.ok) {
 7    return response.json();
 8  } else {
 9    throw new Error("request failed");
10   }
11 }
12 
13 Promise.all([
14   fetch(url1).then(parseFetchResponse),
15   fetch(url2).then(parseFetchResponse),
16   fetch(url3).then(parseFetchResponse)
17 ])
18   .then((dataArr) => {
19     console.log(dataArr);
20   })
21   .catch((error) => console.log(error.message));

```

你可以在下面的Replit中运行上述代码：

<ReplitEmbed src="https://replit.com/@newlineauthors/static-promise-methods-example2" />

### 请求超时

有时，HTTP请求可能由于服务器上的某些问题而挂起。我们不希望请求在待处理状态下停留超过几秒钟。为了避免请求待处理时间过长，我们可以实现请求超时功能，以便让我们的代码知道请求正在花费超过预期的时间。这使我们能够采取适当的措施。

使用`Promise.race`方法，我们可以发起一个带有超时的HTTP请求。该方法与`Promise.all`方法类似，接收一个可迭代的promise集合，并返回一个promise，当输入的一个或多个promise中的任何一个完成时，它就会完成。同样，当任何一个输入promise被拒绝时，该方法返回的promise也会被拒绝。

以下代码示例展示了如何使用`Promise.race`方法实现请求超时：

```js
 1 // simulate a request that takes
 2 // approximately 8 seconds to complete
 3 function delayedRequest() {
 4  return new Promise((resolve, reject) => {
 5    setTimeout(() => {
 6      resolve("hello world");
 7    }, 8000);
 8  });
 9 }
10 
11 // timeout promise that is rejected
12 // after approximately 3 seconds
13 function timeout() {
14   return new Promise((resolve, reject) => {
15     setTimeout(() => {
16       const error = new Error("request timed out");
17       reject(error);
18     }, 3000);
19   });
20 }
21 
22 Promise.race([delayedRequest(), timeout()])
23   .then((response) => {
24     console.log(response);
25   })
26   .catch((error) => console.log(error.message));

```

你可以在下面的Replit中运行上述代码：

<ReplitEmbed src="https://replit.com/@newlineauthors/static-promise-methods-example3" />

在本课中，我们只讨论了两个静态方法，但值得学习`Promise`构造函数上其他可用的[静态方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise#static_methods)。每个静态方法都有其自己的使用场景；我们只讨论了我认为最常用的两个使用场景。

虽然promise改变了我们在JavaScript中编写异步代码的方式，但我们仍然使用回调来注册promise的成功和拒绝处理程序。尽管promise解决了“回调地狱”和传统回调方式中的错误处理问题，但一些人可能会将使用回调与promise结合看作是冗长的。那么有没有更简单、更简洁、更直观的方式来处理promise呢？如果我们在使用promise时能摆脱回调，那该多好！这就是`async await`的优势！

`async await`可以被视为传统使用promise方式的语法糖。它允许我们使用异步执行的代码处理promise，但看起来是同步的。这也使我们能够编写更简洁的代码，更容易理解，因为代码不包含回调，代码流看起来像是同步代码的流。 

让我们看看下面这个使用promise链的代码示例：

```js
 1 function fetchTodo(url) {
 2  fetch(url)
 3    .then((response) => {
 4      if (response.ok) {
 5        return response.json();
 6      } else {
 7        throw new Error("request failed");
 8      }
 9    })
10     .then((data) => {
11       console.log(data);
12     })
13     .catch((error) => {
14       console.log(error.message);
15     });
16 }
17 
18 const url = "https://jsonplaceholder.typicode.com/todos/1";
19 fetchTodo(url);

```

这是一个`Replit`，你可以在这里运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/async-await-example1" />`

上述代码确实比传统的使用回调编写异步代码的方式有所改善，但在可读性方面仍然有提升空间。`async await`语法可以用来重写上述代码示例，如下所示：

```js
 1 async function fetchTodo(url) {
 2  try {
 3    const response = await fetch(url);
 4 
 5    if (response.ok) {
 6      const data = await response.json();
 7      console.log(data);
 8    } else {
 9      throw new Error("request failed");
10     }
11   } catch (error) {
12     console.log(error.message);
13   }
14 }
15 
16 const url = "https://jsonplaceholder.typicode.com/todos/1";
17 fetchTodo(url);

```

这是一个`Replit`，你可以在这里运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/async-await-example2" />`

修改后的代码实现了相同的结果，但更具可读性，不使用任何回调，并且相比于早期使用promise链的示例，更容易理解。尽管代码看起来像是同步代码，但它实际上是异步的。让我们来理解一下`async await`是如何工作的。

在上述使用`async await`语法的代码示例中，有两点需要注意：函数签名中的`async`关键字和函数内部的`await`关键字。使用`async await`语法的主要步骤如下：

1.  使用`async`关键字将任何函数标记为`async`。这是必要的，因为`await`关键字只能在`async`函数内部使用。

1.  在`async`函数内部使用`await`关键字来等待任何promise的解决。

:::info 虽然 `await` 关键字大多在 `async` 函数内部使用，因为在最近语言的变更之前，`await` 关键字仅被允许在 `async` 函数内部使用，现在可以在模块的顶部使用 [await 关键字](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await#top_level_await)。

::::

### `async` 函数

`async` 函数允许在其体内使用 `await` 关键字。`async` 函数与非 `async` 函数不同，因为 `async` 函数始终返回一个承诺。`async` 函数隐式创建并返回一个承诺，类似于每个承诺实例方法创建并返回一个新的承诺。以下代码验证了这一说法：

```js
1 async function foo() {}
2 
3 const result = foo();
4 console.log(result instanceof Promise); // true

```

这里有一个 Replit，你可以运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/async-await-example3" />`

`async` 函数返回的承诺的兑现或拒绝取决于其体内发生的事情，类似于每个承诺实例方法返回的承诺依赖于其回调函数内发生的事件。以下几点总结了 `async` 函数承诺的结算：

+   从 `async` 函数返回任何非承诺值会导致 `async` 函数的承诺被兑现，使用返回的值作为兑现值。

    ```js
    1 async function foo() {
    2   return 123;
    3 }
    4 
    5 foo().then(console.log); // 123

    ```

这里有一个 Replit，你可以运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/async-await-example4" />`

+   不从函数返回任何值会隐式返回 `undefined`。这会导致函数的承诺以 `undefined` 作为兑现值。

    ```js
    1 async function foo() {}
    2 
    3 foo().then(console.log); // undefined

    ```

这里有一个 Replit，你可以运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/async-await-example5" />`

+   在 `async` 函数内部抛出错误会拒绝该 `async` 函数的承诺，并使用抛出的值作为拒绝原因。

    ```js
    1 async function foo() {
    2   throw new Error("some error occurred");
    3 }
    4 
    5 foo().catch((error) => console.log(error.message)); // some error occurred

    ```

这里有一个 Replit，你可以运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/async-await-example6" />`

+   从 `async` 函数返回一个承诺会使该 `async` 函数的承诺被 `resolved` 为函数体内返回的承诺。正如我们在本模块之前的某个课程中学习到的，一个承诺可能会“解析”到另一个承诺，`async` 函数创建的承诺将等待函数体内返回的承诺完成。最终，`async` 函数的承诺将根据其内部返回的承诺的结果被兑现或拒绝。

    ```js
     1 // returns a promise that is fulfilled
     2 // after approximately 2 seconds
     3 function getPromise() {
     4  return new Promise((resolve, reject) => {
     5    setTimeout(() => {
     6      resolve("hello world");
     7    }, 2000);
     8  });
     9 }
    10 
    11 async function foo() {
    12   return getPromise();
    13 }
    14 
    15 foo().then(console.log); // hello world

    ```

这里有一个 Replit，你可以运行上述代码：

`<ReplitEmbed src="https://replit.com/@newlineauthors/async-await-example7" />`

### `await` 关键字

`await` 关键字，也称为 `await` 操作符，用于等待承诺完成。以下是使用 `await` 关键字等待承诺完成的示例：

```js
1 // assume that the following statement
2 // is inside an async function
3 const response = await fetch(url);

```

`await fetch(url)` 是一个表达式，它将评估 `fetch` 函数返回的 promise 的实现值，或者如果 `fetch` 函数返回的 promise 被拒绝，则会抛出拒绝值。抛出的值可以在外围 `try-catch` 块的 `catch` 块中捕获，或者如果 `await` 语句没有被 `try-catch` 包裹，`awaited` promise 的拒绝将使 `async` 函数的 promise 被拒绝，从而允许调用代码处理 promise 的拒绝。

与 promise 链接不同，在 promise 链接中我们必须注册实现处理器以获取 promise 的实现值，而 `await` 表达式评估 promise 的实现值，我们可以将其保存在变量中。但它是如何工作的呢？在等待 promise 解决时，不是阻塞主线程吗？

每当调用 `async` 函数时，它会同步执行，直到遇到第一个 `await` 表达式。函数的执行会暂停，直到等待的 promise 被解决。它并不是阻塞主线程，而是函数的执行暂停，同时主线程可以自由处理其他事务。当 promise 最终被解决时，函数的执行恢复，如果 promise 被实现，代码在 `await` 表达式后继续执行；如果等待的 promise 被拒绝，则抛出 promise 的拒绝值。

重要的是要注意，`async` 函数内部的代码会同步执行，直到第一个 `await` 表达式。如果 `async` 函数内部没有 `await` 关键字，函数会同步执行吗？是的，但请记住，`async` 函数始终返回一个 promise，它将根据 `async` 函数内部的情况被实现或拒绝。这意味着以下代码并不会按预期工作：

```js
1 async function foo() {
2   return "123";
3 }
4 
5 const result = foo();

```

上述代码示例中的 `async` 函数没有使用 `await` 关键字，因此其内部代码是同步执行的，但它是否也同步返回值 `“123”`？不，它不会。该函数是 `async`，这意味着它返回一个 promise，因此上述示例中的 `result` 包含的是 promise 而不是值 `“123”`。要获取 promise 的实现值，我们可以使用如下所示的 promise 链接：

```js
1 async function foo() {
2   return "123";
3 }
4 
5 foo().then(console.log); // "123"

```

这是一个可以运行上述代码的 `Replit`：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/async-await-example10” />`

或者使用如下所示的 `async await` 语法 `await` `foo` 函数返回的 promise：

```js
 1 async function foo() {
 2  return "123";
 3 }
 4 
 5 async function bar() {
 6  const result = await foo();
 7  console.log(result); // "123"
 8 }
 9 
10 bar();

```

这是一个可以运行上述代码的 `Replit`：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/async-await-example11” />`

### 多个 `await` 表达式

`async`函数并不局限于在其主体内只使用一次`await`关键字。您可以在`async`函数内多次使用`await`关键字。需要注意的唯一事项是多个`await`表达式不会并行执行；相反，它们是顺序执行的，一个接一个。函数执行将在每个`await`表达式处暂停，只有在前面的表达式执行完后，才能执行下一个`await`表达式。

```js
 1 // returns a promise that is fulfilled
 2 // after approximately 1 second
 3 function promisifiedRandomNumber() {
 4  return new Promise((resolve, reject) => {
 5    setTimeout(() => {
 6      // generate a random number within range: 0 - 9
 7      const randomNum = Math.floor(Math.random() * 10);
 8      resolve(randomNum);
 9    }, 1000);
10   });
11 }
12 
13 async function random() {
14   const num1 = await promisifiedRandomNumber();
15   const num2 = await promisifiedRandomNumber();
16   const num3 = await promisifiedRandomNumber();
17 
18   console.log(num1, num2, num3);
19 }
20 
21 random();

```

这是一个可以运行上述代码的`Replit`：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/async-await-example12” />`

上述代码示例中的每个`await`表达式大约需要1秒钟，因此函数大约需要3秒钟来评估所有的`await`表达式，并在最后记录它们的值。

```js
 1 // returns a promise that is fulfilled
 2 // after approximately 1 second
 3 function promisifiedRandomNumber() {
 4  return new Promise((resolve, reject) => {
 5    setTimeout(() => {
 6      // generate a random number within range: 0 - 9
 7      const randomNum = Math.floor(Math.random() * 10);
 8      resolve(randomNum);
 9    }, 1000);
10   });
11 }
12 
13 async function random() {
14   const randomSum =
15     (await promisifiedRandomNumber()) + (await promisifiedRandomNumber());
16   console.log(randomSum);
17 }
18 
19 random();

```

这是一个可以运行上述代码的`Replit`：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/async-await-example13” />`

上述代码示例中的两个`await`表达式也不是并行执行的；相反，它们是一个接一个地执行，从左到右。

假设我们想在`async`函数内进行并发异步操作。在这种情况下，我们可以使用`Promise.all`函数，将所有的承诺作为输入，并等待`Promise.all`返回的承诺。

```js
 1 // returns a promise that is fulfilled
 2 // after approximately 1 second
 3 function promisifiedRandomNumber() {
 4  return new Promise((resolve, reject) => {
 5    setTimeout(() => {
 6      // generate a random number within range: 0 - 9
 7      const randomNum = Math.floor(Math.random() * 10);
 8      resolve(randomNum);
 9    }, 1000);
10   });
11 }
12 
13 async function random() {
14   const promiseArr = [
15     promisifiedRandomNumber(),
16     promisifiedRandomNumber(),
17     promisifiedRandomNumber()
18   ];
19   const randomNumsArr = await Promise.all(promiseArr);
20   console.log(randomNumsArr);
21 }
22 
23 random();

```

这是一个可以运行上述代码的`Replit`：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/async-await-example14” />`

### 错误处理

要在`async`函数内处理承诺拒绝，我们可以像下面所示用`try-catch`块包装`await`表达式：

```js
1 async function getUsersAndTasks() {
2   try {
3     const users = await fetchUsers();
4     const tasks = await fetchTasks();
5   } catch (error) {
6     // handle the error
7   }
8 }

```

如果在`try`块中等待的任何承诺被拒绝，之后的`await`表达式后面的代码将不会被执行，执行将跳转到`catch`块。`await`关键字抛出承诺拒绝值，允许`catch`块捕获拒绝。

另外，我们可以省略`try-catch`块，但在这种情况下，调用`async`函数的代码必须处理承诺拒绝，方法是使用承诺链：

```js
 1 async function getUsersAndTasks() {
 2  const users = await fetchUsers();
 3  const tasks = await fetchTasks();
 4 
 5  // do something with users and tasks.
 6 }
 7 
 8 getUsersAndTasks().catch((error) => {
 9  /* handle the error */
10 });

```

或者在调用代码中使用`try-catch`块，如果我们使用`async await`语法：

```js
 1 async function getUsersAndTasks() {
 2  const users = await fetchUsers();
 3  const tasks = await fetchTasks();
 4 
 5  // do something with users and tasks.
 6 }
 7 
 8 async function initApp() {
 9  try {
10     await getUsersAndTasks();
11   } catch (error) {
12     // handle the error
13   }
14 }

```

### 返回与等待承诺

忘记在`async`函数内`await`一个承诺可能会导致错误，产生意外输出。下面的代码展示了它可能引起的问题：

```js
 1 // returns a promise that either
 2 // fulfills or gets rejected randomly
 3 function getPromise() {
 4  return new Promise((resolve, reject) => {
 5    setTimeout(() => {
 6      if (Math.random() < 0.5) {
 7        resolve("success");
 8      } else {
 9        reject(new Error("failed"));
10       }
11     }, 1000);
12   });
13 }
14 
15 async function foo() {
16   getPromise();
17 }
18 
19 foo()
20   .then(() => console.log("foo promise fulfilled"))
21   .catch(() => console.log("foo promise rejected"));

```

这是一个可以运行上述代码的`Replit`：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/async-await-example18” />`

`getPromise` 函数返回一个可能被拒绝的 promise，但 `foo` 函数返回的 promise 始终是被解决的。为什么？`foo` 函数有一个问题：它没有 `return` 或 `await` `getPromise` 函数返回的 promise。因此，`foo` 函数不会等待 `getPromise` 函数返回的 promise 完成；而只是调用 `getPromise` 函数，函数执行结束，隐式返回 `undefined`，导致 `foo` 函数的 promise 以 `undefined` 作为解决值。

进一步的代码示例将使用上面定义的 `getPromise` 函数。

要捕获 `getPromise` 函数返回的 promise 的拒绝，我们有以下选项：

+   `return` `getPromise` 函数返回的 promise。

    ```js
    1 async function foo() {
    2   return getPromise();
    3 }
    4 
    5 foo()
    6   .then(() => console.log("foo promise fulfilled"))
    7   .catch(() => console.log("foo promise failed"));

    ```

这是一个可以运行上述代码的 Replit：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/async-await-example19” />`

返回的 promise `resolves` 了其内部返回的 promise 的 `foo` 函数。因此，无论`getPromise` 返回的 promise 发生了什么，`foo` 函数的 promise 都会有相同的结果。

+   `await` `getPromise` 函数返回的 promise。

    ```js
    1 async function foo() {
    2   await getPromise();
    3 }
    4 
    5 foo()
    6   .then(() => console.log("foo promise fulfilled"))
    7   .catch(() => console.log("foo promise failed"));

    ```

这是一个可以运行上述代码的 Replit：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/async-await-example20” />`

如前所述，如果被等待的 promise 被拒绝，其拒绝值会在 `async` 函数内部抛出。由于 `foo` 函数内部没有 `try-catch` 块，promise 的拒绝导致 `foo` 函数的 promise 也会以相同的拒绝原因被拒绝。

然而，这段代码示例中需要注意的一点是，如果 `getPromise` 返回的 promise 被解决，`foo` 函数的 promise 不会以其解决值被解决；相反，它以 `undefined` 作为解决值被解决，因为我们没有明确从 `foo` 函数返回任何内容，我们知道当我们在 `async` 函数内部没有明确返回任何值时，`async` 函数的 promise 会以 `undefined` 作为解决值被解决。

+   `await` `getPromise` 函数返回的 promise，并用 `try-catch` 块包围它。

    ```js
     1 async function foo() {
     2  try {
     3    await getPromise();
     4  } catch (error) {
     5    console.log("inside catch block of foo function");
     6    return "error caught in foo";
     7  }
     8 }
     9 
    10 foo()
    11   .then(() => console.log("foo promise fulfilled"))
    12   .catch(() => console.log("foo promise failed"));

    ```

这是一个可以运行上述代码的 Replit：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/async-await-example21” />`

等待 `getPromise` 调用将捕获 promise 的拒绝，导致 `catch` 块执行。然而，`foo` 函数返回的 promise 将始终被解决。为什么？因为 `catch` 块没有抛出错误或返回被拒绝的 promise。结果，`foo` 函数的 promise 总是以 `catch` 块的返回值解决。我们可以从 `catch` 中抛出错误来解决这个问题。话虽如此，如果我们在 `catch` 块中所做的只是抛出错误，那么最好省略 `try-catch` 块，让 promise 拒绝自动拒绝 `foo` 函数的 promise。

此代码示例中的另一个问题是，如果 promise 被解决而 `catch` 块从未执行，我们没有显式返回任何值。因此，`foo` 函数的 promise 将以 `undefined` 解决。在 `await` 表达式前添加 `return` 关键字可以解决这个问题。

:::caution 我们能不能只做`return getPromise();`而不是`return await getPromise();`？如果`await`表达式没有被包装在`try-catch`块中，我们是可以的。`try-catch`块有什么区别呢？有了`try-catch`块，`return getPromise();`将导致`foo`函数内的`catch`块永远不会执行。为了使`foo`函数中的`catch`块执行，我们需要在`try`块中`await`这个promise，而不仅仅是返回它。更多细节，请阅读：[await vs return vs return await](https://jakearchibald.com/2017/await-vs-return-vs-return-await/) :::

### 等待非promise值

`await`关键字通常用于等待一个promise解决，但它也可以与非promise值一起使用。以下代码示例展示了这一行为：

```js
1 const printRandomNumber = async () => {
2   const randomNum = await Math.floor(Math.random() * 10);
3   console.log(randomNum);
4 };
5 
6 printRandomNumber();
7 
8 console.log("before printing random number");

```

这是一个Replit，你可以运行上述代码：

<ReplitEmbed src="https://replit.com/@newlineauthors/async-await-example22" />

如果你执行上述代码示例，你会注意到代码示例最后的`console.log`语句在随机数打印之前被记录，尽管函数在最后的`console.log`语句之前被调用。这是为什么呢？因为我们没有等待任何promise，所以这里发生了什么？

当`await`关键字与非承诺值一起使用时，会创建一个新的承诺，该承诺会用我们在`await`关键字中使用的值来满足。在我们的代码示例中，我们等待了一个随机数；它不是一个承诺，因此会创建一个新的承诺，并用生成的随机数来满足。在`await`表达式之后的代码将被执行，就好像它在一个满足处理程序中一样。因此，当承诺被满足时，`await`表达式之后的代码并不会立即执行。它是异步执行的，正如我们在关于事件循环的课程中学到的，任何异步代码只有在我们代码的同步执行结束后才会被执行。最后的`console.log`语句作为我们代码的同步执行的一部分被执行。因此，它在随机数之前被记录。

使用`await`与非承诺值几乎没有用，但要注意的是，这种情况是可能的，该值会被隐式封装在一个承诺中。

我们在本模块的早期课程中了解到，执行DOM事件监听器和`setTimeout`或`setInterval`回调需要调度一个“任务”。任务在任务队列中排队，直到事件循环处理它们。那么承诺的履行或拒绝处理程序呢？它们的执行是否也需要调度一个任务？并不是严格意义上的任务，而是一个“微任务”。

微任务，ECMAScript规范称之为[jobs](https://tc39.es/ecma262/#sec-promise-jobs)，被调度用于比“任务”更高优先级的事情。微任务在以下情况下被处理：

+   每个回调，只要调用栈是空的。

+   每个任务

“任务”按照它们在任务队列中排队的顺序执行，每个事件循环的一个轮次中只执行一个任务。

另一个关于微任务的重要注意事项是，虽然每个事件循环的滴答中仅处理一个任务，但微任务会一直处理，直到微任务队列为空。如果一个任务调度了另一个任务，它不会在下一个事件循环的轮次中被处理，但在微任务的情况下，如果一个微任务由另一个微任务排队，排队的微任务也将被处理。这意味着如果每个微任务不断排队另一个微任务，事件循环可能会陷入无限循环。

考虑以下代码示例：

```js
 1 console.log("start");
 2 
 3 setTimeout(() => {
 4  console.log("setTimeout callback with 500ms delay");
 5 }, 500);
 6 
 7 Promise.resolve()
 8  .then(() => {
 9    console.log("first 'then' callback");
10   })
11   .then(() => {
12     console.log("second 'then' callback");
13   })
14   .then(() => {
15     console.log("third 'then' callback");
16   });
17 
18 setTimeout(() => {
19   console.log("setTimeout callback with 0ms delay");
20 }, 0);
21 
22 console.log("end");
23 
24 /*
25 start
26 end
27 first 'then' callback
28 second 'then' callback
29 third 'then' callback
30 setTimeout callback with 0ms delay
31 setTimeout callback with 500ms delay
32 */

```

这是上面代码在行动中的一个Replit：

`<ReplitEmbed src="https://replit.com/@newlineauthors/microtasks-example1" />`

执行上述代码需要调度任务和微任务。以下步骤解释了如何调度不同的任务和微任务以执行上述代码：

1.  创建一个任务来执行脚本，开始代码的同步执行。

1.  第一个`console.log`语句被执行，在控制台上记录“start”。

    ```js
    1 output:
    2 -------
    3 start

    ```

1.  接下来，我们有一个`setTimeout`调用，延迟500毫秒。这在后台启动一个定时器，其到期将导致一个任务被排队到任务队列中以执行`setTimeout`回调。

    ```js
    1 task queue:
    2 -----------
    3 [task(execute setTimeout callback)]
    4 
    5 output:
    6 -------
    7 start

    ```

1.  继续进行代码的同步执行，调用`Promise.resolve`，它创建了一个已解决的承诺。为了执行其履行处理程序，一个微任务或工作被排队到微任务队列中。

    ```js
     1 task queue:
     2 -----------
     3 [task(execute setTimeout callback)]
     4 
     5 microtask queue:
     6 ----------------
     7 [job(execute fulfillment callback)]
     8 
     9 output:
    10 -------
    11 start

    ```

1.  接下来，我们有一个`setTimeout`调用，延迟为0毫秒。这也安排了一个任务来执行其回调。

    ```js
     1 task queue:
     2 -----------
     3 [
     4    task(execute setTimeout callback),
     5    task(execute setTimeout callback)
     6 ]
     7 
     8 microtask queue:
     9 ----------------
    10 [job(execute fulfillment callback)]
    11 
    12 output:
    13 -------
    14 start

    ```

1.  最后，同步执行以最终的`console.log`语句结束，在控制台上记录“end”。此时，调用栈为空，事件循环可以开始处理已安排的任务和微任务。

    ```js
     1 task queue:
     2 -----------
     3 [
     4    task(execute setTimeout callback),
     5    task(execute setTimeout callback)
     6 ]
     7 
     8 microtask queue:
     9 ----------------
    10 [job(execute fulfillment callback)]
    11 
    12 output:
    13 -------
    14 start
    15 end

    ```

1.  如前所述，微任务在每个任务以及每个回调之后处理，前提是调用栈为空。代码的同步执行是一个任务，当它结束时，调用栈为空，因此微任务队列中的任何微任务都准备好由事件循环处理。我们在微任务队列中只有一个微任务。它将通过在控制台上记录“first ‘then’ callback”来处理。

    ```js
     1 task queue:
     2 -----------
     3 [
     4    task(execute setTimeout callback),
     5    task(execute setTimeout callback)
     6 ]
     7 
     8 microtask queue:
     9 ----------------
    10 []
    11 
    12 output:
    13 -------
    14 start
    15 end
    16 first 'then' callback

    ```

1.  第一个`then`方法的回调函数隐式返回`undefined`，因此`then`方法返回的承诺以`undefined`作为履行值被履行。这在微任务队列中排队了另一个微任务，以执行第一个`then`方法返回的承诺的履行处理程序。

    ```js
     1 task queue:
     2 -----------
     3 [
     4    task(execute setTimeout callback),
     5    task(execute setTimeout callback)
     6 ]
     7 
     8 microtask queue:
     9 ----------------
    10 [job(execute fulfillment callback)]
    11 
    12 output:
    13 -------
    14 start
    15 end
    16 first 'then' callback

    ```

1.  如前所述，微任务会被处理直到微任务队列为空，因此新排队的微任务也会被处理，在控制台上记录“second ‘then’ callback”。

    ```js
     1 task queue:
     2 -----------
     3 [
     4    task(execute setTimeout callback),
     5    task(execute setTimeout callback)
     6 ]
     7 
     8 microtask queue:
     9 ----------------
    10 []
    11 
    12 output:
    13 -------
    14 start
    15 end
    16 first 'then' callback
    17 second 'then' callback

    ```

1.  类似于第8步，第二个`then`方法的回调函数隐式返回`undefined`，因此`then`方法返回的承诺以`undefined`作为履行值被履行。这在微任务队列中排队了另一个微任务，以执行第二个`then`方法返回的承诺的履行处理程序。

    ```js
     1 task queue:
     2 -----------
     3 [
     4    task(execute setTimeout callback),
     5    task(execute setTimeout callback)
     6 ]
     7 
     8 microtask queue:
     9 ----------------
    10 [job(execute fulfillment callback)]
    11 
    12 output:
    13 -------
    14 start
    15 end
    16 first 'then' callback
    17 second 'then' callback

    ```

1.  这导致“third ‘then’ callback”在控制台上被记录。

    ```js
     1 task queue:
     2 -----------
     3 [
     4    task(execute setTimeout callback),
     5    task(execute setTimeout callback)
     6 ]
     7 
     8 microtask queue:
     9 ----------------
    10 []
    11 
    12 output:
    13 -------
    14 start
    15 end
    16 first 'then' callback
    17 second 'then' callback
    18 third 'then' callback

    ```

1.  我们没有对第三个`then`方法返回的承诺做任何操作，因此其履行被忽略。此时，所有微任务都已被处理，微任务队列为空。事件循环现在可以处理任务队列中的第一个任务。

1.  任务队列中的第一个任务是第二个`setTimeout`调用，因为它的延迟小于第一个，因此它在另一个`setTimeout`回调的任务之前排队，后者的延迟为500毫秒。处理它导致在控制台上记录“setTimeout callback with 0ms delay”。

    ```js
     1 task queue:
     2 -----------
     3 [task(execute setTimeout callback)]
     4 
     5 microtask queue:
     6 ----------------
     7 []
     8 
     9 output:
    10 -------
    11 start
    12 end
    13 first 'then' callback
    14 second 'then' callback
    15 third 'then' callback
    16 setTimeout callback with 0ms delay

    ```

1.  最后，任务队列中的最后一个任务是第一个`setTimeout`调用，其延迟为500毫秒，导致“setTimeout callback with 500ms delay”在控制台上被记录。

    ```js
     1 task queue:
     2 -----------
     3 []
     4 
     5 microtask queue:
     6 ----------------
     7 []
     8 
     9 output:
    10 -------
    11 start
    12 end
    13 first 'then' callback
    14 second 'then' callback
    15 third 'then' callback
    16 setTimeout callback with 0ms delay
    17 setTimeout callback with 500ms delay

    ```

:::note 在本模块中，我们使用“resolved”一词来指代一个正在等待另一个承诺解决的承诺。换句话说，我们使用“resolved”一词来指代一个待处理状态的承诺。

话虽如此，“已解决”一词也可以用来指代已被履行或拒绝的承诺。有关更多细节，请阅读：[promises-unwrapping - 状态与命运](https://github.com/domenic/promises-unwrapping/blob/master/docs/states-and-fates.md)

::: 

#### 深入阅读

以下是一些与微任务相关的 Stackoverflow 问题的链接，这些问题是我回答的，解释了类似于上面讨论的代码示例的执行：

+   [如何解释这段代码片段的输出顺序？](https://stackoverflow.com/questions/63052649/how-to-explain-the-output-order-of-this-code-snippet)

+   [结合 `promise.then` 和 `async` 函数的 JavaScript 打印顺序测验](https://stackoverflow.com/questions/72306157/javascript-quiz-of-printing-sequence-with-combination-of-promise-then-and-async)

+   [承诺链 `.then` `.catch`](https://stackoverflow.com/questions/68784426/promise-chain-then-catch)

+   [JavaScript 中的异步执行顺序](https://stackoverflow.com/questions/68882535/asynchronous-execution-order-in-javascript)

以下是一篇通过交互式示例解释任务和微任务执行的文章：

+   [任务、微任务、队列和调度](https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/)

在本课中，我们将讨论应该避免的常见承诺相关反模式。以下是我们将讨论的反模式列表：

+   不必要使用 `Promise` 构造函数

+   错误处理不当

+   将承诺拒绝转换为履行

+   异步执行器函数

### 不必要使用 `Promise` 构造函数

JavaScript 开发者，尤其是那些对承诺没有太多经验的人，常犯的一个错误是使用 `Promise` 构造函数不必要地创建承诺。让我们来看一个例子：

```js
1 function fetchData(url) {
2   return new Promise((resolve, reject) => {
3     fetch(url)
4       .then((res) => res.json(res))
5       .then(resolve)
6       .catch(reject);
7   });
8 }

```

如果你向 `fetchData` 函数传递一个 URL 然后等待承诺解决，上述代码将正常工作，但在上述代码示例中使用 `Promise` 构造函数是多余的。`fetch` 函数已经返回一个承诺，因此我们可以将上述函数重新写为如下所示，而无需用 `Promise` 构造函数包装 `fetch` 函数调用：

```js
1 function fetchData(url) {
2   return fetch(url).then((res) => res.json(res));
3 }

```

修订后的 `fetchData` 函数简洁易读，没有创建任何不必要的承诺，并允许调用 `fetchData` 函数的代码捕获和处理任何错误。旧版本的 `fetchData` 函数也允许调用代码处理错误，但修订版本在不使用 `catch` 方法调用的情况下完成了这一点。

不必要地使用承诺构造函数可能导致另一个问题：如果我们忘记在``Promise``构造函数内部的承诺链中添加``catch``方法调用，那么在HTTP请求期间抛出的任何错误都将无法捕获。忘记在执行器函数内部调用``reject``函数会隐藏异步操作失败的情况。

### 错误的错误处理。

在编写使用承诺的代码时，最重要的规则之一是要么捕获并处理错误，要么返回承诺以允许调用代码捕获和处理它。这个基本规则可以帮助你避免使用承诺的代码中的隐藏错误。

让我们看一个错误处理不当的例子，这个例子违反了上述规则：

```js
1 function fetchData(url) {
2   fetch(url).then((response) => response.json());
3 }
4 
5 fetchData("https://jsonplaceholder.typicode.com/todos/1")
6   .then((data) => console.log(data))
7   .catch((error) => console.log(error));

```

这里是上面代码运行的Replit：

<ReplitEmbed src="https://replit.com/@newlineauthors/promise-anti-patterns-example3" />

上述代码抛出一个错误，因为``fetchData``函数没有返回承诺。这也不允许调用代码进行任何形式的错误处理。

修复上面代码有两种方法：

+   通过在``fetchData``函数前添加``return``关键字来返回承诺。

    ```js
    1 function fetchData(url) {
    2   return fetch(url).then((response) => response.json());
    3 }

    ```

    这里是上面代码运行的Replit：

    <ReplitEmbed src="https://replit.com/@newlineauthors/promise-anti-patterns-example4" />

    由于上述函数只是发出HTTP请求，并在响应对象上调用``json()``方法后返回响应数据，因此调用代码负责使用响应数据以及处理任何错误。

    ```js
    1 fetchData(/* some url */)
    2   .then((data) => {
    3     /* do something with the data */
    4   })
    5   .catch((error) => {
    6     /* handle error */
    7   });

    ```

+   通过将``catch``方法链接到``then``方法，在``fetchData``函数内部处理错误。

    ```js
     1 function fetchData(url) {
     2  fetch(url)
     3    .then((response) => response.json())
     4    .then((data) => {
     5      /* do something with the data */
     6    })
     7    .catch((err) => {
     8      /* error handling code */
     9    });
    10 }

    ```

    并且你以如下所示调用上面的函数：

    ```js
    1 fetchData(/* some url */);

    ```

### 将承诺拒绝转换为履行。

``Promise.prototype``对象上的每个方法都返回一个新的承诺。如果我们不小心，可能会编写代码，将承诺拒绝隐式转换为承诺履行。让我们看一个例子：

```js
1 function getData(url) {
2   return Promise.reject(new Error()).catch((err) => {
3     console.log("inside catch block in getData function");
4   });
5 }
6 
7 getData()
8   .then((data) => console.log("then block"))
9   .catch((error) => console.log("catch block"));

```

这里是上面代码运行的Replit：

<ReplitEmbed src="https://replit.com/@newlineauthors/promise-anti-patterns-example8" />

你期望什么输出？输出如下所示：

```js
1 "inside catch block in getData function"
2 
3 "then block"

```

我们在``getData``函数内部调用了[``Promise.reject``](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/reject)，那么为什么没有记录“then block”，而是“catch block”没有被记录？为什么是``then``方法的回调函数被调用，而不是catch块？让我们理解上面代码的执行过程：

1.  ``getData``函数被调用。

1.  ``Promise.reject(new Error())``创建一个被拒绝的承诺。

1.  由于承诺被拒绝，``catch``方法的回调函数被调用。

1.  “inside catch block in getData function”被记录在控制台上。

1.  由于``catch``方法的回调函数没有显式返回任何内容，因此回调函数隐式返回``undefined``。

1.  `catch`方法返回的承诺以其回调函数的返回值被履行，即`undefined`。

1.  这个被履行的承诺通过`getData`函数返回给其调用代码。

1.  由于`getData`函数返回的承诺以值`undefined`被履行，`then`方法的回调在调用代码中被调用，记录“then块”。

请查看这个[stackoverflow帖子](https://stackoverflow.com/questions/62859190/handle-promise-catches-in-typescript)，它更详细地解释了这种行为。

虽然上面的代码是一个人为的示例，但想象一下，如果`getData`函数中调用的是`fetch`函数而不是`Promise.reject`；如果HTTP请求成功，我们的代码将毫无问题地运行，但如果HTTP请求失败，`getData`函数中的`catch`方法将把承诺拒绝转换为承诺履行。因此，`getData`函数将返回一个被履行的承诺，而不是返回一个被拒绝的承诺。

:::info

有时，您确实希望将承诺拒绝转换为承诺履行，以处理拒绝并让承诺链继续。这是可以的，但要有意识地进行。请注意，如果您不小心，承诺拒绝可能会变成承诺履行。这样做肯定会导致代码中的错误。

:::

假设您在想为什么`catch`方法返回的承诺被履行而不是被拒绝。在这种情况下，答案是，如前面所述，`then`或`catch`方法返回的承诺如果它们的回调函数显式或隐式返回一个值而不是抛出错误或返回一个被拒绝的承诺或最终被拒绝的承诺，就会被履行。

那么，我们如何修复上述代码示例以避免这个问题呢？有两种方法可以解决这个问题：

+   从`catch`方法的回调函数中抛出错误。

    ```js
    1 function getData(url) {
    2   return Promise.reject(new Error()).catch((err) => {
    3     throw err;
    4   });
    5 }

    ```

    这是上面代码在操作中的一个Replit示例：

    <ReplitEmbed src="https://replit.com/@newlineauthors/promise-anti-patterns-example9" />

这将拒绝`catch`方法返回的承诺，并且`getData`函数将返回这个被拒绝的承诺。结果，正如预期的那样，调用代码中的`catch`方法回调将被调用。

+   删除`catch`方法调用。

    ```js
    1 function getData(url) {
    2   return Promise.reject(new Error());
    3 }

    ```

    这是上面代码在操作中的一个Replit示例：

    <ReplitEmbed src="https://replit.com/@newlineauthors/promise-anti-patterns-example10" />

    这也将调用调用代码中的`catch`块，因为现在`getData`函数返回的是调用`Promise.reject`的结果，并且如前所述，`Promise.reject`创建了一个被拒绝的承诺。:::tip 个人而言，我建议使用这种方法而不是从`catch`方法回调中抛出错误。让调用代码捕获并处理错误就可以了。`catch`方法回调仅重新抛出错误是多余的。:::

### 异步执行器函数

在使用`Promise`构造函数创建新承诺时，我们将一个函数传递给承诺构造函数。这个函数被称为`executor`函数。`executor`函数绝不应该是一个`async`函数。为什么呢？

假设`executor`函数是一个`async`函数。在这种情况下，`async` `executor`函数抛出的任何错误都不会被捕获，抛出的错误不会导致新构造的承诺被拒绝。

```js
1 const p = new Promise(async (resolve, reject) => {
2   throw new Error("error");
3 });
4 
5 p.catch((e) => console.log(e.message));

```

在上面的代码示例中，由于`executor`函数是一个`async`函数，因此其中抛出的错误不会拒绝新创建的承诺`p`。结果，针对承诺`p`调用的`catch`方法的回调函数从未被调用。

如果`executor`函数是一个同步函数，则在`executor`函数内部抛出的任何错误将自动拒绝新创建的承诺。尝试删除上面代码示例中的`async`关键字，并观察输出。

另一个需要注意的事项是，如果您发现自己在`executor`函数中使用`await`，这应该提醒您根本不需要`promise`构造函数（记住上面讨论的第一个反模式）。
