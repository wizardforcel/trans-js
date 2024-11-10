## 第8章

这些是[练习](f_0086.xhtml#blazing.fast.lookup.with.hashes.exercises)部分中的题目解答。

1.  以下实现首先将第一个数组的值存储在哈希表中，然后检查第二个数组的每个值与该哈希表的匹配：

    | ​  | `function` getIntersection(array1, array2) { |
    | --- | --- |
    | ​  | `const` intersection = []; |
    | ​  | `const` hashTable = {}; |
    | ​  |  |
    | ​  | array1.forEach((value) => { |
    | ​  | hashTable[value] = `true`; |
    | ​  | }); |
    | ​  |  |
    | ​  | array2.forEach((value) => { |
    | ​  | `if` (hashTable[value]) { |
    | ​  | intersection.push(value); |
    | ​  | } |
    | ​  | }); |
    | ​  |  |
    | ​  | `return` intersection; |
    | ​  | } |

    该算法的效率为O(N)。

1.  以下实现检查数组中的每个字符串。如果字符串尚不在哈希表中，则将字符串添加。如果字符串在哈希表中，这意味着它之前已经被添加过，这意味着它是重复的！该算法的时间复杂度为O(N)：

    | ​  | `function` findDuplicate(array) { |
    | --- | --- |
    | ​  | `const` hashTable = {}; |
    | ​  |  |
    | ​  | `for` (`const` value `of` array) { |
    | ​  | `if` (hashTable[value]) { |
    | ​  | `return` value; |
    | ​  | } `else` { |
    | ​  | hashTable[value] = `true`; |
    | ​  | } |
    | ​  | } |
    | ​  |  |
    | ​  | `return` `null`; |
    | ​  | } |

1.  以下实现首先创建一个哈希表，其中包含我们在字符串中遇到的所有字符。接下来，我们遍历字母表中的每个字符，检查该字符是否包含在我们的哈希表中。如果不包含，这意味着该字符在字符串中缺失，因此我们返回它：

    | ​  | `function` findMissingLetter(string) { |
    | --- | --- |
    | ​  | `const` hashTable = {}; |
    | ​  |  |
    | ​  | `for` (`const` `char` `of` string) { |
    | ​  | hashTable[`char`] = `true`; |
    | ​  | } |
    | ​  |  |
    | ​  | `const` alphabet = 'abcdefghijklmnopqrstuvwxyz'; |
    | ​  |  |
    | ​  | `for` (`const` `char` `of` alphabet) { |
    | ​  | `if` (!hashTable[`char`]) { |
    | ​  | `return` `char`; |
    | ​  | } |
    | ​  | } |
    | ​  |  |
    | ​  | `return` `null`; |
    | ​  | } |

1.  以下实现首先遍历字符串中的每个字符。如果字符尚不存在于哈希表中，则将字符作为键添加到哈希表，值为1，表示该字符到目前为止被找到一次。如果字符已经在哈希表中，我们只需将值加1。因此，如果字符"e"的值为3，这意味着"e"在字符串中出现了三次。

    然后我们再次遍历字符，返回字符串中仅出现一次的第一个字符。该算法的时间复杂度为O(N)：

    | ​  | `function` firstNonDuplicate(string) { |
    | --- | --- |
    | ​  | `const` hashTable = {}; |
    | ​  |  |
    | ​  | `for`(`const` `char` `of` string) { |
    | ​  | `if` (hashTable[`char`]) { |
    | ​  | `hashTable[` `char` `] += 1;` |
    | ​  | } `else` { |
    | ​  | `hashTable[` `char` `] = 1;` |
    | ​  | } |
    | ​  | } |
    | ​  |  |
    | ​  | `for`(`const` `char` `of` string) { |
    | ​  | `if` (hashTable[`char`] === 1) { |
    | ​  | `return` `char`; |
    | ​  | } |
    | ​  | } |
    | ​  | `return` `null`; |
    | ​  | } |
