## 队列在实际应用中

队列在许多应用中很常见，从打印作业到Web应用中的后台工作程序。 

假设我们正在为打印机编程一个简单的JavaScript接口，该打印机可以接受来自网络上各种计算机的打印作业。我们希望确保按接收顺序打印每个文档。

这段代码使用了我们之前实现的队列类：

| ​  | `import` Queue `from` `('./queue.js')`; |
| --- | --- |
| ​  |  |
| ​  | `class` PrintManager { |
| ​  | `constructor`() { |
| ​  | `this`.queue = `new` Queue(); |
| ​  | `}` |
| ​  |  |
| ​  | `queuePrintJob(document) {` |
| ​  | `this`.queue.enqueue(document); |
| ​  | `}` |
| ​  |  |
| ​  | `run() {` |
| ​  | `while` (`this`.queue.read()) { |
| ​  | `this`.printDocument(`this`.queue.dequeue()); |
| ​  | `}` |
| ​  | `}` |
| ​  |  |
| ​  | `printDocument(document) {` |
| ​  | `// 这里是运行实际打印机的代码。` |
| ​  | `// 为了演示，我们将打印到终端：` |
| ​  | `console.log(document);` |
| ​  | `}` |
| ​  | `}` |

然后我们可以像下面这样使用这个类：

| ​  | `const` printManager = `new` PrintManager(); |
| --- | --- |
| ​  | printManager.queuePrintJob(`'第一个文档'`); |
| ​  | printManager.queuePrintJob(`'第二个文档'`); |
| ​  | printManager.queuePrintJob(`'第三个文档'`); |
| ​  | printManager.run(); |

每次调用 `queuePrintJob` 时，我们将文档（在此示例中由字符串表示）添加到队列中：

| ​  | `queuePrintJob(document) {` |
| --- | --- |
| ​  | `this`.queue.enqueue(document); |
| ​  | `}` |

当我们调用 `run` 时，我们通过按接收顺序处理每个文档来“打印”它。也就是说，我们从队列中出队每个文档并打印它：

| ​  | `run() {` |
| --- | --- |
| ​  | `while` (`this`.queue.read()) { |
| ​  | `this`.printDocument(`this`.queue.dequeue()); |
| ​  | `}` |
| ​  | `}` |

当我们运行之前的代码时，程序将按照接收的顺序输出三个文档：

| ​  | 第一个文档 |
| --- | --- |
| ​  | 第二个文档 |
| ​  | 第三个文档 |

尽管这个示例简化了某些细节，真实的打印系统可能会遇到这些细节，但在此类应用中，队列的基本使用是非常真实的，构建该系统的基础。

队列也是处理异步请求的完美工具——它们确保请求按接收顺序处理。它们通常用于模拟现实世界的场景，其中事件需要按照特定顺序发生，例如飞机等待起飞和病人等待看医生。
