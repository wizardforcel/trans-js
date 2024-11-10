## 贪婪算法

这个下一步策略可以加速一些最顽固的算法。它并不适用于每种情况，但在适用时，它可能会改变游戏规则。

让我们谈谈编写贪婪算法。

这听起来可能是一个奇怪的术语，但它的意思是这样的：贪婪算法是在每一步中选择当时看起来最好的选项。这会通过一个基本示例变得清晰。

### 数组最大值

让我们编写一个算法，找到数组中的最大数字。我们可以通过嵌套循环来做到这一点，检查数组中的每个数字与其他每个数字。当我们找到一个大于其他所有数字的数字时，就意味着我们找到了数组中的最大数字。

正如这种算法的典型特征，这种方法的时间复杂度是 `O(N²)`。

另一种方法是将数组按升序排序，并返回数组中的最后一个值。如果我们使用像 `Quicksort` 这样的快速排序算法，这将需要 `O(N log N)` 的时间。

第三个选项是贪婪算法：

| ​  | `function` max(`array`) { |
| --- | --- |
| ​  | `if` (`array.length === 0`) { `return` `null`; } |
| ​  |  |
| ​  | `let` greatestNumber = `array[0]`; |
| ​  |  |
| ​  | `for` (`const` `number` `of` `array`) { |
| ​  | `if` (`number > greatestNumber`) { |
| ​  | greatestNumber = `number`; |
| ​  | } |
| ​  | } |
| ​  |  |
| ​  | `return` greatestNumber; |
| ​  | } |

在确保数组不为空后，我们说：

| ​  | `let` greatestNumber = `array[0]`; |
| --- | --- |

这一行“假设”数组中的第一个数字是 greatestNumber。现在，这是一个“贪婪”的假设；也就是说，我们将第一个数字声明为 greatestNumber，因为它是我们迄今为止遇到的最大数字。当然，它也是我们迄今为止遇到的唯一数字！但这就是贪婪算法的作用——它根据当时可用的信息选择看起来最好的选项。

接下来，我们遍历数组中的所有数字。当我们找到任何大于 greatestNumber 的数字时，我们就把这个新数字设为 greatestNumber。在这里，我们同样是贪婪的；每一步都基于我们当时所知的信息选择最佳选项。

我们基本上就像一个在糖果店里的孩子，抓住我们看到的第一块糖果，但一旦看到更大的糖果，我们就会扔掉第一块，抓住更大的那块。

然而，这种看似幼稚的贪婪实际上是有效的。当我们完成这个函数时，我们的 greatestNumber 确实会是整个数组中的最大数字。

尽管在社会背景下，贪婪并不是一种美德，但它可以极大地提升算法的速度。这个算法只需要 `O(N)` 的时间，因为我们每个数字只接触一次。

### 最大子区间和

让我们看看另一个贪婪算法如何获得好处的例子。

我们要编写一个函数，该函数接受一个数字数组，并返回可以从数组的任何“子区间”计算出的最大和。

我是这个意思。让我们来看以下数组：

| ​  | `[3, -4, 4, -3, 5, -9]` |
| --- | --- |

如果我们计算这个数组中所有数字的和，我们会得到`-4`。

但我们也可以计算数组子区段的和：

![`images/tips_for_code_optimization/subsection_sums.png`](images/tips_for_code_optimization/subsection_sums.png)

当我提到子区段时，我是指连续的子区段；即，一个子区段是包含一系列数字的数组的一部分。

以下不是一个连续的子区段，因为数字不在一行：

![`images/tips_for_code_optimization/not_in_a_row.png`](images/tips_for_code_optimization/not_in_a_row.png)

我们的任务是找到可以从数组中任何子区段计算得出的最大和。在我们的例子中，最大的和是`6`，来源于以下子区段：

![`images/tips_for_code_optimization/largest_sum_6.png`](images/tips_for_code_optimization/largest_sum_6.png)

