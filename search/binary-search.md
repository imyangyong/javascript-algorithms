# 二分查找

在计算机科学中，**二分查找**，也称为**折半搜索算法**，**对数搜索算法**，是一种搜索算法，查找目标值在 **有序数组** 中的位置。

二分查找将目标值与数组的中间元素进行比较。如果它们不相等，剔除不符合的一半，继续在剩下的一半上寻找，直到成功。如果查找结束时剩下的一半为空，则目标不在数组中。

这种搜索算法每一次比较都使搜索范围缩小一半。

![img](https://img.imyangyong.com/blog/2020-07-10%2016-45-26.png)

## 时间复杂度

`O(log(n))` - 每一次比较范围缩小一半

## 代码

```javascript
import Comparator from myComparatorUtil;
// https://github.com/AngusYang9/javascript-algorithms/blob/master/src/utils/comparator/Comparator.js

/**
 * Binary search implementation.
 *
 * @param {*[]} sortedArray
 * @param {*} seekElement
 * @param {function(a, b)} [comparatorCallback]
 * @return {number}
 */

export default function binarySearch(sortedArray, seekElement, comparatorCallback) {
  // Let's create comparator from the comparatorCallback function.
  // Comparator object will give us common comparison methods like equal() and lessThen().
  const comparator = new Comparator(comparatorCallback);

  // These two indices will contain current array (sub-array) boundaries.
  let startIndex = 0;
  let endIndex = sortedArray.length - 1;

  // Let's continue to split array until boundaries are collapsed
  // and there is nothing to split anymore.
  while (startIndex <= endIndex) {
    // Let's calculate the index of the middle element.
    const middleIndex = startIndex + Math.floor((endIndex - startIndex) / 2);

    // If we've found the element just return its position.
    if (comparator.equal(sortedArray[middleIndex], seekElement)) {
      return middleIndex;
    }

    // Decide which half to choose for seeking next: left or right one.
    if (comparator.lessThan(sortedArray[middleIndex], seekElement)) {
      // Go to the right half of the array.
      startIndex = middleIndex + 1;
    } else {
      // Go to the left half of the array.
      endIndex = middleIndex - 1;
    }
  }

  // Return -1 if we have not found anything.
  return -1;
}
```

