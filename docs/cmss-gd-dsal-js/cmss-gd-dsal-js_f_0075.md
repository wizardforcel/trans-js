## `练习`

`以下练习为你提供了在实际情况下练习算法的机会。这些练习的解决方案在[第7章](f_0212.xhtml#big.o.in.everyday.code.solutions)中找到。`

1.  `使用大 O 表示法描述以下函数的时间复杂度。如果数组是一个100和数组，则返回真；如果不是，则返回假。`

    `一个100和数组满足以下条件：`

    +   `它的第一个和最后一个数字相加为100。`

    +   `它的第二个和倒数第二个数字相加为100。`

    +   `它的第三个和倒数第三个数字相加为100，依此类推。`

    `这里是函数：`

    |  | `function oneHundredSum(array) {` |
    | --- | --- |
    |  | `if (array.length % 2 !== 0 | | array.length === 0) {` |
    |  | `return false;` |
    |  | `}` |
    |  |  |
    |  | `let leftIndex = 0;` |
    |  | `let rightIndex = array.length - 1;` |
    |  |  |
    |  | `while (leftIndex < Math.floor(array.length / 2)) {` |
    |  | `if (array[leftIndex] + array[rightIndex] !== 100) {` |
    |  | `return false;` |
    |  | `}` |
    |  |  |
    |  |  |
    |  |  |
    |  |  |
    |  | `leftIndex += 1;` |
    |  | `rightIndex -= 1;` |
    |  | `}` |
    |  | `return true;` |
    |  | `}` |

1.  `使用大 O 表示法描述以下函数的时间复杂度。它合并两个已排序的数组，以创建一个包含两个数组中所有值的新排序数组：`

    |  | `function merge(array1, array2) {` |
    | --- | --- |
    |  | `const newArray = [];` |
    |  | `let array1Pointer = 0;` |
    |  | `let array2Pointer = 0;` |
    |  |  |
    |  | `// 运行循环直到我们到达两个数组的末尾：` |
    |  | `while (array1Pointer < array1.length | | array2Pointer < array2.length) {` |
    |  | `// 如果我们已经到达第一个数组的末尾，` |
    |  | `// 从第二个数组添加项：` |
    |  | `if (array1Pointer >= array1.length) {` |
    |  | `newArray.push(array2[array2Pointer]);` |
    |  | `array2Pointer += 1;` |
    |  | `// 如果我们已经到达第二个数组的末尾，` |
    |  | `// 从第一个数组添加项：` |
    |  | `} else if (array2Pointer >= array2.length) {` |
    |  | `newArray.push(array1[array1Pointer]);` |
    |  | `array1Pointer += 1;` |
    |  | `// 如果第一个数组中的当前数字小于当前` |
    |  | `// 第二个数组中的数字，从第一个数组添加：` |
    |  | `}` else if (array1[array1Pointer] < array2[array2Pointer]) { |
    |  | `newArray.push(array1[array1Pointer]);` |
    |  | `array1Pointer += 1;` |
    |  | `// 如果第二个数组中的当前数字小于或等于` |
    |  | `// 对于第一个数组中的当前数字，从第二个数组添加：` |
    |  | `} else {` |
    |  | `newArray.push(array2[array2Pointer]);` |
    |  | `array2Pointer += 1;` |
    |  | `}` |
    |  | `}` |
    |  |  |
    |  | `return newArray;` |
    |  | `}` |

1.  使用大 O 表示法描述以下函数的时间复杂度。该函数解决了一个著名的问题，称为“在干草堆中寻找针”。

    针和干草堆都是字符串。例如，如果针是"def"而干草堆是"abcdefghi"，则针被包含在干草堆中，因为"def"是"abcdefghi"的子串。然而，如果针是"dd"，它不能在"abcdefghi"的干草堆中找到。

    该函数根据针是否可以在干草堆中找到返回真或假：

    | ​  | `function findNeedle(needle, haystack) {` |
    | --- | --- |
    | ​  | `let needleStartIndex = 0;` |
    | ​  |  |
    | ​  | `while (needleStartIndex <= haystack.length - needle.length) {` |
    | ​  | `if` (needle[0] === haystack[needleStartIndex]) { |
    | ​  | `let` needleOffset = 0; |
    | ​  |  |
    | ​  | `while` (needleOffset < needle.length) { |
    | ​  | `if` (needle[needleOffset] !== |
    | ​  | haystack[needleStartIndex + needleOffset]) { |
    | ​  | `break`; |
    | ​  | } |
    | ​  |  |
    | ​  | `if` (needleOffset === needle.length - 1) { |
    | ​  | `return` `true`; |
    | ​  | } |
    | ​  |  |
    | ​  | needleOffset += 1; |
    | ​  | } |
    | ​  | } |
    | ​  |  |
    | ​  | needleStartIndex += 1; |
    | ​  | } |
    | ​  |  |
    | ​  | `return` `false`; |
    | ​  | } |

1.  使用大 O 表示法描述以下函数的时间复杂度。该函数查找给定数组中三个数字的最大乘积：

    | ​  | `function` largestProduct(array) { |
    | --- | --- |
    | ​  | `if` (array.length < 3) { `return` `null`; } |
    | ​  |  |
    | ​  | `let` largestProductSoFar = array[0] * array[1] * array[2]; |
    | ​  | `let` i = 0; |
    | ​  |  |
    | ​  | `while` (i < array.length) { |
    | ​  | `let` j = i + 1; |
    | ​  |  |
    | ​  | `while` (j < array.length) { |
    | ​  | `let` k = j + 1; |
    | ​  |  |
    | ​  | `while` (k < array.length) { |
    | ​  | `if` (array[i] * array[j] * array[k] > largestProductSoFar) { |
    | ​  | largestProductSoFar = array[i] * array[j] * array[k]; |
    | ​  | } |
    | ​  | k += 1; |
    | ​  | } |
    | ​  |  |
    | ​  | j += 1; |
    | ​  | } |
    | ​  |  |
    | ​  | i += 1; |
    | ​  | } |
    | ​  |  |
    | ​  | `return` largestProductSoFar; |
    | ​  | } |

1.  我曾经看到一个针对人力资源人员的笑话：“想要立即排除你招聘过程中的最不幸运的人吗？只需把你桌子上的一半简历扔进垃圾桶。”

    如果我们要编写一个软件，它不断减少一堆简历，直到只剩下一份，可能会采用交替丢弃顶部一半和底部一半的方式；也就是说，它将首先消除顶部一半的堆，然后继续消除剩下的底部一半。它在消除顶部和底部之间不断交替，直到只剩下一份幸运的简历，这就是我们要雇佣的人！

    描述该函数的效率，使用大 O 表示法：

    | ​  | `function` pickResume(resumes) { |
    | --- | --- |
    | ​  | `if` (resumes.length === 0) { `return` `null`; } |
    | ​  |  |
    | ​  | `let` eliminate = 'top'; |
    | ​  |  |
    | ​  | `while` (resumes.length > 1) { |
    | ​  | `const` midpoint = Math.floor(resumes.length / 2); |
    | ​  |  |
    | ​  | `if` (eliminate === 'top') { |
    | ​  | `resumes = resumes.slice(0, midpoint);` |
    | ​  | `eliminate = 'bottom';` |
    | ​  | } `else` `if` (eliminate === 'bottom') { |
    | ​  | `resumes = resumes.slice(midpoint);` |
    | ​  | `eliminate = 'top';` |
    | ​  | } |
    | ​  | } |
    | ​  |  |
    | ​  | `return` resumes[0]; |
    | ​  | `}` |

版权所有 © 2024, The Pragmatic Bookshelf.