为了简化讨论，假设数组至少包含一个正数。

现在，我们该如何编写代码来计算最大的子区段和呢？

一种方法是计算数组中每个子区段的和，并挑选出最大的那个。然而，对于`N`个项目的数组，约有`N² / 2`个子区段，因此仅生成不同的子区段就需要`O(N²)`的时间。

再次，让我们从构思最佳的 Big `O`开始。我们肯定需要至少检查每个数字一次，所以我们不能超过`O(N)`。因此，让`O(N)`成为我们的目标。

乍一看，`O(N)`似乎超出了我们的能力范围。我们如何能通过仅一次遍历数组来计算多个子区段的和呢？

让我们看看如果我们稍微贪心一下会发生什么…

在这个上下文中，贪心算法会尝试在我们遍历数组的每一步“抓住”最大的和。这可能在我们遍历早期示例数组时看起来是这样的。

从数组的前面开始，我们遇到了一个`3`。以完美的贪心方式，我们会说我们的最大和是`3`：

![`images/tips_for_code_optimization/encounter_3.png`](images/tips_for_code_optimization/encounter_3.png)

接下来，我们遇到了`-4`。当我们将其加到之前的`3`上时，得到当前和`-1`。因此`3`仍然是我们的最大和：

![`images/tips_for_code_optimization/encounter_negative_4.png`](images/tips_for_code_optimization/encounter_negative_4.png)

然后我们遇到了`4`。如果我们将其加到当前和上，我们得到`3`：

![`images/tips_for_code_optimization/encounter_4.png`](images/tips_for_code_optimization/encounter_4.png)

到目前为止，`3`仍然是最大的和。

我们接下来的数字是`-3`。这使得我们的当前和为`0`：

![`images/tips_for_code_optimization/encounter_negative_3.png`](images/tips_for_code_optimization/encounter_negative_3.png)

再次强调，虽然`0`是我们当前的和，`3`仍然是我们最大的和。

接下来，我们到达`5`。这使得我们的当前和为`5`。在我们的贪心之下，我们会宣布这是最大的和，因为这是我们迄今为止遇到的最大和：

![images/tips_for_code_optimization/encounter_5.png](images/tips_for_code_optimization/encounter_5.png)

然后我们到达最后一个数字`-9`。这使我们当前的和降至`-4`：

![images/tips_for_code_optimization/encounter_negative_9.png](images/tips_for_code_optimization/encounter_negative_9.png)

当我们到达数组的末尾时，我们的最大和为`5`。所以如果我们遵循这种纯贪婪的方法，似乎我们的算法应该返回`5`。

然而，`5`并不是最大的子区间和。数组中的一个子区间的和为`6`：

![images/tips_for_code_optimization/largest_sum_6.png](images/tips_for_code_optimization/largest_sum_6.png)

我们算法的问题在于我们只计算了从数组中第一个数字开始的子区间的最大和。但其他子区间也可能以数组中后面的数字开始，而我们并没有考虑这些情况。

那么，我们的贪婪算法没有达到我们希望的效果。

但我们还不应该放弃！通常，我们需要稍微调整贪婪算法才能使其有效。

让我们看看找到一个模式是否会有所帮助。（通常会。）正如我们之前所见，寻找模式的最佳方法是生成大量示例。所以让我们提出一些数组及其最大子区间和的示例，看看是否能发现什么有趣的东西：

![images/tips_for_code_optimization/largest_sum_examples.png](images/tips_for_code_optimization/largest_sum_examples.png)

在分析这些情况时，一个有趣的问题浮现出来：为什么在某些情况下，最大和来自一个从数组开始的子区间，而在其他情况下却不是？

在观察这些情况时，我们可以看到，当最大的子区间不从开始处开始时，是因为一个负数打断了连胜：

![images/tips_for_code_optimization/streak_breakers.png](images/tips_for_code_optimization/streak_breakers.png)

