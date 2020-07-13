# 选择排序

选择排序（Selection sort）是一种简单直观的排序算法。它的工作原理是：第一次从待排序的数据元素中选出最小（或最大）的一个元素，存放在序列的起始位置，然后再从剩余的未排序元素中寻找到最小（大）元素，然后放到已排序的序列的末尾。以此类推，直到全部待排序的数据元素的个数为零。选择排序是不稳定的排序方法。

![img](http://img.90paw.com/AngusYang9/2020-07-11%2017-49-38.gif)

![img](http://img.90paw.com/AngusYang9/2020-07-11%2017-52-28.gif)

## 时间复杂度

`O(n^2)`

## 代码

```javascript
import Sort from '../Sort';
// https://github.com/AngusYang9/javascript-algorithms/blob/master/src/algorithms/sorting/Sort.js

export default class SelectionSort extends Sort {
  sort(originalArray) {
    // Clone original array to prevent its modification.
    const array = [...originalArray];

    for (let i = 0; i < array.length - 1; i += 1) {
      let minIndex = i;

      // Call visiting callback.
      this.callbacks.visitingCallback(array[i]);

      // Find minimum element in the rest of array.
      for (let j = i + 1; j < array.length; j += 1) {
        // Call visiting callback.
        this.callbacks.visitingCallback(array[j]);

        if (this.comparator.lessThan(array[j], array[minIndex])) {
          minIndex = j;
        }
      }

      // If new minimum element has been found then swap it with current i-th element.
      if (minIndex !== i) {
        [array[i], array[minIndex]] = [array[minIndex], array[i]];
      }
    }

    return array;
  }
}
```

