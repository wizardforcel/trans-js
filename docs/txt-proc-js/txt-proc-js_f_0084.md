| Recipe 72 | 实时高亮文本 |
| --- | --- |

### 任务

假设你想在应用程序中添加一个类似于 Google Chrome “页面查找”工具的搜索功能。使用此功能时，当用户在搜索框中输入查询时，Chrome 会实时高亮显示页面上的相应文本。这使得用户能够迅速定位他们正在寻找的信息，而无需手动扫描整个页面。

### 解决方案

定义一个包含输入元素和包含一些文本的 div 元素的 HTML 页面。输入元素的 ID 应为“search-input”，div 元素的 ID 应为“search-results”：

[part_3/highlighting_in_realtime/highlighting_in_realtime_ex1.xhtml](http://media.pragprog.com/titles/fkjavascript/code/part_3/highlighting_in_realtime/highlighting_in_realtime_ex1.xhtml)

|   | *<!DOCTYPE html>* |
| --- | --- |
|   | <html> |
|   | <head> |
|   | <script src=*"highlighting_in_realtime_ex1.js"* defer></script> |
|   | </head> |
|   | <body> |
|   | <input type=*"text"* id=*"search-input"* placeholder=*"搜索..."*> |
|   | <div id=*"search-results"*>蛇可是非常有个性的。你见过 |
|   | 它们的穿衣品味如何？全是条纹和鳞片，仿佛它们在努力 |
|   | 既能是斑马，又能是龙。但不要让它们的平滑 |
|   | 别让它们的动作骗了你——蛇在需要时可真是“嘶嘶”大作。 |
|   | </div> |
|   | </body> |
|   | </html> |

现在，创建 JavaScript 代码，获取输入并高亮显示文本：

[part_3/highlighting_in_realtime/highlighting_in_realtime_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_3/highlighting_in_realtime/highlighting_in_realtime_ex1.js)

|   | **const** searchInput = document.querySelector(*"#search-input"*); |
| --- | --- |
|   | **const** searchResults = document.querySelector(*"#search-results"*); |
|   | **const** content = searchResults.innerHTML; |
|   |  |
|   | **function** highlightText() { |
|   | **const** searchText = searchInput.value.trim().toLowerCase(); |
|   |  |
|   | **if** (searchText.length > 0) { |
|   | **const** searchRegex = **new** RegExp(searchText, *"gi"*); |
|   | **const** highlightedText = content.replace(searchRegex, *"<mark>$&</mark>"*); |
|   |  |
|   | searchResults.innerHTML = highlightedText; |
|   | } **else** { |
|   | searchResults.innerHTML = content; |
|   | } |
|   | } |
|   |  |
|   | searchInput.addEventListener(*"input"*, highlightText); |

这段代码创建了一个实时搜索功能，用户在输入框中键入时，所有匹配的搜索词都会在“search-results”div元素中高亮显示。

### 讨论

JavaScript代码首先创建了对输入框、div元素及其内容的引用。我们使用addEventListener()方法为输入框元素添加了一个事件监听器。该事件监听器会监听输入框值的变化，并在输入变化时触发highlightText()函数。

在highlightText()函数内部，我们获取输入框中的值，去除前后空白字符，将剩余的字符串转换为小写，并将结果存储在searchText变量中。

接下来，我们检查searchText的长度是否大于零。如果是，我们使用给定的输入创建一个正则表达式对象。我们还将g和i标志作为第二个参数传递，表示正则表达式应该全局匹配所有出现的地方，并且不区分大小写。

使用content变量的replace()方法，我们将所有搜索文本的出现位置替换为用HTML <mark>标签包裹的相同文本。最后，我们更新searchResults元素的innerHTML属性，以显示高亮的文本。

如果 `searchText` 的长度为零，我们将 `innerHTML` 属性设置为原始内容变量，这样就会显示文本的初始内容。这个步骤至关重要，因为如果用户删除了整个搜索词，文本就不应该再有高亮。

用户越来越期待能够实时响应他们操作的互动和动态界面。实时文本高亮就是其中一个日益流行的功能。利用这一点，可以使您的用户更容易找到他们需要的信息。

| 保护您的应用免受 ReDoS 攻击 |
| --- |
| ![images/aside-icons/warning.png](images/aside-icons/warning.png) | 当在正则表达式模式中重新使用用户提供的文本时，请小心。如果没有正确清理文本，您的应用可能会受到 ReDoS 攻击的威胁。要了解更多信息，请参见配方 66，[*在正则表达式中转义字符串*](f_0078.xhtml#rcp.escaping_metacharacters)。 |
