| 配方 7 | 使用 DOMParser() 从文本中移除 HTML 标签 |
| --- | --- |

### 任务

假设你写了一个网页爬虫，用来从网络收集新闻。你抓取的文本可能包含不需要的 HTML 元素，比如 <span>、<img>、<a> 等。

更糟糕的是，它可能包含注入的 JavaScript 代码，一旦你将其放到网站上，这些代码会自动执行。你需要的是一个安全地移除文本中所有不需要的元素的函数。

### 解决方案

使用 DOMParser() 接口中的 parseFromString() 方法来解析字符串。一旦解析了字符串，你就可以使用 textContent 属性获取不带任何多余 HTML 标签的文本：

[part_1/removing_html_tags/DOMParser_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/removing_html_tags/DOMParser_ex1.js)

|   | **function** stripHTML(html){ |
| --- | --- |
|   | **const** doc = **new** DOMParser().parseFromString(html, *"text/html"*); |
|   | **return** doc.body.textContent &#124;&#124; *""*; |
|   | } |
|   |  |
|   | **const** rawText = *'<a href="">Fed</a> Signals<img src="n.png"> Smaller Rises'*; |
|   |  |
|   | stripHTML(rawText); *// → "美联储信号较小的加息"* |

DOMParser 接口允许你将字符串中的 XML 或 HTML 代码解析为 DOM 文档。在这个例子中，你需要解析 HTML，所以你将 "text/html" 作为第二个参数传入。结果是一个 HTMLDocument，你可以使用 textContent 提取其中的文本。

| Node 中的 DOMParser() |
| --- |
| ![images/aside-icons/warning.png](images/aside-icons/warning.png) | DOMParser() 接口在 Node 环境中不可用。 |

### 讨论

textContent 属性可以在所有文本和元素节点上使用。那么，为什么不直接在页面上创建一个临时元素来获取它的 textContent，而非解析 HTML 呢？请参考这个例子：

[part_1/removing_html_tags/DOMParser_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/removing_html_tags/DOMParser_ex2.js)

|   | *// 不要使用这个* |
| --- | --- |
|   | **function** stripHTML(html) { |
|   | **const** tmp = document.createElement(*"DIV"*); |
|   | tmp.innerHTML = html; |
|   | **return** tmp.textContent &#124;&#124; *""*; |
|   | } |
|   |  |
|   | **const** rawText = *'<a href="">Fed</a> Signals<img src="n.png"> Smaller Rises'*; |
|   |  |
|   | stripHTML(rawText); *// → "Fed Signals Smaller Rises"* |

初看之下，这段代码似乎是更高效的解决方案，因为它没有涉及字符串解析。但如果源代码中包含恶意代码，你就会让你的代码暴露在攻击之下。

尝试从 HTML 中剥离以下文本，你会发现 onerror 属性中隐藏的 JavaScript 代码被执行了：

[part_1/removing_html_tags/DOMParser_ex3.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/removing_html_tags/DOMParser_ex3.js)

|   | **const** rawText = *"<img onerror='alert(**\"**execute JS here**\"**)' src=untrusted>"*; |
| --- | --- |

尽管你将文本插入了一个临时标签中，浏览器仍然会加载图片，嵌入的 JavaScript 代码有机会被触发。

在抓取和使用外部来源的文本时，记得移除 HTML 标签。一种快速的方法是使用 DOMParser 接口解析数据，然后通过 textContent 提取文本。
