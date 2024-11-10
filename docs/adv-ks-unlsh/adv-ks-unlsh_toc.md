## `目录`

1.  [`什么是 JavaScript`](chap00.xhtml#leanpub-auto-what-is-javascript)

    1.  [`课程概述`](chap00.xhtml#leanpub-auto-course-overview)

    1.  [`先决条件`](chap00.xhtml#leanpub-auto-prerequisites)

    1.  [`运行代码示例`](chap00.xhtml#leanpub-auto-running-code-examples)

    1.  [`这门课程适合谁？`](chap00.xhtml#leanpub-auto-who-is-this-course-for)

    1.  [`JavaScript 的历史`](chap00.xhtml#leanpub-auto-history-of-javascript)

    1.  [`JavaScript 语言的标准化`](chap00.xhtml#leanpub-auto-standardization-of-the-javascript-language)

    1.  [`Ecma 国际组织，TC39`](chap00.xhtml#leanpub-auto-ecma-international-tc39)

    1.  [`提案流程`](chap00.xhtml#leanpub-auto-proposals-process)

    1.  [`跟踪即将推出的特性`](chap00.xhtml#leanpub-auto-track-upcoming-features)

    1.  [`ECMAScript 如何版本控制？`](chap00.xhtml#leanpub-auto-how-is-ecmascript-versioned)

    1.  [`即时编译器`](chap00.xhtml#leanpub-auto-jit-compiler)

    1.  [`JavaScript 引擎`](chap00.xhtml#leanpub-auto-javascript-engine)

    1.  [`执行上下文的类型`](chap00.xhtml#leanpub-auto-types-of-execution-contexts)

    1.  [`执行上下文阶段`](chap00.xhtml#leanpub-auto-execution-context-phases)

    1.  [`堆栈溢出`](chap00.xhtml#leanpub-auto-stack-overflow)

    1.  [`自动垃圾回收`](chap00.xhtml#leanpub-auto-automatic-garbage-collection)

1.  [`提升`](chap01.xhtml#leanpub-auto-hoisting)

    1.  [`“var” 声明`](chap01.xhtml#leanpub-auto-var-declarations)

    1.  [`函数声明`](chap01.xhtml#leanpub-auto-function-declarations)

    1.  [`块内的函数声明`](chap01.xhtml#leanpub-auto-function-declarations-inside-blocks)

    1.  [`类声明`](chap01.xhtml#leanpub-auto-class-declarations)

    1.  [`时间死区 (TDZ)`](chap01.xhtml#leanpub-auto-temporal-dead-zone-tdz)

    1.  [`函数和类表达式`](chap01.xhtml#leanpub-auto-function-and-class-expressions)

    1.  [`关于提升的常见误解`](chap01.xhtml#leanpub-auto-common-misconception-about-hoisting)

1.  [`作用域`](chap02.xhtml#leanpub-auto-scope)

    1.  [`词法作用域`](chap02.xhtml#leanpub-auto-lexical-scope)

    1.  [`避免污染全局作用域`](chap02.xhtml#leanpub-auto-avoid-polluting-the-global-scope)

    1.  [`隐式全局变量`](chap02.xhtml#leanpub-auto-implicit-globals)

    1.  [`遮蔽声明`](chap02.xhtml#leanpub-auto-shadowing-declarations)

    1.  [`函数参数作用域`](chap02.xhtml#leanpub-auto-function-parameter-scope)

    1.  [`函数表达式名称作用域`](chap02.xhtml#leanpub-auto-function-expression-name-scope)

    1.  [`块作用域`](chap02.xhtml#leanpub-auto-block-scope)

    1.  [`模块作用域`](chap02.xhtml#leanpub-auto-module-scope)

    1.  [`作用域链`](chap02.xhtml#leanpub-auto-scope-chain)

1.  [`强制转换`](chap03.xhtml#leanpub-auto-coercion)

    1.  [`转为原始值`](chap03.xhtml#leanpub-auto-toprimitive)

    1.  [`转为数字`](chap03.xhtml#leanpub-auto-tonumber)

    1.  [`转为字符串`](chap03.xhtml#leanpub-auto-tostring)

    1.  [`转为布尔值`](chap03.xhtml#leanpub-auto-toboolean)

    1.  [`抽象相等运算符的总结`](chap03.xhtml#leanpub-auto-summary-of-abstract-equality-operator)

    1.  [`加法运算符`](chap03.xhtml#leanpub-auto-addition-operator)

    1.  [`关系运算符`](chap03.xhtml#leanpub-auto-relational-operators)

1.  [`闭包`](chap04.xhtml#leanpub-auto-closures)

    1.  [`什么是闭包？`](chap04.xhtml#leanpub-auto-what-is-a-closure)

    1.  [`闭包是如何工作的？`](chap04.xhtml#leanpub-auto-how-do-closures-work)

    1.  [`不同作用域是如何链接的？`](chap04.xhtml#leanpub-auto-how-are-different-scopes-linked)

    1.  [`是什么导致了这个问题？`](chap04.xhtml#leanpub-auto-what-causes-this-problem)

    1.  [`如何解决这个问题？`](chap04.xhtml#leanpub-auto-how-to-resolve-this-problem)

1.  [`原型`](chap05.xhtml#leanpub-auto-prototypes)

    1.  [`对象是如何链接的？`](chap05.xhtml#leanpub-auto-how-are-objects-linked)

    1.  [`“prototype”属性`](chap05.xhtml#leanpub-auto-the-prototype-property)

    1.  [`获取任何对象的原型`](chap05.xhtml#leanpub-auto-getting-prototype-of-any-object)

    1.  [`Object.prototype - 所有对象的父类`](chap05.xhtml#leanpub-auto-objectprototype---parent-of-all-objects)

    1.  [`“Function” 函数`](chap05.xhtml#leanpub-auto-function-function)

    1.  [`__proto__ 的问题`](chap05.xhtml#leanpub-auto-problems-with-proto)

    1.  [`Object.create 方法`](chap05.xhtml#leanpub-auto-objectcreate-method)

    1.  [`空原型对象`](chap05.xhtml#leanpub-auto-null-prototype-object)

    1.  [`ES2015 类`](chap05.xhtml#leanpub-auto-es2015-classes)

1.  [`‘this’ 关键字`](chap06.xhtml#leanpub-auto-this-keyword)

    1.  [`函数上下文`](chap06.xhtml#leanpub-auto-function-context)

    1.  [`全局上下文`](chap06.xhtml#leanpub-auto-global-context)

    1.  [`构造函数上下文`](chap06.xhtml#leanpub-auto-constructor-function-context)

    1.  [`类上下文`](chap06.xhtml#leanpub-auto-class-context)

    1.  [`DOM 事件处理程序上下文`](chap06.xhtml#leanpub-auto-dom-event-handler-context)

    1.  [`箭头函数来救场`](chap06.xhtml#leanpub-auto-arrow-functions-to-the-rescue)

    1.  [`借用方法`](chap06.xhtml#leanpub-auto-borrowing-methods)

    1.  [`链式构造函数调用`](chap06.xhtml#leanpub-auto-chain-constructor-calls)

    1.  [`重新审视“this”问题`](chap06.xhtml#leanpub-auto-revisit-this-problem)

    1.  [`“this” vs globalThis`](chap06.xhtml#leanpub-auto-this-vs-globalthis)

1.  [`符号`](chap07.xhtml#leanpub-auto-symbol)

    1.  [`符号与隐私`](chap07.xhtml#leanpub-auto-symbols-and-privacy)

    1.  [`为符号添加描述`](chap07.xhtml#leanpub-auto-adding-a-description-to-symbols)

    1.  [`Symbol.toPrimitive`](chap07.xhtml#leanpub-auto-symboltoprimitive)

    1.  [`Symbol.toStringTag`](chap07.xhtml#leanpub-auto-symboltostringtag)

    1.  [`Symbol.isConcatSpreadable`](chap07.xhtml#leanpub-auto-symbolisconcatspreadable)

1.  [`异步 JavaScript`](chap08.xhtml#leanpub-auto-asynchronous-javascript)

    1.  [`异步是什么意思？`](chap08.xhtml#leanpub-auto-what-does-asynchronous-mean)

    1.  [`异步 JavaScript`](chap08.xhtml#leanpub-auto-asynchronous-javascript-1)

    1.  [`回调函数的问题`](chap08.xhtml#leanpub-auto-problems-with-callbacks)

    1.  [`什么是事件循环？`](chap08.xhtml#leanpub-auto-what-is-an-event-loop)

    1.  [`Promise状态`](chap08.xhtml#leanpub-auto-promise-states)

    1.  [`Promise实例方法`](chap08.xhtml#leanpub-auto-promise-instance-methods)

    1.  [`创建Promise`](chap08.xhtml#leanpub-auto-creating-promises)

    1.  [`在回调基础的API中使用Promise`](chap08.xhtml#leanpub-auto-using-promises-with-callback-based-api)

    1.  [`Promise规范`](chap08.xhtml#leanpub-auto-promise-specification)

    1.  [`Promise与thenable`](chap08.xhtml#leanpub-auto-promise-vs-thenable)

    1.  [`then Promise`](chap08.xhtml#leanpub-auto-then-promise)

    1.  [`catch Promise`](chap08.xhtml#leanpub-auto-catch-promise)

    1.  [`finally Promise`](chap08.xhtml#leanpub-auto-finally-promise)

    1.  [`理解Promise链`](chap08.xhtml#leanpub-auto-making-sense-of-promise-chaining)

    1.  [`then与catch中的拒绝处理器`](chap08.xhtml#leanpub-auto-rejection-handler-in-then-vs-catch)

    1.  [`并发请求`](chap08.xhtml#leanpub-auto-concurrent-requests)

    1.  [`请求超时`](chap08.xhtml#leanpub-auto-request-timeout)

    1.  [`异步函数`](chap08.xhtml#leanpub-auto-async-functions)

    1.  [`await关键字`](chap08.xhtml#leanpub-auto-await-keyword)

    1.  [`多个await表达式`](chap08.xhtml#leanpub-auto-multiple-await-expressions)

    1.  [`错误处理`](chap08.xhtml#leanpub-auto-error-handling-1)

    1.  [`返回与等待Promise`](chap08.xhtml#leanpub-auto-returning-vs-awaiting-promise)

    1.  [`等待非Promise值`](chap08.xhtml#leanpub-auto-awaiting-non-promise-value)

    1.  [`不必要使用Promise构造函数`](chap08.xhtml#leanpub-auto-unnecessary-use-of-the-promise-constructor)

    1.  [`错误处理不当`](chap08.xhtml#leanpub-auto-incorrect-error-handling)

    1.  [`将Promise拒绝转换为实现`](chap08.xhtml#leanpub-auto-converting-promise-rejection-into-fulfillment)

    1.  [`异步执行器函数`](chap08.xhtml#leanpub-auto-async-executor-function)

1.  [`迭代器与生成器`](chap09.xhtml#leanpub-auto-iterators-and-generators)

    1.  [`可迭代对象`](chap09.xhtml#leanpub-auto-iterables)

    1.  [`迭代器`](chap09.xhtml#leanpub-auto-iterators)

    1.  [`迭代器原型`](chap09.xhtml#leanpub-auto-iterator-prototype)

    1.  [`创建自定义可迭代对象`](chap09.xhtml#leanpub-auto-making-custom-iterable-objects)

    1.  [`无限序列`](chap09.xhtml#leanpub-auto-infinite-sequence)

    1.  [`实现迭代器`](chap09.xhtml#leanpub-auto-implementing-iterators)

    1.  [`消费值`](chap09.xhtml#leanpub-auto-consuming-values)

    1.  [`委托给其他迭代器`](chap09.xhtml#leanpub-auto-delegating-to-other-iterators)

    1.  [`进一步阅读`](chap09.xhtml#leanpub-auto-further-reading-11)

    1.  [`for await…of循环`](chap09.xhtml#leanpub-auto-for-awaitof-loop)

1.  [`调试JavaScript`](chap10.xhtml#leanpub-auto-debugging-javascript)

1.  [`总结`](chap11.xhtml#leanpub-auto-wrap-up)

## `指南`

1.  [`开始阅读`](chap00.xhtml)
