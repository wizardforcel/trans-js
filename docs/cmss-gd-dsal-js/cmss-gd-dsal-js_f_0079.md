## 建立一个有趣且有利可图的词库，但主要是为了盈利

在夜晚和周末，你正在单枪匹马地开发一个能够统治世界的隐形创业公司。它是……一个词库应用。但这不是任何普通的词库应用——这是`Quickasaurus`。你知道它将彻底颠覆十亿美金的词库市场。当用户在`Quickasaurus`中查找一个单词时，它只返回一个同义词，而不是像传统词库应用那样返回所有可能的同义词。

由于每个单词都有一个关联的同义词，这对于哈希表来说是一个很好的用例。毕竟，哈希表是成对项目的列表。让我们开始吧。

我们可以用哈希表表示我们的词库：

|   | `thesaurus = {};` |
| --- | --- |

从底层看，哈希表将其数据存储在一排单元格中，类似于数组。每个单元格都有一个对应的编号，如下例所示：

![images/blazing_fast_lookup_with_hashes/hash_1.png](images/blazing_fast_lookup_with_hashes/hash_1.png)

（我们省略了索引`0`，因为根据我们的乘法哈希函数，那里不会存储任何内容。）

让我们将第一个条目添加到哈希表中：

|   | `thesaurus["bad"] = "evil"` |
| --- | --- |

在代码中，我们的哈希表现在看起来是这样的：

|   | `{"bad": "evil"}` |
| --- | --- |

让我们深入探讨哈希表如何存储这些数据。

首先，计算机将哈希函数应用于键。我们将使用之前描述的乘法哈希函数。所以计算如下：

`BAD = 2 * 1 * 4 = 8`

由于我们的键（`"bad"`）哈希到`8`，计算机将值（`"evil"`）放入单元格`8`：

![images/blazing_fast_lookup_with_hashes/hash_2.png](images/blazing_fast_lookup_with_hashes/hash_2.png)

现在，让我们添加另一个键值对：

|   | `thesaurus["cab"] = "taxi";` |
| --- | --- |

计算机再次对键进行哈希：

`CAB = 3 * 1 * 2 = 6`

由于结果值是`6`，计算机将值（`"taxi"`）存储在单元格`6`中。

![images/blazing_fast_lookup_with_hashes/hash_3.png](images/blazing_fast_lookup_with_hashes/hash_3.png)

让我们再添加一个键值对：

|   | `thesaurus["ace"] = "star";` |
| --- | --- |

总结一下这里发生的事情：对于每个键值对，每个值在键被哈希后存储在键的索引处。

`ACE`哈希到`15`，因为`ACE = 1 * 3 * 5 = 15`，所以`"star"`被放入单元格`15`：

![images/blazing_fast_lookup_with_hashes/hash_4.png](images/blazing_fast_lookup_with_hashes/hash_4.png)

在代码中，我们的哈希表目前看起来是这样的：

|   | `{"bad": "evil", "cab": "taxi", "ace": "star"}` |
| --- | --- |
