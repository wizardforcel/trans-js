## 平均摄氏读数

这是另一个涉及平均值的例子。假设我们正在构建天气预报软件。为了确定一个城市的温度，我们从城市各地的多个温度计获取温度读数，并计算这些温度的平均值。

我们还想同时以华氏度和摄氏度显示温度，但我们的读数最初仅以华氏度提供给我们。

为了获得平均摄氏温度，我们的算法做了两件事：首先，它将所有读数从华氏度转换为摄氏度。然后，它计算所有摄氏数字的平均值。

以下是实现这一目标的一些代码。它的Big O是什么？

| ​  | `function` averageCelsius(fahrenheitReadings) { |
| --- | --- |
| ​  | `if` (fahrenheitReadings.length === 0) { `return` `null`; } |
| ​  |  |
| ​  | `const` celsiusNumbers = []; |
| ​  |  |
| ​  | `// 将每个读数转换为摄氏度并附加到数组中:` |
| ​  | `for` (`const` fahrenheitReading `of` fahrenheitReadings) { |
| ​  | `const` celsiusConversion = (fahrenheitReading - 32) / 1.8; |
| ​  | `celsiusNumbers.push(celsiusConversion);` |
| ​  | } |
| ​  |  |
| ​  | `// 计算平均值:` |
| ​  | `let` sum = 0; |
| ​  |  |
| ​  | `for` (`const` celsiusNumber `of` celsiusNumbers) { |
| ​  | `sum += celsiusNumber;` |
| ​  | } |
| ​  |  |
| ​  | `return` Math.floor(sum / celsiusNumbers.length); |
| ​  | } |

首先，我们可以说N是传递给我们方法的fahrenheitReadings的数量。

在方法内部，我们运行两个循环。第一个将读数转换为摄氏度，第二个对所有摄氏数字进行求和。由于我们有两个循环，每个循环都迭代所有N个元素，我们得到了N + N，即2N（再加上一些常数步骤）。因为Big O符号忽略常数，所以这被简化为O(N)。

不要被之前的单词构建示例中的两个循环导致的O(N²)效率所困扰。在那里，循环是嵌套的，这导致N步乘以N步。然而，在我们的案例中，我们只是简单地有两个循环，一个接一个。这是N步加N步（2N），这只是O(N)。
