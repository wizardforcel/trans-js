| Recipe 3 | 使用 startsWith() 和 endsWith() 匹配字符串的开始或结尾 |
| --- | --- |

### 任务

假设你有一个关于宠物护理的文章数据库，你的任务是整理出在文章中得到解答的问题列表。假设这些文章是使用 Markdown 格式编写的，且所有问题都使用二级标题标签（以 ## 开头）。

你会怎么编写代码来区分标题和普通句子？如果你想过滤掉那些问题句子，应该使用什么？你需要一种方法，可以检查字符串的开始和结束字符。

### 解决方案

首先，我们将使用 startsWith() 方法来判断字符串是否以 ## 开头：

[part_1/matching_with_startsWith_endsWith/startsWith_endsWith_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/matching_with_startsWith_endsWith/startsWith_endsWith_ex1.js)

|   | **const** str1 = *"## 为什么巧克力对你的狗不好？"*; |
| --- | --- |
|   | **const** str2 = *"# 10 个惊人的狗狗事实"*; |
|   | **const** searchStr = *"##"*; |
|   |  |
|   | str1.startsWith(searchStr); *// → true* |
|   | str2.startsWith(searchStr); *// → false* |

然后我们将使用 endsWith() 方法来检查字符串是否以问号结尾：

[part_1/matching_with_startsWith_endsWith/startsWith_endsWith_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/matching_with_startsWith_endsWith/startsWith_endsWith_ex2.js)

|   | **const** str1 = *"## 为什么巧克力对你的狗不好？"*; |
| --- | --- |
|   | **const** str2 = *"## 如何修剪狗狗的指甲"*; |
|   | **const** searchStr = *"?"*; |
|   |  |
|   | str1.endsWith(searchStr); *// → true* |
|   | str2.endsWith(searchStr); *// → false* |

现在我们知道 startsWith() 和 endsWith() 方法能产生我们想要的结果，接下来我们创建一个同时执行这两个操作的函数：

[part_1/matching_with_startsWith_endsWith/startsWith_endsWith_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/matching_with_startsWith_endsWith/startsWith_endsWith_ex3.js)

|   | **函数** startsWithEndsWith(str, start, end) { |
| --- | --- |
|   | **如果** ((str.startsWith(start) === **true**) && (str.endsWith(end) === **true**)) { |
|   | **返回** **true**; |
|   | } **否则** { |
|   | **返回** **false**; |
|   | } |
|   | } |

我们还可以通过去除 if 语句来简化函数。逻辑与（&&）运算符会在 startsWith() 和 endsWith() 都返回 true 时返回 true，因此我们可以通过一个语句获得相同的结果：

[part_1/matching_with_startsWith_endsWith/startsWith_endsWith_ex4.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/matching_with_startsWith_endsWith/startsWith_endsWith_ex4.js)

|   | **函数** startsWithEndsWith(str, start, end) { |
| --- | --- |
|   | **返回** str.startsWith(start) && str.endsWith(end); |
|   | } |

这段代码对于测试包含单一句子的字符串效果很好，但我们希望从文章中提取二级 Markdown 标题。因此，我们需要一种方法，将文章的每一行传递给我们的函数。通过调用 split("\n") 将字符串按换行符分割，然后使用 forEach() 遍历结果数组，并将每一行传递给 startsWithEndsWith()：

[part_1/matching_with_startsWith_endsWith/startsWith_endsWith_ex5.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/matching_with_startsWith_endsWith/startsWith_endsWith_ex5.js)

|   | **const** str = |
| --- | --- |
|   | *`## 为什么巧克力对你的狗有害？* |
|   | *一些文本 ...* |
|   | *## 给你的狗修剪指甲的最佳方法* |
|   | *更多文本 ...* |
|   | *## 是否有对狗安全的人类食物？* |
|   | *...`*; |
|   |  |
|   | **函数** startsWithEndsWith(str, start, end) { |
|   | **返回** str.startsWith(start) && str.endsWith(end); |
|   | } |
|   |  |
|   | str.split(*"***\***n"*).forEach(str => { |
|   | **if** (startsWithEndsWith(str, *"##"*, *"?"*)) { |
|   | console.log(str); |
|   | }; |
|   | }); |
|   |  |
|   | *// 输出日志：* |
|   | *// → ## 为什么巧克力对狗有害？* |
|   | *// → ## 是否有对狗狗安全的人类食物？* |

成功！

| 浏览器兼容性 |
| --- |
| ![images/aside-icons/info.png](images/aside-icons/info.png) | Safari 15.4 版本于 2022 年 3 月 15 日发布，稍晚于其他主流浏览器加入该功能，因为它在其他竞争对手已实现 at() 后才加入。为了与旧版浏览器兼容，你需要使用 polyfill。^([[2]](f_0032.xhtml#FOOTNOTE-2)) 在 Node 环境中，你需要至少 Node 版本 16.6.0。^([[3]](f_0032.xhtml#FOOTNOTE-3)) |

### 讨论

在 JavaScript 中，完成任务的方法通常有多种。作为程序员，你通常应该努力使用最有效的工具来完成工作。但你也应该考虑代码的可靠性和可读性，这在大多数项目中更为重要。

获取字符串最后一个字符的另一种方法是使用 at() 方法。它简洁且快速！但是浏览器的支持还不完全，因此你可能会在较旧的浏览器中发现代码无法运行。

使用 at() 方法，你可以像这样获取字符串中某个位置的单个字符：

[part_1/matching_with_startsWith_endsWith/startsWith_endsWith_ex6.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/matching_with_startsWith_endsWith/startsWith_endsWith_ex6.js)

|   | **const** str = *"狗狗会做梦吗？"*; |
| --- | --- |
|   |  |
|   | str.at(-1); *// → "?"* |
|   | str.at(-2); *// → "m"* |

当使用负数调用 at() 时，该方法会从字符串的末尾开始计数。因此，-1 获取的是最后一个字符，-2 获取的是倒数第二个字符，依此类推。

| 调用 at() 方法处理数组 |
| --- |
| ![images/aside-icons/tip.png](images/aside-icons/tip.png) | 你还可以在 JavaScript 数组中使用 at()。查看我在 Medium 上的文章了解更多内容。^([[4]](f_0032.xhtml#FOOTNOTE-4)) |

虽然 startsWith() 让你检查字符串开头的字符，endsWith() 让你判断一个字符串是否以特定字符结尾。如果你只想获取单个字符的值，那么 at() 是一个简洁的替代方案，但请确保检查浏览器的支持情况。
