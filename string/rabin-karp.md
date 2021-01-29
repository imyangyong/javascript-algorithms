# Rabin–Karp 算法

在计算机科学中，Rabin - Karp算法 或 Karp - Rabin算法是由 Richard M. Karp 和 Michael O. Rabin (1987) 创建的字符串搜索算法，它使用 [哈希函数](https://zh.wikipedia.org/wiki/%E6%95%A3%E5%88%97%E5%87%BD%E6%95%B8) 查找在文本中的 `单个模式` 的子串。

## 算法

Rabin-Karp 算法通过使用`哈希函数`来加速对文本中子字符串的模式是否相等的测试。哈希函数是将每个字符串转换为数值的函数，称为其哈希值，比如，`hash('hello') = 5`。该算法利用了这样一个点：**如果两个字符串相等，那么它们的哈希值也相等**。因此，字符串匹配(几乎)被简化为计算搜索模式的哈希值，然后查找具有该哈希值的子字符串。

然而，这种方法有两个问题。首先，因为有这么多不同的字符串和这么少的哈希值，一些不同的字符串将有相同的哈希值。如果哈希值匹配，那么模式和子字符串可能不匹配，因此，搜索模式和子字符串的潜在匹配必须通过比较来确定。对于较长的子字符串，这种可能会花费很长时间。幸运的是，对于合理的字符串，一个好的哈希函数通常不会有太多冲突，所以预期的搜索时间是可以接受的。

## 使用哈希函数

Rabin-Karp 算法性能的关键是有效计算文本连续子字符串的哈希值。[Rabin指纹](https://zh.wikipedia.org/wiki/Rabin%E6%8C%87%E7%BA%B9?wprov=srpw1_1)是一种流行而有效的滚动哈希函数。

在这个例子中描述的多项式哈希函数不是 Rabin指纹，但它同样有效。它将每个子字符串都视为以某种基数表示的数字，该基数通常是一个较大的素数。

## 时间复杂度

对于长度为 `n` 的文本和长度为 `m` 的 `p` 种组合模式，其在 `O(p)` 空间上的平均和最佳运行时间为 `O(n + m)`，而最差情况运行时间为 `O(n * m)`。

## 应用

该算法的一个实际应用是检测抄袭。在给定原材料的情况下，该算法可以在论文中快速搜索原材料中的句子实例，忽略大小写、标点符号等细节。由于搜索的字符串数量太多，单字符串搜索算法是不切实际的。

## 代码

```javascript
import PolynomialHash from myUtils;
// https://github.com/imyangyong/javascript-algorithms/blob/master/src/algorithms/cryptography/polynomial-hash/PolynomialHash.js

/**
 * @param {string} text - Text that may contain the searchable word.
 * @param {string} word - Word that is being searched in text.
 * @return {number} - Position of the word in text.
 */
export default function rabinKarp(text, word) {
  const hasher = new PolynomialHash();

  // Calculate word hash that we will use for comparison with other substring hashes.
  const wordHash = hasher.hash(word);

  let prevFrame = null;
  let currentFrameHash = null;

  // Go through all substring of the text that may match.
  for (let charIndex = 0; charIndex <= (text.length - word.length); charIndex += 1) {
    const currentFrame = text.substring(charIndex, charIndex + word.length);

    // Calculate the hash of current substring.
    if (currentFrameHash === null) {
      currentFrameHash = hasher.hash(currentFrame);
    } else {
      currentFrameHash = hasher.roll(currentFrameHash, prevFrame, currentFrame);
    }

    prevFrame = currentFrame;

    // Compare the hash of current substring and seeking string.
    // In case if hashes match let's make sure that substrings are equal.
    // In case of hash collision the strings may not be equal.
    if (
      wordHash === currentFrameHash
      && text.substr(charIndex, word.length) === word
    ) {
      return charIndex;
    }
  }

  return -1;
}
```

