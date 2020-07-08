# 最长递增子序列

最长递增子序列问题是寻找给定序列的子序列，其中子序列的元素按从低到高的顺序排列，且子序列尽可能长。

这个子序列不一定是连续的，或者是唯一的。

## 时间复杂度

最长递增子序列问题在 `O(n logn)` 复杂度下是可解的，其中 `n` 表示输入序列的长度。

动态规划方法的复杂度为 `O(n * n)`。

## 示例

在[范德科皮特序列](https://zh.wikipedia.org/wiki/%E8%8C%83%E5%BE%B7%E7%A7%91%E7%9A%AE%E7%89%B9%E5%BA%8F%E5%88%97)的前 16 项中：

```bash
0, 8, 4, 12, 2, 10, 6, 14, 1, 9, 5, 13, 3, 11, 7, 15
```

最长递增子序列是：

```bash
0, 2, 6, 9, 11, 15.
```

这个子序列的长度是 6。这个序列中最长递增子序列不是唯一的：

```bash
0, 4, 6, 9, 11, 15 or
0, 2, 6, 9, 13, 15 or
0, 4, 6, 9, 13, 15
```

## 代码

```javascript
/**
 * Dynamic programming approach to find longest increasing subsequence.
 * Complexity: O(n * n)
 *
 * @param {number[]} sequence
 * @return {number}
 */
export default function dpLongestIncreasingSubsequence(sequence) {
  // Create array with longest increasing substrings length and
  // fill it with 1-s that would mean that each element of the sequence
  // is itself a minimum increasing subsequence.
  const lengthsArray = Array(sequence.length).fill(1);

  let previousElementIndex = 0;
  let currentElementIndex = 1;

  while (currentElementIndex < sequence.length) {
    if (sequence[previousElementIndex] < sequence[currentElementIndex]) {
      // If current element is bigger then the previous one then
      // current element is a part of increasing subsequence which
      // length is by one bigger then the length of increasing subsequence
      // for previous element.
      const newLength = lengthsArray[previousElementIndex] + 1;
      if (newLength > lengthsArray[currentElementIndex]) {
        // Increase only if previous element would give us bigger subsequence length
        // then we already have for current element.
        lengthsArray[currentElementIndex] = newLength;
      }
    }

    // Move previous element index right.
    previousElementIndex += 1;

    // If previous element index equals to current element index then
    // shift current element right and reset previous element index to zero.
    if (previousElementIndex === currentElementIndex) {
      currentElementIndex += 1;
      previousElementIndex = 0;
    }
  }

  // Find the biggest element in lengthsArray.
  // This number is the biggest length of increasing subsequence.
  let longestIncreasingLength = 0;

  for (let i = 0; i < lengthsArray.length; i += 1) {
    if (lengthsArray[i] > longestIncreasingLength) {
      longestIncreasingLength = lengthsArray[i];
    }
  }

  return longestIncreasingLength;
}
```



