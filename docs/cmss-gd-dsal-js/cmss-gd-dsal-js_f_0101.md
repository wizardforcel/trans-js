## `文件系统遍历`

现在你已经看到了递归是如何工作的，我们可以用它来解决某些原本难以解决的问题。

一种适合递归的问题是当我们需要深入多个层次的问题，而不知道有多少层次时。

以遍历文件系统为例。假设你有一个脚本，可以处理目录内的所有内容，比如打印所有子目录的名称。然而，你并不希望脚本只处理直接的子目录——你希望它能够作用于目录内所有子目录的子目录，以及它们所有的子目录，等等。

让我们创建一个简单的脚本，打印给定目录内所有子目录的名称：

| ​  | `import` { `readdirSync`, `lstatSync` } `from` `fs`; |
| --- | --- |
| ​  | `import` { `join` } `from` `path`; |
| ​  |  |
| ​  | `function` printSubdirectories(`directoryName`) { |
| ​  | `for` (`const` `fileName` `of` `readdirSync`(`directoryName`)) { |
| ​  | `if` (`lstatSync`(`fileName`).isDirectory()) { |
| ​  | `const` pathName = `join`(`directoryName`, `fileName`); |
| ​  | `console.log`(`pathName`); |
| ​  | } |
| ​  | } |
| ​  | } |

我们可以通过传入目录名称来调用这个函数。如果我们想在当前目录上调用它，可以写如下代码：

| ​  | printSubdirectories(`'.'`); |
| --- | --- |

在这个脚本中，我们查看给定目录内的每一个文件。如果文件本身是一个子目录，我们就打印子目录的名称。

虽然这工作得很好，但它只打印当前目录下立即存在的子目录的名称。它并不打印那些子目录内的子目录的名称。

让我们更新我们的脚本，使其能够搜索更深一层：

| ​  | `import` { `readdirSync`, `lstatSync` } `from` `fs`; |
| --- | --- |
| ​  | `import` { `join` } `from` `path`; |
| ​  |  |
| ​  | `function` printSubdirectories(`directoryName`) { |
| ​  | `for` (`const` `fileName` `of` `readdirSync`(`directoryName`)) { |
| ​  | `if` (`lstatSync`(`fileName`).isDirectory()) { |
| ​  | `const` pathName = `join`(`directoryName`, `fileName`); |
| ​  | `console.log`(`pathName`); |
| ​  |  |
| ​  | `for` (`const` `fileName2` `of` `readdirSync`(`pathName`)) { |
| ​  | `const` pathName2 = `join`(`pathName`, `fileName2`); |
| ​  | `console.log`(`pathName2`); |
| ​  | } |
| ​  | } |
| ​  | } |
| ​  | } |

现在，每次我们的脚本发现一个目录时，它都会通过该目录的子目录进行一个相同的循环，并打印子目录的名称。但这个脚本也有其局限性，因为它只搜索两层深。我们如果想搜索三层、四层或五层深呢？我们需要五层嵌套循环。

如果我们想搜索子目录的深度，应该怎么做呢？这似乎是不可能的，因为我们甚至不知道有多少层。

而这正是递归真正闪光的地方。使用递归，我们可以编写一个可以无限深入的脚本，并且代码量更少！

| ​  | `import` { `readdirSync`, `lstatSync` } `from` `'fs';` |
| --- | --- |
| ​  | `import` { `join` } `from` `'path';` |
| ​  |  |
| ​  | `function` `printSubdirectories(directoryName) {` |
| ​  | `for` (`const` `fileName` `of` `readdirSync(directoryName)) {` |
| ​  | `const` `pathName` = `join`(`directoryName`, `fileName`); |
| ​  | `if` (`lstatSync(pathName).isDirectory()) {` |
| ​  | `console.log(pathName);` |
| ​  | `printSubdirectories(pathName);` |
| ​  | } |
| ​  | } |
| ​  | } |

当这个脚本遇到文件时，如果它们本身是子目录，它会调用`printSubdirectories`方法来处理那个子目录。因此，脚本可以根据需要深入，不留下任何子目录未处理。

为了可视化这个算法如何作用于示例文件系统，请查看以下图示，它指定了脚本遍历子目录的顺序：

![images/recursively_recurse_with_recursion/filesystem.png](images/recursively_recurse_with_recursion/filesystem.png)
