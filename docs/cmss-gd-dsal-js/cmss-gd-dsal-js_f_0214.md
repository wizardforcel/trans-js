## `第 9 章`

这些是[`练习`](f_0095.xhtml#stacks.and.queues.exercises)部分中找到的习题的解决方案。

1.  可以推测，我们希望对来电者友好，并按接收顺序接听他们的电话。为此，我们会使用队列，以FIFO（先进先出）方式处理数据。

1.  我们能够读取`4`，它现在是栈中的顶部元素。这是因为我们已经弹出了之前位于`4`上方的`6`和`5`。

1.  我们能够读取`3`，它现在位于队列的前面，在将`1`和`2`出队之后。

1.  我们可以利用栈的特性，因为我们以与推入栈的顺序相反的顺序弹出每个项目。因此，我们将首先将字符串的每个字符推入栈中。然后，我们在将它们添加到新字符串的末尾时弹出每一个：

    | ​  | `import` Stack `from` *'./stack.js'*; |
    | --- | --- |
    | ​  |  |
    | ​  | `function` reverse(string) { |
    | ​  | `const` stack = `new` Stack(); |
    | ​  | `let` newString = *''*; |
    | ​  |  |
    | ​  | `for` (`const` **char** `of` string) { |
    | ​  | `stack.push(`**char**`);` |
    | ​  | } |
    | ​  |  |
    | ​  | `while` (stack.read()) { |
    | ​  | newString += stack.pop(); |
    | ​  | } |
    | ​  |  |
    | ​  | `return` newString; |
    | ​  | } |

    在我们代码开头导入的 Stack 类是我们自己实现的 Stack，来自`第 9 章`，我们将其保存在名为`stack.js`的文件中。
