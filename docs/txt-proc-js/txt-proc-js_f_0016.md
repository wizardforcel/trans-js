| 配方 6 | 向十六进制颜色添加透明度 |
| --- | --- |

### 任务

假设你想为应用中的某些元素添加半透明的叠加层。例如，你可能会有一个提示，要求读者在继续之前先登录，你可能希望在提示周围加入半透明的白色，使页面的其余部分模糊。

如果你使用普通的十六进制颜色，叠加层将完全遮挡其下方的内容。如果你使用 CSS 的透明度，它将设置整个元素的透明度，包括其内容。

你需要一个解决方案，允许你向十六进制颜色添加透明度。

### 解决方案

编写一个函数，该函数接受一个十六进制值和一个百分比作为输入参数。该函数应该将百分比转换为十六进制值，然后将其添加到原始的十六进制值中：

[part_1/adding_transparency_to_hex/adding_transparency_to_hex_ex1.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/adding_transparency_to_hex/adding_transparency_to_hex_ex1.js)

|   | **函数** addAlphaToHex(hex, percent) { |
| --- | --- |
|   | **const** decimal = percent / 100; |
|   | **const** rgb = Math.round(decimal * 255); |
|   | **const** alpha = rgb.toString(16).toUpperCase(); |
|   |  |
|   | **if** (alpha.length === 1) { |
|   | alpha = *"0"* + alpha; |
|   | } |
|   |  |
|   | **return** hex + alpha; |
|   | } |
|   |  |
|   | addAlphaToHex(*"#FFFFFF"*, 70); *// → "#FFFFFFB3"* |

该函数返回一个包含透明度级别的八字符十六进制值。在此情况下，返回值是具有 70% 透明度的白色十六进制颜色（#FFFFFFB3）。

### 讨论

以前，开发者必须将十六进制颜色值转换为 RGBA 或 HSLA 颜色值以设置透明度。这个转换是必要的，因为 RGBA 或 HSLA 值中的 alpha 通道可以用来确定透明度的级别。然而，随着 CSS 色彩模块第 4 级的引入，问题已经得到解决，通过新增包含 alpha 值的四位（#rgba）和八位（#rrggbbaa）十六进制表示法。因此，开发者不再需要将十六进制颜色转换为其他格式以设置透明度。

该表示法中的 rr、gg、bb 和 aa 分别代表红色、绿色、蓝色和 alpha 组件的十六进制值，范围从 00 到 FF。alpha 值决定了颜色的透明度，其中 00 代表完全透明的颜色，FF 代表完全不透明的颜色。例如，颜色 #FF0000FF 是完全不透明的红色，而颜色 #FF000000 是完全透明的红色。

我们的函数 `addAlphaToHex()` 接受两个参数：hex 和 percent。该函数的目的是将百分比值转换为相应的十六进制表示，并将其作为 alpha 值附加到给定的十六进制颜色上。在函数内部，我们首先通过将百分比除以 100 来计算百分比的十进制值。然后，我们将结果乘以 255，并使用 `Math.round()` 函数四舍五入结果，以获得一个 RGB 值。

接下来，我们使用 `toString()` 方法将 RGB 值转换为十六进制字符串，并使用基数 16（即，16进制）。然后，我们使用 `toUpperCase()` 方法将字符串转换为大写字母。之后，我们检查十六进制值是否只有一个字符长。如果是，我们通过字符串拼接运算符（+）添加一个前导零，使其长度为两个字符。最后，我们返回原始的值参数并与 alpha 十六进制值拼接在一起。

如果你希望尽可能紧凑地编写 JavaScript 代码，可以使用以下版本：

[part_1/adding_transparency_to_hex/adding_transparency_to_hex_ex2.js](http://media.pragprog.com/titles/fkjavascript/code/part_1/adding_transparency_to_hex/adding_transparency_to_hex_ex2.js)

|   | **function** addAlphaToHex(hex, percent) { |
| --- | --- |
|   | **const** alpha = Math.round(percent / 100 * 255).toString(16) |
|   | .toUpperCase().padStart(2, *"0"*); |
|   | **return** hex + alpha; |
|   | } |
|   |  |
|   | addAlphaToHex(*"#FFFFFF"*, 70); *// → "#FFFFFFB3"* |

这个版本将 rgb 和 alpha 常量合并为一行，并使用 padStart() 在必要时添加前导零。padStart() 的第一个参数定义了给定字符串在填充后结果字符串的长度，因此 padStart(2, "0") 确保十六进制字符串始终为两位数。

如果你想以不同的格式查看颜色，可以使用 Chrome/Edge 开发者工具。打开开发者工具面板并导航到样式部分，找到你想查看的颜色。然后，点击颜色左侧的框，直接调整其值：

![images/src/adding_transparency_to_hex/hex.png](images/src/adding_transparency_to_hex/hex.png)

你还可以按住 Shift 键并点击框，切换不同的格式选项，值会自动转换。
