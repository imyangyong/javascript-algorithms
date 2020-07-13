# 归并排序

在计算机科学中，归并排序是一种高效的、通用的、基于比较的[稳定排序](https://baike.baidu.com/item/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95%E7%A8%B3%E5%AE%9A%E6%80%A7)算法。

归并排序是一种分而治之的算法，由约翰·冯·诺伊曼在1945年发明。举个例子。首先将列表划分为最小的单元（ 1 个元素），然后将每个列表与相邻列表进行比较，然后对相邻的两个列表进行排序和合并。

![img](http://img.90paw.com/AngusYang9/2020-07-11%2021-32-52.gif)

下面是递归合并排序算法，用于对 7 个整数值的数组进行排序。这些是模仿合并排序（自上而下）所要采取的步骤。

![img](http://img.90paw.com/AngusYang9/2020-07-11%2021-59-10.png)

## 时间复杂度

`O(nlog(n))`

## 代码

```javascript
import Sort from '../Sort';
// https://github.com/AngusYang9/javascript-algorithms/blob/master/src/algorithms/sorting/Sort.js

export default class MergeSort extends Sort {
  sort(originalArray) {
    // Call visiting callback.
    this.callbacks.visitingCallback(null);

    // If array is empty or consists of one element then return this array since it is sorted.
    if (originalArray.length <= 1) {
      return originalArray;
    }

    // Split array on two halves.
    const middleIndex = Math.floor(originalArray.length / 2);
    const leftArray = originalArray.slice(0, middleIndex);
    const rightArray = originalArray.slice(middleIndex, originalArray.length);

    // Sort two halves of split array
    const leftSortedArray = this.sort(leftArray);
    const rightSortedArray = this.sort(rightArray);

    // Merge two sorted arrays into one.
    return this.mergeSortedArrays(leftSortedArray, rightSortedArray);
  }

  mergeSortedArrays(leftArray, rightArray) {
    let sortedArray = [];

    // In case if arrays are not of size 1.
    while (leftArray.length && rightArray.length) {
      let minimumElement = null;

      // Find minimum element of two arrays.
      if (this.comparator.lessThanOrEqual(leftArray[0], rightArray[0])) {
        minimumElement = leftArray.shift();
      } else {
        minimumElement = rightArray.shift();
      }

      // Call visiting callback.
      this.callbacks.visitingCallback(minimumElement);

      // Push the minimum element of two arrays to the sorted array.
      sortedArray.push(minimumElement);
    }

    // If one of two array still have elements we need to just concatenate
    // this element to the sorted array since it is already sorted.
    if (leftArray.length) {
      sortedArray = sortedArray.concat(leftArray);
    }

    if (rightArray.length) {
      sortedArray = sortedArray.concat(rightArray);
    }

    return sortedArray;
  }
}
```

