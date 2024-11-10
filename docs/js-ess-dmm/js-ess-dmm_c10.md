第 10 章

# `Dealing with Form Data`

`IN THIS CHAPTER`

![Bullet](images/check.png) `Coding text boxes`

![Bullet](images/check.png) `Programming checkboxes, radio buttons, and selection lists`

![Bullet](images/check.png) `Monitoring and triggering form events`

![Bullet](images/check.png) `Dealing with the form data`

在本章中，您将学习如何通过将 HTML 表单连接到一些 JavaScript 代码来“接线”。您将探索各种与表单相关的对象，然后开始编码文本字段、复选框、单选按钮和选择列表。您还将深入了解表单事件的有用世界，甚至学习如何使用键盘快捷键增强您的表单控件。最后，您将疯狂学习如何使用 Web 存储 API 存储表单数据。  ## `Coding Text Fields`

基于文本的字段是最常用的表单元素，大多数使用`<input>`标签。`input`元素有很多属性，但从编码的角度来看，您通常只对四个属性感兴趣：

`<input id="textId" type="textType" name="textName" value="textValue">`

下面是各部分的说明：

+   `textId`: 文本字段的唯一标识符

+   `textType`: 您想在表单中使用的文本字段类型

+   `textName`: 您分配给字段的名称

+   `textValue`: 字段的初始值（如果有）

### 按字段类型引用

一种常见的表单脚本技术是在每个相同类型的字段上运行操作。例如，您可能想要对所有 URL 字段应用样式。下面是用于选择给定类型的所有`input`元素的 JavaScript 选择器：

`document.querySelectorAll('input[type=url]')`

**注意：**`fieldType`是您想要选择的`type`属性值，例如`text`或`url`。

这里是一个示例，其中 JavaScript 返回所有使用类型`url`的`input`元素的集合：

HTML:

`<label for="url1"> Site 1: </label> <input id="url1" type="url" name="url1" value="https://"> <label for="url2"> Site 2: </label> <input id="url2" type="url" name="url2" value="https://"> <label for="url3"> Site 3: </label> <input id="url3" type="url" name="url3" value="https://">`

JavaScript:

`const urlFields = document.querySelectorAll('input[type=url]'); console.log(urlFields);`  ### 获取文本字段值

您的脚本可以通过使用字段对象的值相关属性之一来获取任何文本字段的当前值：

`field.value field.valueAsDate field.valueAsNumber`

下面是一个示例：

HTML:

`<label for="search-field"> Search the site: </label> <input id="search-field" name="q" type="search">`

JavaScript:

`const searchString = document.getElementById('search-field').value; console.log(searchString);`  ### 设置文本字段值

要更改文本字段值，请将新字符串分配给字段对象的`value`属性：

`field.value = value`

下面是各部分的说明：

+   `field`: 您想要操作的表单字段对象的引用

+   `value`：你想要分配给文本字段的字符串

这是一个示例：

HTML:

`<label for="homepage-field"> Type your homepage address: </label> <input id="homepage-field" name="homepage" type="url" value="HTTPS://PAULMCFEDRIES.COM/"">`

JavaScript:

`const homepageField = document.getElementById('homepage-field'); const homepageURL = homepageField.value; homepageField.value = homepageURL.toLowerCase();`

