## 第11章

这些是[练习](f_0111.xhtml#learning.to.write.in.recursive.exercises)部分中找到的练习的解决方案。

1.  让我们将函数命名为`characterCount`。第一步是假装`characterCount`函数已经实现。

    接下来，我们需要识别子问题。如果我们的问题是数组`["ab", "c", "def", "ghij"]`，那么我们的子问题可以是少了一个字符串的同一个数组。我们具体说一下，我们的子问题是去掉第一个字符串后的数组，也就是`["c", "def", "ghij"]`。

    现在，让我们看看在子问题上应用“已经实现”的函数会发生什么。如果我们调用`characterCount(["c", "def", "ghij"])`，我们会得到一个返回值8，因为总共有八个字符。

    所以，要解决我们最初的问题，我们只需将第一个字符串（`"ab"`）的长度加到调用`characterCount`函数的子问题结果上。

    这是一个可能的实现：

    | ​  | `function` `characterCount`(array) { |
    | --- | --- |
    | ​  | `// 基本情况：当数组为空时：` |
    | ​  | `if` (array.length === 0) { `return` 0; } |
    | ​  |  |
    | ​  | `return` array[0].length + `characterCount`(array.slice(1)); |
    | ​  | } |
    | ​  | `export` `default` `characterCount`; |

    请注意，我们的基本情况是一个空数组，在这种情况下没有字符可以计算。

1.  首先，让我们假装`selectEven`函数已经正常工作。接下来，识别子问题。如果我们试图在示例数组`[1, 2, 3, 4, 5]`中选择所有的偶数，我们可以说子问题是数组中除了第一个数的所有数。所以我们假设`selectEven([2, 3, 4, 5])`已经正常工作并返回`[2, 4]`。

    因为数组中的第一个数字是1，我们只想返回`[2, 4]`。然而，如果数组中的第一个数字是0，我们想返回`[2, 4]`并加上0。

    我们的基本情况是一个空数组。

    这是一个可能的实现：

    | ​  | `function` `selectEven`(array) { |
    | --- | --- |
    | ​  | `if` (array.length === 0) { `return` []; } |
    | ​  |  |
    | ​  | `if` (array[0] % 2 === 0) { |
    | ​  | `return` [array[0]].concat(`selectEven`(array.slice(1))); |
    | ​  | } `else` { |
    | ​  | `return` `selectEven`(array.slice(1)); |
    | ​  | } |
    | ​  | } |

1.  三角数的定义是n加上序列中的前一个数，n指的是数字在模式中的位置。（例如，如果我们在计算序列的第七个数字，那么n就是7。）如果我们的函数名为`triangle`，我们可以简单地表示为n + `triangle`(n - 1)。基本情况是n为1。

    | ​  | `function` `triangle`(n) { |
    | --- | --- |
    | ​  | `if` (n === 1) { `return` 1; } |
    | ​  |  |
    | ​  | `return` n + `triangle`(n - 1); |
    | ​  | } |

1.  -   让我们假装我们的函数`indexOfX`已经实现。接下来，假设子问题是去掉第一个字符后的字符串。例如，如果我们的输入字符串是`"hex"`，那么子问题就是`"ex"`。

    -   现在，`indexOfX("ex")`将返回1。要计算原始字符串中`"x"`的索引，我们需要在这个值上加1，因为字符串前面的额外`"h"`将`"x"`向下移动了一个索引。下面是我们的代码：

    | ​  | `function` indexOfX(string) { |
    | --- | --- |
    | ​  | `if` (string[0] === `'x'`) { `return` 0; } |
    | ​  |  |
    | ​  | `return` indexOfX(string.slice(1)) + 1; |
    | ​  | } |

1.  -   这个练习类似于楼梯问题。让我们分解一下：

    -   从起始位置，我们只有两个移动选择。我们可以向右移动一个位置，或者向下移动一个位置。

    -   这意味着，唯一最短路径的总数将是从`S`右边空间的路径数 + 从`S`下方空间的路径数。

    -   从`S`右边空间的路径数量等同于在一个六列三行的网格中计算路径，如下所示：

    ![images/learning_to_write_in_recursive/unique_paths_move_right_shaded.png](images/learning_to_write_in_recursive/unique_paths_move_right_shaded.png)

    -   从`S`下方空间的路径数量等同于在一个七列两行的网格中的路径：

    ![images/learning_to_write_in_recursive/unique_paths_move_down_shaded.png](images/learning_to_write_in_recursive/unique_paths_move_down_shaded.png)

    -   递归允许我们优雅地表达这一点：

    | ​  | `return` uniquePaths(rows - 1, columns) + uniquePaths(rows, columns - 1); |
    | --- | --- |

    -   现在我们需要做的就是添加基本情况。可能的基本情况包括当我们只有一行或一列时，因为在这种情况下，我们只有一条路径可供选择。

    -   这是完整的函数：

    | ​  | `function` uniquePaths(rows, columns) { |
    | --- | --- |
    | ​  | `if` (rows === 1 | | columns === 1) { |
    | ​  | `return` 1; |
    | ​  | } |
    | ​  |  |
    | ​  | `return` uniquePaths(rows - 1, columns) + uniquePaths(rows, columns - 1); |
    | ​  | } |
