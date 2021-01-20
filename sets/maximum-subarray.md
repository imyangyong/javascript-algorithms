# 最大子数列问题

**最大子数列问题** 是在一维数组 `a[1…n]`，查找连续子数组，其总和最大。其中，

![img](https://img.imyangyong.com/blog/2020-07-08%2020-00-01.png)

![img](https://img.imyangyong.com/blog/2020-07-08%2020-00-21.png)

## 示例

列表通常包含正数和负数以及 `0`。例如，对于值 `−2, 1, −3, 4, −1, 2, 1, −5, 4` 的数组，具有最大和的连续子数组为 `4, −1, 2, 1` ，t这个子数列和为 `6`。

## 代码

### 1. BF 算法实现

```javascript
/**
 * Brute Force solution.
 * Complexity: O(n^2)
 *
 * @param {Number[]} inputArray
 * @return {Number[]}
 */
export default function bfMaximumSubarray(inputArray) {
  let maxSubarrayStartIndex = 0;
  let maxSubarrayLength = 0;
  let maxSubarraySum = null;

  for (let startIndex = 0; startIndex < inputArray.length; startIndex += 1) {
    let subarraySum = 0;
    for (let arrLength = 1; arrLength <= (inputArray.length - startIndex); arrLength += 1) {
      subarraySum += inputArray[startIndex + (arrLength - 1)];
      if (maxSubarraySum === null || subarraySum > maxSubarraySum) {
        maxSubarraySum = subarraySum;
        maxSubarrayStartIndex = startIndex;
        maxSubarrayLength = arrLength;
      }
    }
  }

  return inputArray.slice(maxSubarrayStartIndex, maxSubarrayStartIndex + maxSubarrayLength);
}
```

### 2. 动态编程实现

```javascript
/**
 * Dynamic Programming solution.
 * Complexity: O(n)
 *
 * @param {Number[]} inputArray
 * @return {Number[]}
 */
export default function dpMaximumSubarray(inputArray) {
  // We iterate through the inputArray once, using a greedy approach to keep track of the maximum
  // sum we've seen so far and the current sum.
  //
  // The currentSum variable gets reset to 0 every time it drops below 0.
  //
  // The maxSum variable is set to -Infinity so that if all numbers are negative, the highest
  // negative number will constitute the maximum subarray.

  let maxSum = -Infinity;
  let currentSum = 0;

  // We need to keep track of the starting and ending indices that contributed to our maxSum
  // so that we can return the actual subarray. From the beginning let's assume that whole array
  // is contributing to maxSum.
  let maxStartIndex = 0;
  let maxEndIndex = inputArray.length - 1;
  let currentStartIndex = 0;

  inputArray.forEach((currentNumber, currentIndex) => {
    currentSum += currentNumber;

    // Update maxSum and the corresponding indices if we have found a new max.
    if (maxSum < currentSum) {
      maxSum = currentSum;
      maxStartIndex = currentStartIndex;
      maxEndIndex = currentIndex;
    }

    // Reset currentSum and currentStartIndex if currentSum drops below 0.
    if (currentSum < 0) {
      currentSum = 0;
      currentStartIndex = currentIndex + 1;
    }
  });

  return inputArray.slice(maxStartIndex, maxEndIndex + 1);
}
```

