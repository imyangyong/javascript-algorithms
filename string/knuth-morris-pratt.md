# KMP 算法

**Knuth-Morris-Pratt[字符串查找算法](https://zh.wikipedia.org/wiki/字符串查找算法) **（简称为**KMP算法**）可在一个**主文本字符串** `S` 内查找一个**子串** `W` 的出现位置。此算法通过运用对这个词在不匹配时本身就包含足够的信息来确定下一个匹配将在哪里开始，从而避免重新检查先前匹配的字符。

## 示例

让我们用一个实例来演示这个算法。在任意给定时间，本算法被两个整数 `m` 和 `i` 所决定：

- `m` 代表主文字符串 `S` 内匹配字符串 `W` 的当前查找位置，
- `i ` 代表匹配字符串 `W` 当前做比较的字符位置。

图示如下：

![img](https://img.imyangyong.com/blog/2020-07-09%2020-29-15.png)

我们从`W`与`S`的开头比较起。我们比对到`S[3](=' ')`时，发现`W[3](='D')`与其不符。接着并不是从`S[1]`比较下去。我们已经知道`S[1]~S[3]`不与`W[0]`相合。因此，略过这些字符，令`m = 4`以及`i = 0`。

![img](https://img.imyangyong.com/blog/2020-07-09%2020-30-11.png)

如上所示，我们检核了`"ABCDAB"`这个字符串。然而，这与目标仍有些差异。我们可以注意到，`"AB"`在字符串头尾处出现了两次。这意味着尾端的`"AB"`可以作为下次比较的起始点。因此，我们令`m = 8, i = 2`，继续比较。图标如下：

![img](https://img.imyangyong.com/blog/2020-07-09%2020-30-54.png)

于`m = 10`的地方，又出现不相符的情况。类似地，令`m = 11, i = 0`继续比较：

![img](https://img.imyangyong.com/blog/2020-07-09%2020-31-36.png)

这时，`S[17](='C')`不与`W[6]`相同，但是亦出现了两次`"AB"`，我们采取一贯的作法，令`m = 15`和`i = 2`，继续搜索。

![img](https://img.imyangyong.com/blog/2020-07-09%2020-32-16.png)

我们找到完全匹配的字符串了，其起始位置于`S[15]`的地方。

## 复杂度

- 时间复杂度：`O(|W| + |T|)` （比普通的遍历法快得多 `O(|W| * |T|)`）

- 空间复杂度：`O(|W|)`

## 代码

```javascript
/**
 * @see https://www.youtube.com/watch?v=GTJr8OvyEVQ
 * @param {string} word
 * @return {number[]}
 */
function buildPatternTable(word) {
  const patternTable = [0];
  let prefixIndex = 0;
  let suffixIndex = 1;

  while (suffixIndex < word.length) {
    if (word[prefixIndex] === word[suffixIndex]) {
      patternTable[suffixIndex] = prefixIndex + 1;
      suffixIndex += 1;
      prefixIndex += 1;
    } else if (prefixIndex === 0) {
      patternTable[suffixIndex] = 0;
      suffixIndex += 1;
    } else {
      prefixIndex = patternTable[prefixIndex - 1];
    }
  }

  return patternTable;
}

/**
 * @param {string} text
 * @param {string} word
 * @return {number}
 */
export default function knuthMorrisPratt(text, word) {
  if (word.length === 0) {
    return 0;
  }

  let textIndex = 0;
  let wordIndex = 0;

  const patternTable = buildPatternTable(word);

  while (textIndex < text.length) {
    if (text[textIndex] === word[wordIndex]) {
      // We've found a match.
      if (wordIndex === word.length - 1) {
        return (textIndex - word.length) + 1;
      }
      wordIndex += 1;
      textIndex += 1;
    } else if (wordIndex > 0) {
      wordIndex = patternTable[wordIndex - 1];
    } else {
      wordIndex = 0;
      textIndex += 1;
    }
  }

  return -1;
}
```