最大的子区间本应来自数组的开始，但一个负数破坏了连胜，导致最大子区间必须从数组的后面开始。

但等一下。在某些情况下，最大的子区间包含一个负数，而这个负数并没有打断连胜：

![images/tips_for_code_optimization/unbroken_streak.png](images/tips_for_code_optimization/unbroken_streak.png)

那么区别是什么？

这个模式是这样的：如果负数导致前一个子区间的和降到负数，连胜就被打断。但如果负数只是降低了当前子区间的和，而和仍然是正数，那么连胜就没有被打断。

如果我们仔细想想，这就有道理。如果在我们遍历数组时，当前子区间的和变得小于0，我们最好将当前和重置为0。否则，当前的负和只会减少我们想要找到的最大和。

所以让我们利用这个见解来调整我们的贪心算法。

再次，让我们从 3 开始。当前最大总和为 3：

![images/tips_for_code_optimization/encounter_3.png](images/tips_for_code_optimization/encounter_3.png)

接下来，我们遇到了 -4。这将使我们的当前总和为 -1：

![images/tips_for_code_optimization/encounter_negative_4.png](images/tips_for_code_optimization/encounter_negative_4.png)

由于我们试图找到最大总和的子部分，而当前总和是负数，我们需要在继续到下一个数字之前将当前总和重置为 0：

![images/tips_for_code_optimization/reset_sum_to_zero.png](images/tips_for_code_optimization/reset_sum_to_zero.png)

我们还将以下一个数字开始一个全新的子部分。

再次，推理是如果下一个数字是正数，我们不妨从那里开始下一个子部分，而不是让当前的负数拖低总和。相反，我们将通过将当前总和重置为 0 来执行重置，并将下一个数字视为新子部分的开始。

所以让我们继续。

我们现在达到了 4。这又是一个新子部分的开始，所以当前总和是 4，这也成为了我们迄今为止看到的最大总和：

![images/tips_for_code_optimization/greatest_sum_is_4.png](images/tips_for_code_optimization/greatest_sum_is_4.png)

接下来，我们遇到了 -3。当前的总和现在是 1：

![images/tips_for_code_optimization/current_sum_is_1.png](images/tips_for_code_optimization/current_sum_is_1.png)

我们接下来遇到了 5。这使得当前总和为 6，这也是最大的总和：

![images/tips_for_code_optimization/current_sum_is_6.png](images/tips_for_code_optimization/current_sum_is_6.png)

最后，我们达到了 -9。这将使当前总和为 -3，在这种情况下，我们将其重置为 0。然而，我们也达到了数组的末尾，可以得出最大总和是 6。确实，这就是正确的结果。

这是这个方法的代码：

| ​  | `function` maxSum(array) { |
| --- | --- |
| ​  | `let` currentSum = 0; |
| ​  | `let` greatestSum = 0; |
| ​  |  |
| ​  | `for` (`const` num `of` array) { |
| ​  | `if` (currentSum + num < 0) { |
| ​  | currentSum = 0; |
| ​  | } `else` { |
| ​  | currentSum += num; |
| ​  | `if` (currentSum > greatestSum) { |
| ​  | `greatestSum = currentSum;` |
| ​  | } |
| ​  | } |
| ​  | } |
| ​  |  |
| ​  | `return` greatestSum; |
| ​  | } |

使用这个贪心算法，我们能够在 `O(N)` 时间内解决这个棘手的问题，因为我们只遍历了一次数字数组。这比我们最初的 `O(N²)` 方法有了很大的改进。在空间方面，这个算法是 `O(1)`，因为我们不生成任何额外的数据。

虽然发现一个模式帮助我们找到了精确的解决方案，但通过采用贪心思维方式，我们一开始就知道我们在寻找什么样的模式。

### 贪心股票预测

让我们再看看一个贪心算法。

