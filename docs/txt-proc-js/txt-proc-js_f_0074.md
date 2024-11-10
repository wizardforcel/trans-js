| 配方 62 | 移除重复的空白字符 |
| --- | --- |

### 任务

假设你发现博客上的客人帖子不仅包含多余的空格字符，还包含其他空白字符，如制表符。因此，这次你想要替换所有空白字符，包括空格、制表符 (\t)、换行符 (\n)、回车符 (\r)、垂直制表符 (\v)、换页符 (\f) 等。

例如，考虑以下字符串，其中“My”和“life”之间的空格由两个制表符字符组成。你可以通过在字符串中搜索 \t 来确认制表符字符的存在：

[part_3/removing_dup_whitespaces/removing_dup_whitespaces_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_3/removing_dup_whitespaces/removing_dup_whitespaces_ex1.js)

|   | **const** str = *"我的生活需要编辑。"*; |
| --- | --- |
|   |  |
|   | */My**\t\t**/*.test(str); *// → true* |

你需要一个解决方案，能够找到重复的制表符或其他空白字符，并将它们替换为一个单一的空格。

### 解决方案

使用 \s 字符类来匹配一个空白字符，然后再次使用 \s 来匹配第一个空白字符后面的所有额外空白字符：

[part_3/removing_dup_whitespaces/removing_dup_whitespaces_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_3/removing_dup_whitespaces/removing_dup_whitespaces_ex2.js)

|   | **const** str = *"我的生活需要编辑。"*; |
| --- | --- |
|   |  |
|   | **function** removeExtraWhitespaces(str) { |
|   | **const** re = */**\s\s**+/g*; |
|   | **return** str.replace(re, *" "*); |
|   | } |
|   |  |
|   | removeExtraWhitespaces(str); |
|   | *// → "我的生活需要编辑。"* |

这个函数的目的是将所有重复的空白字符（两个或更多）替换为一个单一的空格字符。注意输出开始时有一个单一的空白字符。为了确保该函数还可以去除任何额外的前导/尾随空白字符，你应该在返回输出字符串之前应用 trim()：

[part_3/removing_dup_whitespaces/removing_dup_whitespaces_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_3/removing_dup_whitespaces/removing_dup_whitespaces_ex3.js)

|   | **const** str = *" 我的生活需要编辑。"*; |
| --- | --- |
|   |  |
|   | **function** removeExtraWhitespaces(str) { |
|   | **const** re = */**\s\s**+/g*; |
|   | str = str.replace(re, *" "*); |
|   | str = str.trim(); |
|   | **return** str; |
|   | } |
|   |  |
|   | removeExtraWhitespaces(str); |
|   | *// → "我的生活需要编辑。"* |

任务完成！

### 讨论

在JavaScript中，“空格”和“空白字符”并不是同一个概念。空格字符是当你按下键盘上的空格键时得到的字符。而空白字符是一个更广泛的术语，包含了任何表示文本中空白区域的字符。理解这两种字符之间的区别非常重要，因为它们可能对你的代码产生不同的影响。

本例中的解决方案替换了任何类型的空白字符，因此如果换行符（\n）出现在制表符（\t）之后，它们都会被替换为空格。如果你的目的是只替换某种特定类型的空白字符，那么下面的替代方案可能更适合你的需求。

| \s的否定形式 |
| --- |
| ![images/aside-icons/tip.png](images/aside-icons/tip.png) | 记住，当你使用大写的\S时，它的作用是\s小写字母的否定形式。\S可以匹配任何不是空白字符的字符。 |
