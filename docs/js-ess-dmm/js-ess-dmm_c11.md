`第11章`

# `十种JavaScript调试策略`

`在本章中`

![Bullet](images/check.png) `使用控制台调试、断点和其他开发者工具`

![Bullet](images/check.png) `编写便于调试的代码`

![Bullet](images/check.png) `巧妙地通过注释进行调试`

对于任何非平凡的JavaScript代码，几乎没有（可能不存在！）脚本在第一次（甚至第十次！）运行时完全正确。脚本错误发生在即使是最有经验的开发者身上，因此代码中出现错误并不意味着您是一个失败的编码者！这只是意味着您是一个编码者。

但是，当错误进入您的代码时，您会想尽快消灭它们。本章为您提供了十种调试策略，可以帮助您。## `前往开发者工具`

所有网页调试都始于访问您的网页浏览器开发工具。在每个浏览器中，打开开发工具的最快方法是右键点击页面元素，然后点击`Inspect`。您也可以按`Ctrl+Shift+I`（Windows）或`Option⌘  +I`（macOS）。## `控制台是您最好的调试伙伴`

在您的代码中，您可以通过将该值输出到开发工具的控制台选项卡来查看变量或对象属性的当前值：

`console.log(output);`

替换`output`为您想要在控制台打印的表达式。输出表达式可以是文本字符串、变量、对象属性、函数结果或这些的任意组合。## `为您的代码设置断点`

暂停您的代码使您能够看到发生了什么，并在控制台中运行一些命令。您有两种方式可以在执行过程中暂停代码：

+   `设置断点。` 在开发工具中，打开包含JavaScript代码的文件，找到您想要暂停的语句，然后点击该语句左侧的行号。

+   `添加一个` `debugger` `语句。` 在您的JavaScript代码中，在您想要暂停的语句之前添加一个`debugger`语句。## `逐步调试您的代码`

一旦您的JavaScript代码处于断点模式，使用开发工具执行控制来逐行执行代码。您可以逐语句执行、跳过函数或进入函数。## `监视变量和对象属性值`

使用`console.log()`语句将值输出到控制台，或者当您的代码处于断点模式时，将鼠标指针悬停在变量或对象上，以在工具提示中查看其当前值。您还可以创建监视表达式来监视值。## `缩进您的代码`

JavaScript代码在每个语句块中缩进时更具可读性。可读性强的代码更容易追踪和理解，因此您的调试工作有一个更少的障碍需要克服。通常，每个语句缩进两个或四个空格。## `分解复杂任务`

不要试图一次性解决所有问题。如果您有一个大型脚本或函数没有正常工作，最好将其分成小块进行测试，以便缩小问题的范围。  ## 拆分长语句

脚本调试中最复杂的方面之一是理解长语句（特别是表达式）。`控制台`窗口可以帮助您（您可以用它打印语句的部分内容），但通常最好将语句保持尽可能简短。一旦您的代码开始正常工作，您通常可以重新组合语句，以提高代码效率。  ## 注释掉有问题的语句

如果某个特定语句让您头疼，您可以通过在行首加上两个斜杠（`//`）来暂时停用它。这告诉JavaScript将该行视为注释。如果有多行语句您希望跳过，可以在第一行的开头加上`/*`，在最后一行的末尾加上`*/`。 ## 使用注释记录您的脚本

说到注释，有一个编程公理，那就是您永远无法为您的代码添加足够的解释性注释。您添加的注释越多，您的脚本就越容易调试。