假设我们正在编写能够进行股票预测的金融软件。我们现在正在研究的特定算法寻找给定股票的正向趋势。

具体来说，我们正在编写一个接受股票价格数组并确定是否存在任何三个价格创建向上趋势的函数。

例如，这是一个代表给定股票随时间变化的股票价格数组：

| ​  | `[22, 25, 21, 18, 19.6, 17, 16, 20.5]` |
| --- | --- |

虽然一开始可能难以发现，但有三个价格形成了向上的趋势：

![`images/tips_for_code_optimization/upward_trend.png`](images/tips_for_code_optimization/upward_trend.png)

当我们从左到右时，有三个价格，其中一个“右侧”价格大于“中间”价格，而“中间”价格反过来又大于“左侧”价格。

另一方面，以下数组不包含三点向上趋势：

| ​  | `[50, 51.25, 48.4, 49, 47.2, 48, 46.9]` |
| --- | --- |

如果数组包含三个价格的向上趋势，我们的函数应返回`true`，否则返回`false`。

那么我们该如何处理呢？

我们可以通过三重嵌套循环来实现这一点。当一个循环迭代每个股票价格时，第二个循环迭代后续的所有股票价格。而对于第二个循环的每一轮，第三个嵌套循环检查后续第二个价格的所有价格。当我们指向每组三个股票价格时，我们检查它们是否按升序排列。一旦我们找到这样的一组，我们返回`true`。但如果我们完成循环而没有找到任何这样的趋势，我们返回`false`。

这个算法的时间复杂度为`O(N³)`。速度相当慢！有没有什么方法可以优化呢？

让我们首先考虑最佳的 Big O。我们肯定需要检查每个股票价格来找出趋势，因此我们知道我们的算法不可能比`O(N)`更快。让我们看看是否可以优化这样的速度。

再次，现在是贪婪的时候了。

要将贪婪思维应用于我们的情况，我们希望以某种方式始终获取我们认为是三价格向上趋势最低点的值。如果我们能够使用相同的贪婪方法不断获取我们认为是该趋势中的中间和最高点的值，那将会很棒。

这是我们将要做的：

我们假设数组中的第一个价格是三价格向上趋势中的最低点。

至于中间价格，我们将其初始化为一个保证大于数组中最高股票价格的数字。为此，我们将其设置为`infinity`。这个步骤乍一看可能是最不直观的，但你很快会看到我们为什么需要这样做。

然后我们将按照以下步骤对整个数组进行一次遍历：

1.  如果当前价格低于我们迄今为止遇到的最低价格，这个价格将成为新的最低价格。

1.  如果当前价格高于最低价格但低于中间价格，我们将中间价格更新为当前价格。

1.  如果当前价格高于中间价格，这意味着我们发现了一个三价格上升趋势！

让我们看看这个操作。首先，我们将从一个简单的例子开始，处理这个股票价格数组：

![images/tips_for_code_optimization/array_of_stocks.png](images/tips_for_code_optimization/array_of_stocks.png)

我们从`5`开始遍历数组。我们一开始就充满贪婪，假设这个`5`是三点趋势中的最低价格，如下数组所示：

![images/tips_for_code_optimization/stock_5.png](images/tips_for_code_optimization/stock_5.png)

接下来，我们处理`2`。因为`2`低于`5`，我们变得更加贪婪，假设`2`现在是趋势中的最低价格：

![images/tips_for_code_optimization/stock_2.png](images/tips_for_code_optimization/stock_2.png)

我们到达数组中的下一个数字，`8`。这个数字高于我们的最低点，所以我们保持最低点为`2`。然而，它低于当前的中间价格，即`infinity`，所以我们现在贪婪地将`8`赋值为我们三点趋势中的中间点：

![images/tips_for_code_optimization/stock_8.png](images/tips_for_code_optimization/stock_8.png)

