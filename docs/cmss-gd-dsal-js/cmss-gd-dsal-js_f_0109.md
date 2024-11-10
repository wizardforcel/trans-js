## 变位词生成

为了结束我们的讨论，让我们解决迄今为止最复杂的递归问题。我们将利用所有递归工具箱中的资源来使其生效。

我们将编写一个返回给定字符串所有变位词数组的函数。变位词是字符串内所有字符的重新排列。例如，`"abc"`的变位词如下：

| ​  | `["abc",` |
| --- | --- |
| ​  | `"acb",` |
| ​  | `"bac",` |
| ​  | `"bca",` |
| ​  | `"cab",` |
| ​  | `"cba"]` |

现在，假设我们要收集字符串`"abcd"`的所有变位词。让我们对这个问题应用自上而下的思维方式。

可以说，`"abcd"`的子问题是`"abc"`。接下来是这个问题：如果我们有一个正常工作的anagrams函数返回所有`"abc"`的变位词，我们该如何利用它们生成`"abcd"`的所有变位词？想一想，看你能否提出任何方法。

这是我想到的方法。（当然还有其他方法。）

如果我们有`"abc"`的所有六个变位词，我们可以通过在每个变位词的每个可能位置插入`"d"`来获得`"abcd"`的每个排列：

![images/learning_to_write_in_recursive/d_anagram_placement.png](images/learning_to_write_in_recursive/d_anagram_placement.png)

这是该算法的JavaScript实现。你会注意到，它确实比本章前面的例子更复杂：

| ​  | `function` anagramsOf(string) { |
| --- | --- |
| ​  | `if` (string.length === 1) { `return` [string[0]]; } |
| ​  |  |
| ​  | `const` collection = []; |
| ​  |  |
| ​  | `const` substringAnagrams = anagramsOf(string.slice(1)); |
| ​  |  |
| ​  | `for` (`const` substringAnagram `of` substringAnagrams) { |
| ​  | `for` (`let` index = 0; index <= substringAnagram.length; index += 1) { |
| ​  | `const` newString = (substringAnagram.slice(0, index) |
| ​  | `+ string[0]` |
| ​  | `+ substringAnagram.slice(index));` |
| ​  | collection.push(newString); |
| ​  | `}` |
| ​  | `}` |
| ​  |  |
| ​  | `return` collection; |
| ​  | `}` |

这段代码并不简单，所以让我们分解一下。目前我们将跳过基本情况。

我们首先创建一个空数组，用于收集所有变位词的集合：

| ​  | `const` collection = []; |
| --- | --- |

这是我们在函数结束时将返回的同一个数组。

接下来，我们从字符串的子字符串中获取所有变位词的数组。这个子字符串是子问题字符串——即，从第二个字符到末尾。例如，如果字符串是`"hello"`，子字符串就是`"ello"`：

| ​  | `const` substringAnagrams = anagramsOf(string.slice(1)); |
| --- | --- |

注意我们如何使用自上而下的思维方式来假设anagramsOf函数已经在子字符串上正常工作。

然后我们遍历每个substringAnagrams：

| ​  | `for` (`const` substringAnagram `of` substringAnagrams) { |
| --- | --- |

在继续之前，值得注意的是，我们在此时使用了循环和递归的组合。使用递归并不意味着你必须完全消除代码中的循环！我们正在以最自然的方式使用每种工具来帮助我们解决当前的问题。

对于每个子字符串变体，我们遍历其每个索引—加上末尾的一个额外索引。对于每个索引，我们创建一个全新的字符串（称为 `newString`），并用子字符串变体加上当前字符串的第一个字符插入到当前索引处填充：

| ​  | `for` (`let` index = `0`; index <= `substringAnagram.length`; index += `1`) { |
| --- | --- |
| ​  | `const` `newString` = (`substringAnagram.slice(0, index) |
| ​  | + `string[0]` |
| ​  | + `substringAnagram.slice(index));` |

例如，如果字符串是 `"abcd"`，而子字符串变体是 `"bcd"`，我们遍历每个索引（加上末尾的一个额外索引），这将是 `0` 到 `3`，并创建以下新字符串：

| ​  | `"abcd"`​ ​// 在索引 `0` 处插入 `'a'`​ |
| --- | --- |
| ​  | `"bacd"`​ ​// 在索引 `1` 处插入 `'a'`​ |
| ​  | `"bcad"`​ ​// 在索引 `2` 处插入 `'a'`​ |
| ​  | `"bcda"`​ ​// 在索引 `3` 处插入 `'a'`​ |

事实上，子字符串变体 `"bcd"` 并没有索引 `3`，但是我们遍历索引 `3` 以便能够将 `'a'` 插入到子字符串变体的最后。

每个 `newString` 代表一个新的变体，所以我们将其添加到我们的集合中：

| ​  | `collection.push(newString);` |
| --- | --- |

当我们完成时，我们返回变体的集合。

基本情况是子字符串仅包含一个字符，在这种情况下只有一个变体—该字符本身！

### 变体生成的效率

顺便提一下，让我们停下来分析一下我们的变体生成算法的效率，因为我们会发现一些有趣的事情。实际上，生成变体的时间复杂度是一个我们之前未遇到过的新类别的 Big O。

如果我们思考一下生成了多少变体，我们会注意到一个有趣的模式。

对于包含三个字符的字符串，我们创建以三个字符中的每一个字符开头的排列。每个排列然后从剩下的两个字符中选择中间字符，从剩下的最后一个字符中选择最后一个字符。这是 `3 * 2 * 1`，即 `六` 种排列。

查看其他字符串长度，我们得到：

| ​  | `4` 个字符: `4 * 3 * 2 * 1` 个变体 |
| --- | --- |
| ​  | `5` 个字符: `5 * 4 * 3 * 2 * 1` 个变体 |
| ​  | `6` 个字符: `6 * 5 * 4 * 3 * 2 * 1` 个变体 |

你认出这个模式了吗？这是一个阶乘！

所以如果字符串有六个字符，则变体的数量是 `6` 的阶乘。这是 `6 * 5 * 4 * 3 * 2 * 1`，计算得出 `720`。

阶乘的数学符号是感叹号。所以，阶乘 `6` 表示为 `6!`，而 `10` 的阶乘表示为 `10!`。

记住，Big O 表示对关键问题的回答：如果有 `N` 个数据元素，算法将需要多少步？在我们的情况下，`N` 将是字符串的长度。

对于长度为`N`的字符串，我们生成`N!`个字谜。那么在Big O符号中，这表示为`O(N!)`。这也被称为阶乘时间。

`O(N!)`是我们在本书中遇到的最慢的Big O类别。让我们看看它与其他“慢”的Big O类别相比的样子，如图所示`[graph](#fig.ch11.big_o_factorial_graph)`。

`![images/learning_to_write_in_recursive/big_o_factorial_graph.png](images/learning_to_write_in_recursive/big_o_factorial_graph.png)`

尽管`O(N!)`极其缓慢，但我们没有更好的选择，因为我们的任务是生成所有的字谜，而对于一个N字符的单词，确实有`N!`个字谜。

无论如何，递归在这个算法中发挥了关键作用，这是一个递归如何用于解决复杂问题的重要示例。
