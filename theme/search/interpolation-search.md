# 插值查找

**插值查找** 是利用 `插值公式` 来计算猜测目标元素在有序数组中键值 (索引) 可能的位置。搜索方式与[二分查找](theme/search/binary-search.html)相同。

插值查找是一个改进的二分查找。二分查找总是到中间的元素去检查。然而，插值查找可以根据所查找键的值定位不同的位置。例如，如果键的值更接近最后一个元素，插值查找很可能从末端开始查找。

与二分查找差别在：

- 二分查找法：猜测键值在中间位置

- 插值查找法：用插值公式计算键值位置

那么时间复杂度：

- 线性查找：`O(n)`
- 跳跃查找： `O(√n)`

- 二分查找：`O(log(n))`
- 插值查找：`O(log(log(n)))`

## 算法

为了找到要目标的位置，使用如下公式，即 **插值公式**：

```javascript
// The idea of formula is to return higher value of pos
// when element to be searched is closer to arr[hi]. And
// smaller value when closer to arr[lo]
pos = lo + ((x - arr[lo]) * (hi - lo) / (arr[hi] - arr[Lo]))

arr[] - Array where elements need to be searched
x - Element to be searched
lo - Starting index in arr[]
hi - Ending index in arr[]
```

## 时间复杂度

`O(log(log(n)))`

## 代码

```javascript
/**
 * Interpolation search implementation.
 *
 * @param {*[]} sortedArray - sorted array with uniformly distributed values
 * @param {*} seekElement
 * @return {number}
 */
export default function interpolationSearch(sortedArray, seekElement) {
  let leftIndex = 0;
  let rightIndex = sortedArray.length - 1;

  while (leftIndex <= rightIndex) {
    const rangeDelta = sortedArray[rightIndex] - sortedArray[leftIndex];
    const indexDelta = rightIndex - leftIndex;
    const valueDelta = seekElement - sortedArray[leftIndex];

    // If valueDelta is less then zero it means that there is no seek element
    // exists in array since the lowest element from the range is already higher
    // then seek element.
    if (valueDelta < 0) {
      return -1;
    }

    // If range delta is zero then subarray contains all the same numbers
    // and thus there is nothing to search for unless this range is all
    // consists of seek number.
    if (!rangeDelta) {
      // By doing this we're also avoiding division by zero while
      // calculating the middleIndex later.
      return sortedArray[leftIndex] === seekElement ? leftIndex : -1;
    }

    // Do interpolation of the middle index.
    const middleIndex = leftIndex + Math.floor(valueDelta * indexDelta / rangeDelta);

    // If we've found the element just return its position.
    if (sortedArray[middleIndex] === seekElement) {
      return middleIndex;
    }

    // Decide which half to choose for seeking next: left or right one.
    if (sortedArray[middleIndex] < seekElement) {
      // Go to the right half of the array.
      leftIndex = middleIndex + 1;
    } else {
      // Go to the left half of the array.
      rightIndex = middleIndex - 1;
    }
  }

  return -1;
}
```

