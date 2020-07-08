# 最短公共父序列

与 [最长公共子序列（LCS）](theme/sets/longest-common-subsequence.html) 相反。

两个序列 `X` 和 `Y` 的最短公共父序列（SCS）是指，子序列为 `X` 和 `Y` 的最短序列。

换句话说，假设我们有两个字符串 str1 和 str2 ，找出有 str1 和 str2 作为子序列的最短字符串。

这是一个与 最长公共子序列（LCS）密切相关的问题。

## 示例

```bash
Input:   str1 = "geek",  str2 = "eke"
Output: "geeke"

Input:   str1 = "AGGTAB",  str2 = "GXTXAYB"
Output:  "AGXGTXAYB"
```

## 代码

```javascript
import longestCommonSubsequence from 最长公共子序列

/**
 * @param {string[]} set1
 * @param {string[]} set2
 * @return {string[]}
 */

export default function shortestCommonSupersequence(set1, set2) {
  // Let's first find the longest common subsequence of two sets.
  const lcs = longestCommonSubsequence(set1, set2);

  // If LCS is empty then the shortest common supersequence would be just
  // concatenation of two sequences.
  if (lcs.length === 1 && lcs[0] === '') {
    return set1.concat(set2);
  }

  // Now let's add elements of set1 and set2 in order before/inside/after the LCS.
  let supersequence = [];

  let setIndex1 = 0;
  let setIndex2 = 0;
  let lcsIndex = 0;
  let setOnHold1 = false;
  let setOnHold2 = false;

  while (lcsIndex < lcs.length) {
    // Add elements of the first set to supersequence in correct order.
    if (setIndex1 < set1.length) {
      if (!setOnHold1 && set1[setIndex1] !== lcs[lcsIndex]) {
        supersequence.push(set1[setIndex1]);
        setIndex1 += 1;
      } else {
        setOnHold1 = true;
      }
    }

    // Add elements of the second set to supersequence in correct order.
    if (setIndex2 < set2.length) {
      if (!setOnHold2 && set2[setIndex2] !== lcs[lcsIndex]) {
        supersequence.push(set2[setIndex2]);
        setIndex2 += 1;
      } else {
        setOnHold2 = true;
      }
    }

    // Add LCS element to the supersequence in correct order.
    if (setOnHold1 && setOnHold2) {
      supersequence.push(lcs[lcsIndex]);
      lcsIndex += 1;
      setIndex1 += 1;
      setIndex2 += 1;
      setOnHold1 = false;
      setOnHold2 = false;
    }
  }

  // Attach set1 leftovers.
  if (setIndex1 < set1.length) {
    supersequence = supersequence.concat(set1.slice(setIndex1));
  }

  // Attach set2 leftovers.
  if (setIndex2 < set2.length) {
    supersequence = supersequence.concat(set2.slice(setIndex2));
  }

  return supersequence;
}
```