HTML定义了一个类型为`url`的`input`元素，其中默认值为全大写字母。JavaScript代码获取一个URL，将其转换为全小写字母，然后返回到同一`url`字段。如[图10-1](#c10-fig-0001)所示，文本框现在显示全小写字母。

![CaptionThe script converts the input element’s default text to all-lowercase letters. The fields below reads, type your homepage address.](images/9781394263219-fg1001.png)

[FIGURE 10-1:](#rc10-fig-0001) 该脚本将`input`元素的默认文本转换为全小写字母。 ## 编程复选框

你在网页表单中使用复选框来切换设置的开启（即复选框被选中）和关闭（复选框未被选中）。你可以通过在表单中包含以下版本的`<input>`标签来创建复选框：

`<input id="*checkId*" type="checkbox" name="*checkName*" value="*checkValue*" [checked]>`

这是各个部分的说明：

+   `checkId`：复选框的唯一标识符。

+   `checkName`：你想要分配给复选框的名称。

+   `checkValue`：你想要分配给复选框的值。请注意，这是一个隐藏值，脚本可以在表单提交时访问；用户不会遇到它。

+   `checked`：当这个可选属性存在时，复选框最初被选中。

### 引用复选框

如果你的代码需要引用页面中的所有复选框，请使用以下选择器：

`document.querySelectorAll('input[type=checkbox]')`

如果你只想要某个特定表单中的复选框，可以在表单的`id`值上使用后代或子选择器：

`document.querySelectorAll('#*formid* input[type=checkbox]')`

或者：

`document.querySelectorAll('#*formid* > input[type=checkbox]')`  ### 获取复选框状态

你的代码需要知道复选框是被选中还是未选中。这称为复选框的 `state`（状态）。在这种情况下，你需要检查复选框对象的 `checked` 属性：

`*checkbox*.checked`

`checked` 属性返回 `true` 表示复选框已选中，返回 `false` 表示复选框未选中。

这是一个示例：

HTML:

`<label> <input id="autosave" type="checkbox" name="autosave"> 自动保存此项目 </label>`

JavaScript:

``const autoSaveCheckBox = document.querySelector('#autosave'); if (autoSaveCheckBox.checked) { console.log(`${autoSaveCheckBox.name} 已选中`); } else { console.log(`${autoSaveCheckBox.name} 未选中`); }``

JavaScript 代码将复选框对象的引用存储在 `autoSaveCheckBox` 变量中。然后，`if` 语句检查该对象的 `checked` 属性，并根据 `checked` 返回 `true` 或 `false` 来在控制台显示不同的消息。  ### 设置复选框状态

要将复选框字段设置为选中或未选中状态，可以将布尔表达式赋值给 `checked` 属性：

``*checkbox*.checked = true|false``

例如，假设你有一个包含大量复选框的表单，并希望设置该表单使用户最多只能选择三个复选框。以下是完成这项工作的代码：

``document.querySelector('form').addEventListener('click', event => {  // 确保点击的是复选框 if (event.target.type === 'checkbox') {  // 获取已选中复选框的总数 const totalSelected = document.querySelectorAll('input[type=checkbox]:checked').length;  // 是否有超过三个复选框被选中？ if (totalSelected > 3) {  // 如果是，取消选中刚才点击的复选框 event.target.checked = false; } } });``

这个事件处理程序会在 `form` 元素内部的任何内容被点击时运行，并将点击事件作为参数 `event` 传递。然后，代码使用 `:checked` 选择器来返回所有具有 `checked` 属性的 `checkbox` 元素集合，`length` 属性告诉你集合中有多少个元素。`if` 语句检查是否有超过三个复选框被选中。如果是这样，代码会取消选中刚才点击的复选框。  ## 编写单选按钮代码

你可以使用以下方式创建一个单选按钮：

``<input id="*radioId*" type="radio" name="*radioGroup*" value="*radioValue*" [checked]>``

以下是各部分的解释：

+   ``*radioId*``: 单选按钮的唯一标识符。

+   ``*radioGroup*``: 你希望赋给单选按钮组的名称。所有使用相同 `name` 值的单选按钮都属于该组。

+   ``*radioValue*``: 你希望赋给单选按钮的值。如果该单选按钮在表单提交时被选中，那么这个值将包含在提交中。

+   ``checked``: 当此可选属性存在时，单选按钮将被默认选中。

### 引用单选按钮

如果你的代码需要与页面中的所有单选按钮一起工作，可以使用以下 JavaScript 选择器：

``document.querySelectorAll('input[type=radio]')``

如果你想获取某个特定表单中的单选按钮，可以在表单的 `id` 值上使用后代或子选择器：

``document.querySelectorAll('#*formid* input[type=radio]')``

或者：

``document.querySelectorAll('#*formid* > input[type=radio]')``

如果你只需要某个特定组的单选按钮，可以使用以下 JavaScript 选择器，其中 ``*radioGroup*`` 是该组的共同名称：

``document.querySelectorAll('input[name=*radioGroup*]')``  ### 获取单选按钮的状态

如果你的代码需要知道某个特定的单选按钮是被选中还是未选中，你需要确定单选按钮的 `state`。你可以通过检查单选按钮的 `checked` 属性来实现，如下所示：

`radio.checked`

如果单选按钮被选中，`checked` 属性返回 `true`，如果按钮未选中，则返回 `false`。

例如，考虑以下 HTML：

`<form> <fieldset> <legend> 选择一种交付方式 </legend> <label> <input type="radio" id="carrier-pigeon" name="delivery" value="pigeon" checked>信鸽 </label> <label> <input type="radio" id="pony-express" name="delivery" value="pony">小马快递 </label> <label> <input type="radio" id="snail-mail" name="delivery" value="postal">蜗牛邮件 </label> <label> <input type="radio" id="some-punk" name="delivery" value="bikecourier">骑车小子 </label> </fieldset> </form>`

如果你的代码需要知道哪个单选按钮在某个组中被选中，可以通过将 `:checked` 选择器应用于该组，然后获取返回对象的 `value` 属性来实现：

`const deliveryMethod = document.querySelector('input[name=delivery]:checked').value;` ### 设置单选按钮的状态

要将单选按钮字段设置为选中或未选中状态，可以将布尔表达式分配给 `checked` 属性：

`radio.checked = true|false`

例如，在上一节的 HTML 代码中，表单组的初始状态是第一个单选按钮被选中。你可以通过选择该按钮来重置组。你可以获取第一个单选按钮的 `id`，但是如果后来你改变了（或者别人改变了）单选按钮的顺序怎么办？一种更安全的方法是获取组中第一个单选按钮的引用，无论它是什么，然后选择该元素。以下是实现这一功能的代码：

`const firstRadioButton = document.querySelectorAll('input[name=delivery]')[0]; firstRadioButton.checked = true;`

这段代码使用 `querySelectorAll()` 返回 `delivery` 组中所有单选按钮的 `NodeList` 集合；然后使用 `[0]` 来引用集合中的第一个元素。接着将该元素的 `checked` 属性设置为 `true`。  ## 编程选择列表

选择列表是 HTML 表单中常见的控件，因为它们允许 Web 开发人员以紧凑的控件显示大量选项，大多数用户都知道如何操作。

要创建列表容器，您使用``<select>``标签：

``<select id="selectId" name="selectName" size="selectSize" [multiple]>``

这里是各个部分的说明：

+   `selectId`: 选择列表的唯一标识符。

+   `selectName`: 您想要分配给选择列表的名称。

+   `selectSize`: 选择列表框中可见的可选行数。如果您省略此值，浏览器将显示为下拉框。

+   ``multiple``: 当此可选属性存在时，用户可以在列表中选择多个选项。

对于列表中的每个项目，您在``<select>``和``</select>``标签之间添加一个``<option>``标签：

``<option value=`optionValue` [selected]>``

这里是各个部分的说明：

+   *``optionValue``*: 您想要分配给列表选项的值。

+   ``selected``: 当此可选属性存在时，列表选项最初被选中。

### 引用选择列表选项

如果您的代码需要处理选择列表中的所有选项，请使用选择列表对象的``options``属性：

``document.querySelector(`list`).options``

要处理列表中的特定选项，请使用 JavaScript 的方括号运算符（``[]``）来指定选项在列表中的索引位置：

``document.querySelector(`list`).options[`n`]``

这里是各个部分的说明：

+   *``list``*: 指定您要处理的``select``元素的选择器

+   *``n``*: 返回的``NodeList``集合中选项的索引（``0``是第一个选项，``1``是第二个选项，以此类推）

要获取选项的文本（即在列表中显示的文本），请使用选项对象的``text``属性：

``document.querySelector(`list`).options[2].text``  ### 获取选中的列表选项

如果您的代码需要知道选择列表中某个特定选项是选中还是未选中，请检查该选项的``selected``属性，如下所示：

``option.selected``

``selected``属性返回``true``如果选项被选中，或``false``如果选项未被选中。

例如，考虑以下选择列表：

``<select id="hair-color" name="hair-color"> <option value="black">Black</option> <option value="blonde">Blonde</option> <option value="brunette" selected>Brunette</option> <option value="red">Red</option> <option value="neon">Something neon</option> <option value="none">None</option> </select>``

您的代码可能想要知道选择列表中哪个选项被选中。您可以通过列表的``selectedOptions``属性来实现：

``const hairColor = document.querySelector('#hair-color').selectedOptions[0];``

这不是一个多选列表，因此指定``selectedOptions[0]``返回选中的``option``元素。在这个例子中，您的代码可以使用``hairColor.text``来获取所选选项的文本。

如果列表包括``multiple``属性，``selectedOptions``属性可能会返回一个``HTMLCollection``对象，包含多个元素。您的代码需要考虑这种可能性，例如，通过循环遍历集合：

HTML：

``<select id="hair-products" name="hair-products" size="5" multiple> <option value="gel" selected>Gel</option> <option value="grecian-formula" selected>Grecian Formula</option> <option value="mousse">Mousse</option> <option value="peroxide">Peroxide</option> <option value="shoe-black">Shoe black</option> </select>``

JavaScript:

`const selectedHairProducts = document.querySelector('#hair-products').selectedOptions; for (const hairProduct of selectedHairProducts) { console.log(hairProduct.text); }` ### 更改选中的选项

要将选择列表选项设置为选中或未选中状态，可以将一个布尔表达式赋值给选项对象的``selected``属性：

`option.selected = Boolean`

这里是各个部分的说明：

+   `option`: 引用您想要修改的`option`元素。

+   `Boolean`: 你要分配给选项的布尔值或表达式。使用 `true` 选择该选项；使用 `false` 取消选择该选项。

使用前一节的 HTML 代码，以下语句选择列表中的第三个选项：

`document.querySelector('#hair-products').options[2].selected = true;`

你可以通过取消选择所有选项来重置列表。方法是将选择列表对象的 `selectedIndex` 属性设置为 `-1`：

`document.querySelector('#hair-products').selectedIndex = -1` ## 处理表单事件

随着点击、输入、切换和拖动的发生，网页表单成了真正的事件工厂。幸运的是，你可以忽略大多数事件，但有些事件确实很有用，不仅能在事件发生时运行代码，还能触发这些事件。

大多数表单事件是点击事件，因此你可以通过使用 JavaScript 的 `addEventListener()` 方法设置 `click` 事件处理程序（我将在[第六章](c06.xhtml)中介绍）。以下是一个例子：

HTML:

`<form> <label for="user">用户名：</label> <input id="user" type="text" name="username"> <label for="pwd">密码：</label> <input id="pwd" type="password" name="password"> </form>`

JavaScript:

`document.querySelector('form').addEventListener('click', () => { console.log('感谢点击表单！'); });`

这个例子监听整个 `form` 元素上的点击事件，但你也可以为按钮、`input` 元素、复选框、单选按钮等创建 `click` 事件处理程序。

### 设置焦点

一个简单的功能，可以改善表单页面上的用户体验，那就是在页面加载时将焦点设置到第一个表单字段。设置焦点可以避免用户在第一个字段内进行烦人的点击操作。

要实现这一点，运行 JavaScript 的 `focus()` 方法来设置元素在启动时获得焦点：

`field.focus()`

以下是一个例子，它在启动时将焦点设置到 `id` 等于 `user` 的文本字段：

HTML:

`<form> <label for="user">用户名：</label> <input id="user" type="text" name="username"> <label for="pwd">密码：</label> <input id="pwd" type="password" name="password"> </form>`

JavaScript:

`document.querySelector('#user').focus();` ### 监控焦点事件

与其设置焦点，你可能更希望监控某个字段何时获得焦点（例如，用户点击或切换到该字段时）。你可以通过在该字段上设置`focus`事件处理程序来监控这一过程：

`*field*.addEventListener('focus', () => { *焦点代码在这里* });`

这里有一个例子：

`document.querySelector('#user').addEventListener('focus', () => { console.log('用户名字段已获得焦点！'); });` ### 监控失去焦点事件

将焦点设置到元素的反面是*失去焦点*，这会移除元素的焦点。你可以通过在元素上运行`blur()`方法来失去元素的焦点：

`*field*.blur()`

然而，与其让一个元素失去焦点，你更可能想在特定元素失去焦点时运行一些代码（例如，用户点击或切换出该字段时）。你可以通过设置`blur()`事件处理程序来监控特定的失去焦点元素：

`*field*.addEventListener('blur', () => { *失去焦点代码在这里* });`

这里有一个例子：

`document.querySelector('#user').addEventListener('blur', () => { console.log('用户名字段已失去焦点！'); });` ### 监听元素变化

最有用的表单事件之一是`change`事件，当字段的值或状态以某种方式被修改时，该事件会触发。此事件何时触发取决于元素类型：

+   对于`textarea`元素和各种文本相关的`input`元素，当元素失去焦点时，`change`事件会触发。

+   对于复选框、单选按钮、选择列表和选择器，当用户点击要修改选择或值的元素时，`change`事件会立即触发。

你通过设置`change()`事件处理程序来监听字段的`change`事件：

`*field*.addEventListener('change', () => { *Change code goes here* });`

这里有一个例子：

HTML:

`<label for="bgcolor">选择一个背景颜色</label> <input id="bgcolor" type="color" name="bg-color" value="#ffffff">`

JavaScript:

`document.querySelector('#bgcolor').addEventListener('change', (event) => { const backgroundColor = event.target.value; document.body.bgColor = backgroundColor; });`

HTML代码设置了一个颜色选择器。JavaScript代码将`change`事件处理程序应用于颜色选择器。当颜色选择器上的`change`事件触发时，代码通过引用`event.target.value`将新颜色值存储在`backgroundColor`变量中，其中`event.target`指的是绑定事件监听器的元素（在这种情况下是颜色选择器）。然后代码将该颜色应用于`body`元素的`bgColor`属性。 ## 处理表单数据

有一个表单事件我之前没有提到，那就是一个重要的事件：`submit`事件，它在表单数据要发送到服务器时触发。

然而，如果你的脚本仅在本地处理表单数据——也就是说，你从不将数据发送到服务器——那么你就不需要烦恼提交表单。相反，更简单的方法是给表单添加一个按钮，然后使用该按钮的`click`事件处理程序以所需的方式处理表单数据。

这里有一个例子：

HTML:

`<form> <fieldset> <legend> 设置 </legend> <label for="background-color">选择一个背景颜色</label> <input id="background-color" type="color" name="bg-color" value="#ffffff"> <label for="text-color">选择一个文本颜色</label> <input id="text-color" type="color" name="text-color" value="#000000"> <label for="font-stack">选择一个字体：</label> <select id="font-stack" name="font-stack"> <option value="Georgia, 'Times New Roman', serif" selected>Serif</option> <option value="Verdana, Tahoma, sans-serif">Sans-serif</option> <option value="'Bradley Hand', Brush Script MT, cursive">Cursive</option> <option value="Luminari">Fantasy</option> <option value="Monaco, Courier, monospace">Monospace</option> </select> <button> 保存设置 </button> </fieldset> </form>`

`JavaScript:`

`// 监听 #background-color 颜色选择器的变化 document.querySelector('#background-color').addEventListener('change', function() { const backgroundColor = this.value; document.body.style.backgroundColor = backgroundColor; }); // 监听 #text-color 颜色选择器的变化 document.querySelector('#text-color').addEventListener('change', function() { const textColor = this.value; document.body.style.color = textColor; }); // 监听 #font-stack 下拉列表的变化 document.querySelector('#font-stack').addEventListener('change', function() { const fontStack = this.selectedOptions[0].value; document.body.style.fontFamily = fontStack; }); // 监听按钮点击事件 document.querySelector('button').addEventListener('click', () => { // 将表单数据存储在 JavaScript 对象中 const userSettings = { backgroundColor: document.querySelector('#background-color').value, textColor: document.querySelector('#text-color').value, fontStack: document.querySelector('#font-stack').selectedOptions[0].value } // 将设置保存到本地存储 localStorage.setItem('user-settings', JSON.stringify(userSettings)); });`

`HTML 设置了一个表单（请查看[图 10-2](#c10-fig-0002)）来收集一些用户设置——背景颜色、文本颜色和字体样式——以及一个按钮。JavaScript 为两个颜色选择器和下拉列表设置了变化事件处理程序。最后，代码监听按钮的点击事件，处理程序将表单数据存储在一个 JavaScript 对象中，然后将数据保存到本地存储。`

![用于收集页面用户设置的表单快照。设置字段包括选择背景颜色、选择文本颜色和选择字体。](images/9781394263219-fg1002.png)

[图 10-2:](#rc10-fig-0002) 用于收集页面用户设置的表单。
