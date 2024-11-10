## 栈的实际应用

虽然栈通常不用于长期存储数据，但它可以作为多种算法处理临时数据的一个极佳工具。让我们看一个例子。

让我们创建一个 JavaScript 代码检查器的开端——即一个检查程序员 JavaScript 代码的程序，确保每一行都是语法正确的。JavaScript因其代码中大量的括号而臭名昭著，因此我们将重点关注语法的这一方面。这包括括号、方括号和大括号——这些都是令人沮丧的语法错误的常见原因。

为了解决这个问题，让我们先分析一下在括号方面哪些语法是不正确的。如果我们将其分解，会发现三种语法错误的情况。

第一个情况是当存在一个没有对应闭括号的开括号时，例如：

| ​  | (`let` x = 2; |
| --- | --- |

我们称之为`语法错误类型 #1`。

第二个情况是当出现一个从未之前有对应开括号的闭括号：

| ​  | ​(`let` x = 2;) |
| --- | --- |

我们称之为`语法错误类型 #2`。

第三个情况，我们称之为`语法错误类型 #3`，是当一个闭括号与紧接着的开括号不是同一种括号时：

| ​  | (`let` x = [1, 2, 3)]; |
| --- | --- |

在前面的示例中，有一对匹配的圆括号和一对匹配的方括号，但闭圆括号的位置不对，因为它不匹配紧接着的开括号，即方括号。

我们如何实现一个算法来检查一行 JavaScript 代码，并确保没有与括号相关的语法错误？这就是栈能够让我们实现一个优雅的代码检查算法，其工作原理如下。

我们首先准备一个空栈，然后按照以下规则从左到右读取每个字符：

1.  如果我们发现任何不是括号类型（圆括号、方括号或大括号）的字符，我们将忽略它并继续前进。

1.  如果我们发现一个开括号，我们就将其推入栈中。将其放在栈中意味着我们在等待关闭那个特定的括号。

1.  如果我们发现一个闭括号，我们就弹出栈顶元素并检查它。然后我们分析：

    +   如果我们弹出的项目（它总是一个开括号）与当前的闭括号不匹配，则意味着我们遇到了`语法错误类型 #3`。

    +   如果我们无法弹出一个元素，因为栈是空的，那就意味着当前的闭括号之前没有对应的开括号。这是`语法错误类型 #2`。

    +   如果我们弹出的项目与当前的闭括号相对应，则意味着我们成功关闭了那个开括号，我们可以继续解析这行 JavaScript 代码。

1.  如果我们到达行的末尾，栈中仍有内容，则意味着存在一个没有对应闭括号的开括号，这就是`语法错误类型 #1`。

让我们通过以下示例来看看这一点：

![`images/stacks_and_queues/parens_1_new.png`](images/stacks_and_queues/parens_1_new.png)

在准备一个空栈之后，我们开始从左到右读取每个字符。

第1步：我们从第一个字符开始，它恰好是一个开括号：

![`images/stacks_and_queues/parens_2_new.png`](images/stacks_and_queues/parens_2_new.png)

第2步：由于它是一个开括号的类型，我们将其推入栈中：

![`images/stacks_and_queues/push_open_parens.png`](images/stacks_and_queues/push_open_parens.png)

然后我们忽略所有字符 `let x =`，因为它们不是括号字符。

第3步：我们遇到了下一个开括号：

![`images/stacks_and_queues/parens_3_new.png`](images/stacks_and_queues/parens_3_new.png)

第4步：我们将其推入栈中：

![`images/stacks_and_queues/push_open_curly_brace.png`](images/stacks_and_queues/push_open_curly_brace.png)

然后我们忽略 `y:`。

第5步：我们遇到开方括号：

![`images/stacks_and_queues/parens_4_new.png`](images/stacks_and_queues/parens_4_new.png)

第6步：我们也将其添加到栈中：

![`images/stacks_and_queues/push_open_square_bracket.png`](images/stacks_and_queues/push_open_square_bracket.png)

然后我们忽略 `1`，`2`，`3`。

第7步：我们遇到了第一个闭合括号——一个闭合方括号：

![`images/stacks_and_queues/first_closing_brace_new.png`](images/stacks_and_queues/first_closing_brace_new.png)

第8步：我们弹出栈顶的元素，它恰好是一个开方括号：

![`images/stacks_and_queues/pop_square_bracket.png`](images/stacks_and_queues/pop_square_bracket.png)

由于我们的闭合方括号与栈顶元素相对应，这意味着我们可以继续算法而不会抛出任何错误。

第9步：我们继续，遇到一个闭合大括号：

![`images/stacks_and_queues/parens_6_new.png`](images/stacks_and_queues/parens_6_new.png)

第10步：我们从栈中弹出顶部项：

![`images/stacks_and_queues/pop_curly_brace.png`](images/stacks_and_queues/pop_curly_brace.png)

这是一个开括号，所以我们找到了与当前闭合括号的匹配。

第11步：我们遇到了一个闭合括号：

![`images/stacks_and_queues/parens_7_new.png`](images/stacks_and_queues/parens_7_new.png)

第12步：我们弹出栈中的最后一个元素。它是一个相应的匹配，因此到目前为止没有错误。

因为我们已经遍历了整行代码并且栈是空的，所以我们的静态检查工具可以得出结论，这一行（关于开闭括号）没有语法错误。

### 代码实现：基于栈的代码静态检查工具

下面是前述算法的实现。请注意，我们使用了之前实现的 `Stack` 类：

| ​  | `import` Stack `from` *'./stack.js'*; |
| --- | --- |
| ​  |  |
| ​  | `class` Linter { |
| ​  | `constructor`() { |
| ​  | `this`.stack = `new` Stack(); |
| ​  | } |
| ​  |  |
| ​  | `lint`(text) { |
| ​  | `while` (`this`.stack.read()) { |
| ​  | `this`.stack.pop(); |
| ​  | } |
| ​  |  |
| ​  | `const` 匹配括号 = { `'('`: `')'`, `'['`: `']'`, `'{'`: `'}'` }; |
| ​  |  |
| ​  | `for`(`const` `char` `of` text) { |
| ​  | `if`(`matchingBraces[`char`]) { |
| ​  | `this`.stack.push(`char`); |
| ​  | } `else` `if` (Object.values(matchingBraces).includes(`char`)) { |
| ​  | `if` (!`this`.stack.read()) { |
| ​  | `return` `${`char`} does not have opening brace`; |
| ​  | } `else` { |
| ​  | `const` poppedOpeningBrace = `this`.stack.pop(); |
| ​  |  |
| ​  | `if`(`char` !== `matchingBraces[poppedOpeningBrace]`) { |
| ​  | `return` `${`char`} has mismatched opening brace`; |
| ​  | } |
| ​  | } |
| ​  | } |
| ​  | } |
| ​  |  |
| ​  | `// 如果我们到达行末，且栈不为空：` |
| ​  | `if` (`this`.stack.read()) { |
| ​  | `return` `${`this`.stack.read()} does not have closing brace`; |
| ​  | } |
| ​  |  |
| ​  | `// 如果行没有错误，返回 true：` |
| ​  | `return` `true`; |
| ​  | } |
| ​  | } |

`import Stack from './stack.js'` 允许我们的代码使用我们在上面实现的栈，因为我们将其保存在一个名为 `stack.js` 的文件中。

一旦我们创建了 `Linter` 类的实例，我们就会创建一个算法可以使用的栈。这是通过以下代码实现的：

| ​  | `constructor`() { |
| --- | --- |
| ​  | `this`.stack = `new` Stack(); |
| ​  | } |

主 linting 算法发生在 `lint` 方法中，该方法接受一段 JavaScript 代码的字符串并将其分配给一个名为 `text` 的变量。

我们首先确保栈是空的，因为它可能仍然包含来自之前的 linting 的数据。我们通过不断弹出栈中的数据，直到没有剩余数据：

| ​  | `while`(`this`.stack.read()) { |
| --- | --- |
| ​  | `this`.stack.pop(); |
| ​  | } |

我们随后定义了我们认为是匹配括号的集合：

| ​  | `const` matchingBraces = { `'('`: `')'`, `'['`: `']'`, `'{'`: `'}'` }; |
| --- | --- |

我们现在进入算法的主要部分，它通过循环逐个分析 `text` 中的每个字符：

| ​  | `for`(`const` `char` `of` text) { |
| --- | --- |

如果当前字符是一个开括号，我们将它推入栈中：

| ​  | `if`(`matchingBraces[`char`]) { |
| --- | --- |
| ​  | `this`.stack.push(`char`); |
| ​  | } |

如果当前字符不是一个开括号，我们接着检查它是否可能是一个闭括号：

| ​  | `else` `if` (Object.values(matchingBraces).includes(`char`)) { |
| --- | --- |

`Object.values` 方法给我们提供了一个包含 `matchingBraces` 对象所有值的数组（即一个哈希表），不包含键。在我们的例子中，这些值都是闭括号。

如果当前字符是一个闭括号，我们将考虑几种可能性。我们首先检查栈中是否有任何内容。如果没有，我们触发`语法错误 #2`：

| ​  | `if`​ (!​`this`.stack.read()) { |
| --- | --- |
| ​  | `return` ​*`*​${​`char`​}​ *does not have opening brace`*​; |
| ​  | } |

如果栈中有内容，我们将其弹出并检查它是否是匹配的开括号。如果不是，我们触发`语法错误 #3`：

| ​  | `else`​ { |
| --- | --- |
| ​  | `const`​ `poppedOpeningBrace` = `this`.stack.pop(); |
| ​  |  |
| ​  | `if`​ (`char` !== `matchingBraces[poppedOpeningBrace]`) { |
| ​  | `return` ​*`*​${​`char`​}​ *has mismatched opening brace`*​; |
| ​  | } |
| ​  | } |

循环以这种方式继续，直到处理整个文本。

然而，我们还没有完全完成。我们仍然需要检查栈中是否包含任何内容，因为如果有，说明我们有一个未关闭的孤立开括号。这同样是`语法错误 #1`：

| ​  | `if`​ (`this`.stack.read()) { |
| --- | --- |
| ​  | `return` ​*`*​${​`this`​.stack.read()}​ *does not have closing brace`*​; |
| ​  | } |

在我们的方法结束时，如果处理了整个文本且未遇到任何错误，我们将返回`true`。

这里有一些示例代码来运行我们的 linter：

| ​  | `const`​ `linter` = `new`​ `Linter();` |
| --- | --- |
| ​  | `linter.lint(​*'(let x = 2;'*​)` |

这个例子将会触发 `Syntax Error #1`，因为左括号没有配对的右括号。

在这个例子中，我们使用栈来实现我们的 linter，采用了一个简洁的算法。但是，如果栈的底层实际上使用了数组，那为什么还要使用栈呢？难道我们不能用数组完成同样的任务吗？
