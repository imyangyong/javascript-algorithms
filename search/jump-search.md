# 跳跃查找

类似[二分查找](theme/search/binary-search.html)，跳跃查找（或块查找）是一个对有序的数组，查找匹配值的搜索算法。基本思想是通过固定的步长向前跳跃或跳过一些元素来代替搜索所有元素来检查更少的元素，那么这比线性搜索效率更高。

例如，假设我们有一个大小为 `n` 的数组 `arr[]` 和大小为 `m` 的块（要跳转）。接着，我们搜索 `arr[0]`，`arr[m]`，`arr[2 * m]`，`...`，`arr[k * m]`。一旦我们找到了区间 `arr[k * m] < x < arr[(k+1) * m]`，我们从索引 `k * m` 执行一个线性搜索操作来查找元素 `x`。

**要跳过的最佳块大小是多少呢？** 在最差的情况下，我们必须进行 `n/m` 次跳跃，如果最后检查的值大于要搜索的元素，我们会对线性搜索多进行 `m - 1` 次比较。因此，最差情况下的比较总次数是 `((n/m) + m - 1)` 。当 m =$$ \sqrt{n} $$  时，函数 `((n/m) + m - 1)` 的值最小。因此，最佳跳跃步长为  m =$$ \sqrt{n} $$ 。

## 时间复杂度

O($$ \sqrt{n} $$) - 因为我们是用大小为 $$ \sqrt{n} $$  的块来搜索的。

## 代码

```javascript
import Comparator from myComparatorUtil;
// https://github.com/imyangyong/javascript-algorithms/blob/master/src/utils/comparator/Comparator.js

/**
 * Jump (block) search implementation.
 *
 * @param {*[]} sortedArray
 * @param {*} seekElement
 * @param {function(a, b)} [comparatorCallback]
 * @return {number}
 */
export default function jumpSearch(sortedArray, seekElement, comparatorCallback) {
  const comparator = new Comparator(comparatorCallback);
  const arraySize = sortedArray.length;

  if (!arraySize) {
    // We can't find anything in empty array.
    return -1;
  }

  // Calculate optimal jump size.
  // Total number of comparisons in the worst case will be ((arraySize/jumpSize) + jumpSize - 1).
  // The value of the function ((arraySize/jumpSize) + jumpSize - 1) will be minimum
  // when jumpSize = √array.length.
  const jumpSize = Math.floor(Math.sqrt(arraySize));

  // Find the block where the seekElement belong to.
  let blockStart = 0;
  let blockEnd = jumpSize;
  while (comparator.greaterThan(seekElement, sortedArray[Math.min(blockEnd, arraySize) - 1])) {
    // Jump to the next block.
    blockStart = blockEnd;
    blockEnd += jumpSize;

    // If our next block is out of array then we couldn't found the element.
    if (blockStart > arraySize) {
      return -1;
    }
  }

  // Do linear search for seekElement in subarray starting from blockStart.
  let currentIndex = blockStart;
  while (currentIndex < Math.min(blockEnd, arraySize)) {
    if (comparator.equal(sortedArray[currentIndex], seekElement)) {
      return currentIndex;
    }

    currentIndex += 1;
  }

  return -1;
}
```

`$$ \sqrt{n} $$`： 根号 n