接下来，我们到达`4`。这个值高于`2`，所以我们继续假设`2`是我们趋势中的最低点。然而，由于`4`低于`8`，我们将`4`作为我们的新中间点，而不是`8`。这也是出于贪婪，因为通过降低我们的中间点，我们增加了找到更高价格的机会，从而形成我们所寻求的趋势。因此，`4`是我们的新中间点：

![images/tips_for_code_optimization/stock_4.png](images/tips_for_code_optimization/stock_4.png)

数组中的下一个数字是`3`。我们将最低价格保持为`2`，因为`3`大于它。但我们将其作为我们的新中间点，因为它低于`4`：

![images/tips_for_code_optimization/stock_3.png](images/tips_for_code_optimization/stock_3.png)

最后，我们到达`7`，这是数组中的最后一个值。因为`7`大于我们的中间价格（`3`），这意味着数组包含一个上升的三点趋势，我们的函数可以返回`true`：

![images/tips_for_code_optimization/stock_7.png](images/tips_for_code_optimization/stock_7.png)

注意数组中存在两种这样的趋势。一个是`2-3-7`，但还有一个是`2-4-7`。不过，这对我们来说并不重要，因为我们只是想确定这个数组是否包含任何上升趋势；因此找到一个实例就足以返回`true`。

这是该算法的一种实现：

| ​  | `function` `isIncreasingTriplet(array)` { |
| --- | --- |
| ​  | `let` `lowestPrice = array[0];` |
| ​  | `let` `middlePrice = `**Infinity**`;` |
| ​  |  |
| ​  | `for` (`const` price `of` array) { |
| ​  | `if` (price <= `lowestPrice`) { |
| ​  | `lowestPrice = price;` |
| ​  | } `else` `if` (price <= `middlePrice`) { |
| ​  | `middlePrice = price;` |
| ​  | } `else` { |
| ​  | `return` `true`; |
| ​  | } |
| ​  | } |
| ​  |  |
| ​  | `return` `false`; |
| ​  | } |

这个算法的一个反直觉的方面值得指出。具体来说，在某些情况下，这个算法似乎不起作用，但实际上是有效的。

让我们看看这个场景：

![images/tips_for_code_optimization/second_stock_example.png](images/tips_for_code_optimization/second_stock_example.png)

让我们看看当我们将算法应用于这个数组时会发生什么。

起初，`8`成为我们的最低点：

![images/tips_for_code_optimization/second_example_stock_8.png](images/tips_for_code_optimization/second_example_stock_8.png)

然后`9`成为我们的中间点：

![images/tips_for_code_optimization/second_example_stock_9.png](images/tips_for_code_optimization/second_example_stock_9.png)

接下来，我们到达`7`。因为这低于我们的最低点，我们将最低点更新为`7`：

![images/tips_for_code_optimization/second_example_stock_7.png](images/tips_for_code_optimization/second_example_stock_7.png)

然后我们到达`10`：

![images/tips_for_code_optimization/second_example_stock_10.png](images/tips_for_code_optimization/second_example_stock_10.png)

因为`10`大于当前的中间点`9`，我们的函数返回了`true`。现在，这是正确的响应，因为我们的数组确实包含`8-9-10`的趋势。然而，当我们的函数完成时，最低点变量指向的是`7`。但`7`并不是上升趋势的一部分！

尽管如此，我们的函数仍然返回了正确的响应。这是因为我们函数所需做的只是达到一个高于中间点的数字。由于中间点只是在找到其前面的低点后才建立的，一旦我们达到一个高于中间点的数字，这仍然意味着数组中存在上升趋势。即使我们最后将低点覆盖成了其他数字，这一点依然成立。

无论如何，我们的贪心方法取得了成功，因为我们只对数组迭代了一次。这是一个惊人的改进，因为我们将一个运行时间为`O(N³)`的算法转变为`O(N)`。

当然，贪心算法并不总是有效。但它是你在优化算法时可以尝试的另一个工具。
