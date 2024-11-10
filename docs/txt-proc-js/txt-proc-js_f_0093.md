## matchAll()

matchAll() 方法与 match() 类似，但当你设置全局标志 (g) 时，它会提供额外的关于匹配的信息，例如捕获组和索引位置：

[appendix/methods/methods_ex6.js](http://media.pragprog.com/titles/fkjavascript/code/appendix/methods/methods_ex6.js)

|   | **const** str = *"9英尺, 10英尺, 11英尺"*; |
| --- | --- |
|   | **const** re = */**(\d\d)**英尺/g*; |
|   |  |
|   | console.log(str.match(re)); |
|   | *// → ["10英尺", "11英尺"]* |
|   |  |
|   | console.log(...str.matchAll(re)); |
|   | *// → ["10英尺", "10", index: 5, input: "9英尺, 10英尺, 11英尺", groups: undefined]* |
|   | *// → ["11英尺", "11", index: 11, input: "9英尺, 10英尺, 11英尺", groups: undefined]* |
|   |  |
|   | console.log(re.exec(str)); |
|   | *// → ["10英尺", "10", index: 5, input: "9英尺, 10英尺, 11英尺", groups: undefined]* |

matchAll() 是 ECMAScript 中相对较新的方法，和本附录中介绍的其他方法相比，Edge 79（发布于2020-01-15）是最后一个实现 matchAll() 的浏览器。^([[39]](f_0098.xhtml#FOOTNOTE-39)) 如果你需要支持旧版本的浏览器，可以使用 Polyfill。^([[40]](f_0098.xhtml#FOOTNOTE-40)) 以前，开发者需要在循环中调用 exec() 来获取类似的结果，但效率较低。以下是一个可能在互联网上遇到的示例： 

[appendix/methods/methods_ex7.js](http://media.pragprog.com/titles/fkjavascript/code/appendix/methods/methods_ex7.js)

|   | **const** str = *"9英尺, 10英尺, 11英尺"*; |
| --- | --- |
|   | **const** re = */**(\d\d)**英尺/g*; |
|   |  |
|   | **let** matches; |
|   |  |
|   | **while** ((matches = re.exec(str)) !== **null**) { |
|   | console.log(matches); |
|   | } |
|   |  |
|   | *// 日志:* |
|   | *// → ["10英尺", "10", index: 5, input: "9英尺, 10英尺, 11英尺", groups: undefined]* |
|   | *// → ["11英尺", "11", index: 11, input: "9英尺, 10英尺, 11英尺", groups: undefined]* |
