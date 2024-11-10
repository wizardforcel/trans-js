## 练习

以下练习为您提供了分析算法的机会。这些练习的解决方案可以在章节 [*第 5 章*](f_0210.xhtml#optimizing.code.with.and.without.big.o.solutions) 中找到。

1.  使用大 O 符号来描述一个算法的时间复杂度，该算法需要 4N + 16 步。

1.  使用大 O 符号来描述一个算法的时间复杂度，该算法需要 2N²。

1.  使用大 O 符号来描述以下函数的时间复杂度，该函数返回在数字被加倍后数组中所有数字的总和：

    | ​  | `function` `doubleThenSum(array) {` |
    | --- | --- |
    | ​  | `const` `doubledArray = [];` |
    | ​  |  |
    | ​  | `for` ( `const` `number` `of` `array`) { |
    | ​  | `doubledArray.push(number * 2);` |
    | ​  | `}` |
    | ​  |  |
    | ​  | `let` `sum = 0;` |
    | ​  |  |
    | ​  | `for` ( `const` `number` `of` `doubledArray) {` |
    | ​  | `sum += number;` |
    | ​  | `}` |
    | ​  |  |
    | ​  | `return` `sum;` |
    | ​  | `}` |

1.  使用大 O 符号来描述以下函数的时间复杂度，该函数接受一个字符串数组并以多种形式打印每个字符串：

    | ​  | `function` `multipleCases(array) {` |
    | --- | --- |
    | ​  | `for` ( `const` `string` `of` `array`) { |
    | ​  | `console.log(string.toUpperCase());` |
    | ​  | `console.log(string.toLowerCase());` |
    | ​  | `// 首字母大写:` |
    | ​  | `console.log(string[0].toUpperCase() + string.slice(1));` |
    | ​  | `}` |
    | ​  | `}` |

1.  下一个函数遍历一个数字数组。在此过程中，它关注每个其他数字，同时忽略中间的数字。对于每个“关注数字”，函数继续逐一打印出数组中的每个数字，前提是将其与关注数字相加。

    这个函数的效率在大 O 符号方面是什么？

    | ​  | `function` `everyOther(array) {` |
    | --- | --- |
    | ​  | `for` ( `const` `[index, number]` `of` `array.entries()) {` |
    | ​  | `if` (index % 2 === 0) { |
    | ​  | `for` ( `const` `otherNumber` `of` `array`) { |
    | ​  | `console.log(number + otherNumber);` |
    | ​  | `}` |
    | ​  | `}` |
    | ​  | `}` |
    | ​  | `}` |

版权所有 © 2024, The Pragmatic Bookshelf。
