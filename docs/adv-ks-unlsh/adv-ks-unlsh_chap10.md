## 调试 JavaScript

调试是查找和修复代码中问题或错误的过程。大多数软件开发者（如果不是全部的话）花在调试代码上的时间比写代码的时间还要多。因此，调试是任何软件开发者必备的技能。编写无错误代码是不可能的，因此有效地学习调试自己的或他人的代码可以大大提高您的工作效率。作为软件开发者，我们无法逃避调试，因此不如学会有效地进行调试。

在本模块中，我们将学习不同的调试 JavaScript 代码的方法。每个 JavaScript 开发者都会使用 `console.log` 和 `alert` 函数来调试他们的代码，这样做是可以的，但还有其他调试 JavaScript 的方法。本模块的目标是介绍以下三种可以帮助我们有效调试 JavaScript 代码的方法：

+   使用 `debugger` 语句

+   使用浏览器开发工具中的断点

+   使用 `VS Code` 调试器

:::note

上述提到的调试策略依赖于 [调试器](https://en.wikipedia.org/wiki/Debugger) 来帮助我们有效地调试代码。

:::

接下来的几节课将介绍上述每种方法。

`debugger` 语句允许我们在代码中设置一个点，调试器可以在此暂停代码的执行。这就像在代码中设置断点一样，可以暂停代码的执行，从而检查代码中不同变量的值。

在浏览器中运行以下代码示例并输入值 `“18”`。下面的代码可以正常工作，但对于值 `“18”` 给出了错误的输出。

```js
 1 function isOldEnoughToDrive() {
 2  const age = prompt("What is your age?");
 3  let result;
 4 
 5  debugger;
 6 
 7  if (age === 18) {
 8    result = "You are just about the right age to drive!";
 9  } else if (age < 18) {
10     result = "Not allowed to drive";
11   } else if (age > 18) {
12     result = "Allowed to drive!";
13   } else {
14     result = "invalid age value provided";
15   }
16 
17   const resultElm = document.querySelector("#result");
18   resultElm.innerHTML = result;
19 }
20 
21 isOldEnoughToDrive();

```

```js
1 <body>
2   <h2 id="result"></h2>
3   <script src="index.js"></script>
4 </body>

```

这是上述代码在操作中的 `Replit`：

`<ReplitEmbed src=”https://replit.com/@newlineauthors/debugger-statement-example1” />`

:::info

您可以使用 `VS Code` 的 [实时服务器](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) 扩展在浏览器中打开上述代码示例。

:::

值 `“18”` 是一个有效值，但我们得到了 `“提供的年龄值无效”` 的输出。这是为什么呢？让我们使用 `debugger` 语句来调试一下。

:::note

在本模块中，使用 `Firefox` 浏览器展示了不同的调试策略。您可以使用 `Firefox`、`Microsoft Edge` 或 `Chrome` 浏览器进行跟随。

:::

您可能已经注意到 `debugger` 语句已经添加到代码中。它仅在调试代码时需要，完成调试后可以移除。但它在代码中并没有任何作用；我们的代码没有在 `debugger` 语句处暂停。为什么会这样？为了让 `debugger` 语句暂停代码执行，我们需要打开浏览器的开发工具。只需打开 [浏览器的开发工具](https://balsamiq.com/support/faqs/browserconsole/)。

打开后，刷新浏览器窗口，您会注意到代码执行已暂停，如下图所示：

![调试器语句暂停时的代码截图](images/module_11----lesson_11.02----public----assets----debugger-screenshot.png)

`debugger`语句暂停时的代码截图

:::info 你可能需要拖动开发者工具窗口以增加其宽度，以匹配上面图像中的布局。窗口的窄宽度可能会显示上面图像中不同区域的不同布局。:::

现在代码执行已暂停，我们可以关注调试器的两个区域：调试器控制和当前作用域中不同变量的值；这两个区域在上面的图像中都有高亮显示。

调试器控制允许我们逐行执行代码，使我们更容易看到每一行代码的执行情况以及它如何影响不同变量的值。

:::info 你可以悬停在调试器控制中的每个按钮上，以了解它的功能。:::

你还可以在上面的图像中看到“Scopes”部分上方的调用栈。这使我们能够查看当前函数是如何被调用的。我们还可以悬停在代码中的不同变量上，以查看它们的值。

:::info 你可以通过双击“Scopes”部分中不同变量的值来更改它们的值。这使我们能够查看如果当前作用域中的变量值发生变化，代码的行为会如何。:::

让我们调试一下为什么当值为`"18"`时我们的代码不工作。注意`age`变量的值（悬停或查看“Scopes”部分）；你会看到它的值是字符串而不是数字。这意味着`prompt`函数（获取用户输入）返回的是一个字符串。所以当我们到达第一个`if`条件，即`age === 18`时，它并不会评估为`true`。你能猜到为什么吗？因为使用三重等号（严格相等）运算符比较字符串和数字总是评估为`false`，你可能知道这一点，但如果你不知道，调试器帮助你知道`age`的值是字符串，并且你正在将其与数字进行比较，所以它确实帮助你更好地理解了你的代码。

现在我们知道问题所在，我们可以通过在比较之前将`age`转换为数字来修复它：

```js
1 const age = Number(prompt("What is your age?"));

```

这是一个简单的示例，向你展示如何使用`debugger`语句来调试我们的代码。浏览器内置的调试器非常强大，值得探索其每一个功能，以提升你的调试技能。

在上一课中，我们使用`debugger`语句来暂停代码执行并调试我们的代码。还有另一种暂停代码执行的方法，那就是使用断点。断点的作用就像`debugger`语句，但不同的是，我们不必在代码中写任何特殊的关键字。相反，我们在浏览器的开发者工具中打开JavaScript代码，并在开发者工具中设置断点。

如前一课所示，我们的`JavaScript`代码在“Debugger”选项卡中打开。在`Chrome`中，相应的选项卡名为“Sources”。这两个浏览器的调试器的整体功能或多或少是相同的。以下是包含我们`JavaScript`代码的`Chrome`浏览器中“Sources”选项卡的截图：

![Chrome开发者工具中的sources选项卡截图](images/module_11----lesson_11.03----public----assets----chrome-sources-tab-screenshot.png)

`Chrome开发者工具中的sources选项卡截图`

现在，我们不使用`debugger`语句来暂停代码执行，而是使用断点。我们将使用与前一课相同的示例，但不使用`debugger`语句。要设置断点，我们首先需要在浏览器中打开我们的代码，打开开发者工具，并在使用`Firefox`浏览器或`Chrome`时打开“Sources”或“Debugger”选项卡（其他浏览器也会有类似的选项卡）。

:::info

如果您在上一课中跟随操作，您可能已经在浏览器中打开了代码；如果没有，您可以在浏览器中打开上一课的代码示例。您可以使用`VS Code`的[live server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)扩展来打开代码示例。

:::

一旦代码在浏览器的开发者工具中打开，设置断点就像点击代码中的行号一样简单。以下图片显示了在代码中设置的两个断点：

![浏览器开发者工具中断点的截图](images/module_11----lesson_11.03----public----assets----breakpoint-screenshot.png)

`浏览器开发者工具中断点的截图`

只需点击要设置断点的行号，然后刷新浏览器窗口。就像使用`debugger`语句一样，当执行到达我们代码中设置的断点时，代码执行将被暂停，从此我们可以使用浏览器调试器提供的不同功能来调试我们的代码。

#### 进一步阅读

+   [调试 JavaScript (Chrome 开发者文档)](https://developer.chrome.com/docs/devtools/javascript/)

`Visual Studio Code` (`VS Code`)是现在最常用的编辑器之一，因其提供的功能和灵活性以及许多可用扩展的帮助而备受欢迎。在`VS Code`提供的众多功能中，有一个内置调试器，允许我们在`VS Code`中调试代码。除了内置调试器，还有许多可用于调试不同语言编写的代码的扩展。

要使用`VS Code`调试我们的代码，请在`VS Code`中打开我们在过去两课中一直在使用的相同代码示例。打开后，在包含我们代码（HTML和JavaScript文件）的文件夹中创建一个名为`.vscode`的文件夹。在`.vscode`文件夹中，创建一个名为`launch.json`的文件，并将以下 JSON 粘贴到该文件中：

```js
 1 {
 2  "version": "0.2.0",
 3  "configurations": [
 4    {
 5      "type": "chrome",
 6      "request": "launch",
 7      "name": "Launch Chrome against localhost",
 8      "file": "${workspaceFolder}/index.html"
 9    }
10   ]
11 }

```

在我们能够运行调试器之前，我们需要设置断点。我们可以在代码中使用`debugger`语句，或者通过点击在`VS Code`中打开的 JavaScript 代码文件中的行号来设置断点。下图显示了在`VS Code`中打开的 JavaScript 代码文件中添加的断点：

![在 VS Code 中添加断点的截图](images/module_11----lesson_11.04----public----assets----vscode-breakpoint.png)

`VS Code`中添加断点的截图

上图中的红点是通过点击行号`5`添加的断点。

在此之后，打开`VS Code`中的“运行和调试”选项，如下图所示：

![VS Code中运行和调试选项的截图](images/module_11----lesson_11.04----public----assets----run-debug-option-vscode.png)

`VS Code`中的运行和调试选项的截图

一旦“运行和调试”窗口打开，如上图所示，点击上图中的绿色播放按钮。这将打开`Chrome`浏览器，当调试器到达断点时，代码执行将暂停。如上图所示，断点添加在行`5`，因此调试器将在用户输入后暂停执行。根据您添加断点的位置，每当代码执行到该点时，执行将被暂停。

下图显示了当代码执行在断点处暂停时`VS Code`的状态：

![VS Code调试器的截图](images/module_11----lesson_11.04----public----assets----vscode-debugger.png)

`VS Code`调试器的截图

你可以在顶部看到调试器控制，这与浏览器中的调试器控制类似。高亮显示的行表示代码执行暂停的点，左侧边栏中有调用栈和当前作用域内的变量。我们可以使用调试器控制向前推进调试器或恢复它，并查看执行流程及作用域内不同变量的值，以调试我们的代码。

#### 进一步阅读：

在`VS Code`中，你可以用调试器做很多事情。我们手动创建的“launch.json”文件可以通过`VS Code`一键自动生成。关于这一点以及`VS Code`调试器的其他功能在`VS Code`文档中都有说明：

+   [调试（VS Code 文档）](https://code.visualstudio.com/docs/editor/debugging)
