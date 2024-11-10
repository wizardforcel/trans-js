## 第20章

这些是[`练习`](f_0204.xhtml#tips.for.code.optimization.exercises)部分的练习解决方案。

1.  如果我们问自己：“如果我能在`O(1)`的时间内神奇地找到所需的信息，我能否让我的算法更快？”那么我们就可以优化这个算法。

    具体来说，当我们遍历一个数组时，我们希望能“神奇地”在另一个数组中以`O(1)`的时间查找那个运动员。为此，我们可以先将其中一个数组转换为哈希表。我们将全名（即名和姓）作为键，`true`（或任何任意项）作为值。

    一旦我们将一个数组转换为这个哈希表，我们就遍历另一个数组。当我们遇到每个运动员时，我们在哈希表中进行一次`O(1)`的查找，以查看该运动员是否已经在另一个运动中比赛。如果是，我们就将该运动员添加到我们的`multisportAthletes`数组中，最后在函数结束时返回它。

    这里是这个方法的代码：

    | ​  | `function` findMultisportAthletes(array1, array2) { |
    | --- | --- |
    | ​  | `const` hashTable = {}; |
    | ​  | `const` multisportAthletes = []; |
    | ​  |  |
    | ​  | `for` ( `const` athlete `of` array1) { |
    | ​  | `hashTable[`*`*​${athlete.firstName}​​${athlete.lastName}​*`*​] = `true`; |
    | ​  | } |
    | ​  |  |
    | ​  | `for` ( `const` athlete `of` array2) { |
    | ​  | `if` (hashTable[`*`*​${athlete.firstName}​​${athlete.lastName}​*`*​]) { |
    | ​  | multisportAthletes.push(​*`*​${athlete.firstName}​​${athlete.lastName}​*`*​); |
    | ​  | } |
    | ​  | } |
    | ​  |  |
    | ​  | `return` multisportAthletes; |
    | ​  | } |

    这个算法是`O(N + M)`，因为我们只需遍历每组运动员一次。

1.  对于这个算法，生成例子以寻找模式将非常有帮助。

    让我们取一个包含六个整数的数组，看看每次移除一个不同的整数会发生什么：

    | ​  | [1, 2, 3, 4, 5, 6] : 缺失`0`：`sum = 21` |
    | --- | --- |
    | ​  | [0, 2, 3, 4, 5, 6] : 缺失`1`：`sum = 20` |
    | ​  | [0, 1, 3, 4, 5, 6] : 缺失`2`：`sum = 19` |
    | ​  | [0, 1, 2, 4, 5, 6] : 缺失`3`：`sum = 18` |
    | ​  | [0, 1, 2, 3, 5, 6] : 缺失`4`：`sum = 17` |
    | ​  | [0, 1, 2, 3, 4, 6] : 缺失`5`：`sum = 16` |

    嗯。当我们移除`0`时，总和是`21`。当我们移除`1`时，总和是`20`。而当我们移除`2`时，总和是`19`，依此类推。这显然是一个模式！

    在我们深入之前，让我们把这个例子中的`21`称为“完整总和”。这是数组在只缺少`0`时的总和。

    如果我们仔细分析这些情况，就会发现任何数组的总和比完整的总和少了缺失数字的值。例如，当我们缺失`4`时，总和是`17`，比`21`少四。而当我们缺失`1`时，总和是`20`，比`21`少一。

    所以我们可以通过计算完整总和来开始我们的算法。然后我们可以从完整总和中减去实际总和，这将是我们的缺失数字。

    这里是这个代码：

    | ​  | `function` `findMissingNumber`(`array`) { |
    | --- | --- |
    | ​  | `let` `fullSum` = `0`; |
    | ​  |  |
    | ​  | `for`(`let` `num` = `1`; `num` <= `array.length`; `num` += `1`) { |
    | ​  | `fullSum` += `num`; |
    | ​  | } |
    | ​  |  |
    | ​  | `let` `currentSum` = `0`; |
    | ​  |  |
    | ​  | `for`(`const` `num` `of` `array`) { |
    | ​  | `currentSum` += `num`; |
    | ​  | } |
    | ​  |  |
    | ​  | `return` `fullSum` - `currentSum`; |
    | ​  | `}` |

    -   这个算法是 O(N)。计算总和需要 N 步，然后再计算实际总和需要 N 步。总共是 2N 步，简化为 O(N)。

1.  -   如果我们使用贪心算法，这个函数可以变得更快。（也许这并不令人惊讶，因为我们的代码试图在股票上获得尽可能大的利润。）

    -   为了获得最大的利润，我们希望尽可能低价买入，尽可能高价卖出。我们的贪心算法首先将第一个价格赋值为 `buyPrice`。然后我们遍历所有价格，一旦找到更低的价格，就将其作为新的 `buyPrice`。

    -   同样地，在遍历价格时，我们检查如果以当前价格出售能赚多少利润。利润通过从当前价格减去 `buyPrice` 计算得出。以贪心的方式，我们将这个利润保存在一个名为 `greatestProfit` 的变量中。当我们遍历所有价格时，每当发现更大的利润时，就更新 `greatestProfit`。

    -   当我们完成遍历价格时，`greatestProfit` 将保存我们通过一次买入和卖出所能获得的最大利润。

    -   这是我们算法的代码：

    | ​  | `function` `findGreatestProfit`(`array`) { |
    | --- | --- |
    | ​  | `let` `buyPrice` = `array[0]`; |
    | ​  | `let` `greatestProfit` = `0`; |
    | ​  |  |
    | ​  | `for`(`const` price `of` array) { |
    | ​  | `const` `potentialProfit` = `price` - `buyPrice`; |
    | ​  |  |
    | ​  | `if` (`price` < `buyPrice`) { |
    | ​  | `buyPrice` = `price`; |
    | ​  | `} else if` (`potentialProfit` > `greatestProfit`) { |
    | ​  | `greatestProfit` = `potentialProfit`; |
    | ​  | } |
    | ​  | } |
    | ​  |  |
    | ​  | `return` `greatestProfit`; |
    | ​  | } |

    -   因为我们仅遍历 N 个价格一次，所以我们的函数运行时间为 O(N)。我们不仅赚了很多钱，而且速度也很快。

1.  -   这是另一个通过生成示例来寻找模式以优化的算法。

    -   根据练习的说明，最大乘积可能是负数的结果。让我们看一下各种数组及其由两个数字形成的最大乘积的例子：

    | ​  | `[-5, -4, -3, 0, 3, 4]` -> 最大乘积: `20` (`-5 * -4`) |
    | --- | --- |
    | ​  | `[-9, -2, -1, 2, 3, 7]` -> 最大乘积: `21` (`3 * 7`) |
    | ​  | `[-7, -4, -3, 0, 4, 6]` -> 最大乘积: `28` (`-7 * -4`) |
    | ​  | `[-6, -5, -1, 2, 3, 9]` -> 最大乘积: `30` (`-6 * -5`) |
    | ​  | `[-9, -4, -3, 0, 6, 7]` -> 最大乘积: `42` (`6 * 7`) |

    看到这些情况可能会帮助我们意识到，最大的乘积只能由最大的两个数字或最低的两个（负）数字组成。

    考虑到这一点，我们应该设计我们的算法来跟踪这四个数字：

    +   最大的数字

    +   第二大数字

    +   最低的数字

    +   第二低的数字

    然后我们可以比较两个最大数字的乘积与两个最小数字的乘积。较大的乘积就是数组中的最大乘积。

    现在，我们如何找到最大的两个数字和最低的两个数字？如果我们对数组进行排序，那将很简单。但这仍然是 O(N log N)，而说明中说我们可以实现 O(N)。

    事实上，我们可以在一次遍历数组中找到所有四个数字。是时候再次采取贪心策略了。

    这里是代码及其解释：

    | ​  | `function` greatestProduct(array) { |
    | --- | --- |
    | ​  | `let` greatestNumber = -`Infinity`; |
    | ​  | `let` secondToGreatestNumber = -`Infinity`; |
    | ​  |  |
    | ​  | `let` lowestNumber = `Infinity`; |
    | ​  | `let` secondToLowestNumber = `Infinity`; |
    | ​  |  |
    | ​  | `for` (`const` number `of` array) { |
    | ​  | `if` (number >= greatestNumber) { |
    | ​  | secondToGreatestNumber = greatestNumber; |
    | ​  | greatestNumber = number; |
    | ​  | } `else` `if` (number > secondToGreatestNumber) { |
    | ​  | secondToGreatestNumber = number; |
    | ​  | } |
    | ​  |  |
    | ​  | `if` (number <= lowestNumber) { |
    | ​  | secondToLowestNumber = lowestNumber; |
    | ​  | lowestNumber = number; |
    | ​  | } `else` `if` (number < secondToLowestNumber) { |
    | ​  | secondToLowestNumber = number; |
    | ​  | } |
    | ​  | } |
    | ​  |  |
    | ​  | `const` greatestProductFromTwoHighest = |
    | ​  | (greatestNumber * secondToGreatestNumber); |
    | ​  |  |
    | ​  | `const` greatestProductFromTwoLowest = (lowestNumber * secondToLowestNumber); |
    | ​  |  |
    | ​  | `if` (greatestProductFromTwoHighest > greatestProductFromTwoLowest) { |
    | ​  | `return` greatestProductFromTwoHighest; |
    | ​  | } `else` { |
    | ​  | `return` greatestProductFromTwoLowest; |
    | ​  | } |
    | ​  | } |

    在我们开始循环之前，我们将 greatestNumber 和 secondToGreatestNumber 设置为负无穷。这确保它们的初始值低于数组中的任何数字。

    然后我们遍历每个数字。如果当前数字大于 greatestNumber，我们就贪婪地将当前数字设为新的 greatestNumber。如果我们已经找到 secondToGreatestNumber，我们将其重新分配为在到达当前数字之前的 greatestNumber。这样可以确保 secondToGreatestNumber 确实是第二大的数字。

    如果当前迭代的数字小于 greatestNumber 但大于 secondToGreatestNumber，我们将 secondToGreatestNumber 更新为当前数字。

    我们按照相同的过程找到`lowestNumber`和`secondToLowestNumber`。

    一旦找到所有四个数字，我们计算两个最高数字的乘积和两个最低数字的乘积，并返回较大的乘积。

1.  优化该算法的关键在于我们正在对有限数量的值进行排序。具体来说，这个数组中只有十一种温度读数，即：

    | ​  | 95, 96, 97, 98, 99, 100, 101, 102, 103, 104, 105 |
    | --- | --- |

    假设我们的输入数组是：

    | ​  | [98, 99, 95, 105, 104, 99, 101, 99, 101, 97] |
    | --- | --- |

    如果我们将温度数组想象成一个哈希表，我们可以将每个温度存储为键，将出现次数存储为值。它的形式大致如下：

    | ​  | {98: 1, 99: 3, 95: 1, 105: 1, 104: 1, 101: 2, 97:1} |
    | --- | --- |

    考虑到这一点，我们可以运行一个从 95 到 105 的循环，并检查哈希表中该温度的出现次数。每次查找的时间复杂度都是 O(1)。

    然后我们使用该出现次数来填充一个新数组。因为我们的循环设置为从 95 到 105，所以我们的数组最终将呈现完美的升序。

    这里是该代码：

    | ​  | `function` sortTemperatures(array) { |
    | --- | --- |
    | ​  | `const` hashTable = {}; |
    | ​  |  |
    | ​  | `for` (`const` temperature `of` array) { |
    | ​  | `if` (hashTable[temperature]) { |
    | ​  | hashTable[temperature] += 1; |
    | ​  | } `else` { |
    | ​  | hashTable[temperature] = 1; |
    | ​  | } |
    | ​  | } |
    | ​  |  |
    | ​  | `const` sortedTemperatures = []; |
    | ​  | `let` temperature = 95; |
    | ​  |  |
    | ​  | `while` (temperature <= 105) { |
    | ​  | `if` (hashTable[temperature]) { |
    | ​  | `for` (`let` i = 0; i < hashTable[temperature]; i += 1) { |
    | ​  | sortedTemperatures.push(temperature); |
    | ​  | } |
    | ​  | } |
    | ​  |  |
    | ​  | temperature += 1; |
    | ​  | } |
    | ​  |  |
    | ​  | `return` sortedTemperatures; |
    | ​  | } |

    现在让我们分析该算法的效率。我们需要 N 步骤来创建哈希表。然后我们循环执行十一次，遍历所有可能的温度，从 95 到 105。

    在每轮循环中，我们运行一个嵌套循环来填充`sortedTemperatures`与温度。然而，这个内层循环不会运行超过输入数组中的 N 个温度。这是因为内层循环仅针对原始数组中的每个温度运行一次。

    因此，我们有 N 步骤来创建哈希表，外层循环需要十一步，内层循环也需要 N 步骤。这是 2N + 11，简化为 O(N)。

    该算法是经典的排序算法，称为计数排序。它在处理相对小范围的可能输入值时非常有用，例如我们这一例中只有十一种可能的值。

1.  这种优化运用了我见过的最巧妙的魔法查找。

    想象一下，我们正在遍历数字数组，遇到了`5`。让我们问自己一个神奇的查找问题：“如果我能在`O(1)`时间内神奇地找到所需的信息，我能否让我的算法更快？”

    好吧，为了确定`5`是否是最长连续序列的一部分，我们需要知道数组中是否有`6`。我们还想知道是否有`7`、`8`，依此类推。

    我们可以在`O(1)`时间内完成每次查找，如果我们首先将数组中的所有数字存储在哈希表中；也就是说，数组`[10, 5, 12, 3, 55, 30, 4, 11, 2]`如果移动到哈希表中，可能看起来是这样的：

    | ​  | {10: `true`, 5: `true`, 12: `true`, 3: `true`, 55: `true`, |
    | --- | --- |
    | ​  | 30: `true`, 4: `true`, 11: `true`, 2: `true`} |

    在这种情况下，如果我们遇到`2`，我们可以运行一个循环，不断检查哈希表中的下一个数字。如果找到了，我们就将当前序列的长度增加一。这个循环会重复这个过程，直到找不到序列中的下一个数字。每次查找只需一步。

    但是，你可能会问，这有什么帮助？想象一下我们的数组是`[6, 5, 4, 3, 2, 1]`。当我们遍历到`6`时，会发现从那里无法建立序列。当我们到达`5`时，会找到序列`5-6`。当我们到达`4`时，会找到序列`4-5-6`。当我们到达`3`时，会找到序列`3-4-5-6`，依此类推。我们仍然会经历大约`N² / 2`步来找到所有这些序列。

    答案是，我们只会在当前数字是序列的底部数字时开始构建序列。因此，当数组中有`3`时，我们不会构建`4-5-6`。

    但我们怎么知道当前数字是否是序列的底部？通过进行一次神奇的查找！

    怎么办？在运行循环寻找序列之前，我们会先进行一次`O(1)`的哈希表查找，以检查是否有比当前数字小`1`的数字。因此，如果当前数字是`4`，我们会首先检查数组中是否有`3`。如果有，我们就不必构建序列。我们只想从该序列的底部数字开始构建序列；否则，我们就会有冗余的步骤。

    这是实现这个功能的代码：

    | ​  | `function` longestSequenceLength(`array`) { |
    | --- | --- |
    | ​  | `const` hashTable = {}; |
    | ​  | `let` greatestSequenceLength = `0`; |
    | ​  |  |
    | ​  | `for` (`const` `number` `of` `array`) { |
    | ​  | `hashTable[number] = true;` |
    | ​  | } |
    | ​  |  |
    | ​  | `for` (`const` `number` `of` `array`) { |
    | ​  | `if` (!`hashTable[number - 1]`) { |
    | ​  | `let` currentSequenceLength = `1`; |
    | ​  | `let` currentNumber = `number`; |
    | ​  |  |
    | ​  | `while` (`hashTable[currentNumber + 1]`) { |
    | ​  | currentNumber += `1`; |
    | ​  | currentSequenceLength += `1`; |
    | ​  |  |
    | ​  | `if` (currentSequenceLength > greatestSequenceLength) { |
    | ​  | greatestSequenceLength = currentSequenceLength; |
    | ​  | } |
    | ​  | } |
    | ​  | } |
    | ​  | } |
    | ​  |  |
    | ​  | `return` greatestSequenceLength; |
    | ​  | } |

    在这个算法中，我们进行`N`步来构建哈希表。我们又花费`N`步遍历数组。然后大约再花费`N`步在哈希表中查找数字以构建不同的序列。总而言之，这大约是`3N`，简化为`O(N)`。

Copyright © 2024, `The Pragmatic Bookshelf`. Thank you!

我们希望你喜欢这本书，并且已经在思考接下来想要学习的内容。为了帮助你更轻松地做出决定，我们给你提供了这个礼物。

现在就去看看[`https://pragprog.com`](https://pragprog.com)，使用优惠码`BUYANOTHER2024`在你下次购买电子书时享受`30%`的折扣。此优惠在法律禁止或限制的地方无效。此优惠不适用于任何版本的`The Pragmatic Programmer`电子书。

如果你想与世界分享自己的专业知识，为什么不向我们提议一个写作想法呢？毕竟，我们许多优秀的作者都是从我们的读者开始的，就像你一样。最高可获得`50%`的稿酬，世界级的编辑服务，以及你信任的名字，完全没有风险。今天就访问[`https://pragprog.com/become-an-author/`](https://pragprog.com/become-an-author/)了解更多信息并开始吧。

感谢你一直以来的支持。我们希望不久后能再次听到你的消息！

`The Pragmatic Bookshelf`

![`images/Coupon.png`](images/Coupon.png)
