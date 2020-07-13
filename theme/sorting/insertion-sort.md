# 插入排序

插入排序是一种简单的排序算法。对于少量元素的排序，它是一个有效的算法；`但在大型列表上，它的效率远远低于更高级的算法，如快速排序、堆排序或合并排序。`

插入排序的基本思想是将一个记录插入到已经排好序的有序表中，从而一个新的、记录数增 1 的有序表。

![img](http://img.90paw.com/AngusYang9/2020-07-11%2018-15-13.gif)

![img](http://img.90paw.com/AngusYang9/2020-07-11%2018-16-50.gif)

## 时间复杂度

- 最优：`O(n)`
- 一般：`O(n^2)`
- 最差：`O(n^2)`

## 代码

```javascript
import Sort from '../Sort';
// https://github.com/AngusYang9/javascript-algorithms/blob/master/src/algorithms/sorting/Sort.js

export default class InsertionSort extends Sort {
  sort(originalArray) {
    const array = [...originalArray];

    // Go through all array elements...
    for (let i = 0; i < array.length; i += 1) {
      let currentIndex = i;

      // Call visiting callback.
      this.callbacks.visitingCallback(array[i]);

      // Go and check if previous elements and greater then current one.
      // If this is the case then swap that elements.
      while (
        array[currentIndex - 1] !== undefined
        && this.comparator.lessThan(array[currentIndex], array[currentIndex - 1])
      ) {
        // Call visiting callback.
        this.callbacks.visitingCallback(array[currentIndex - 1]);

        // Swap the elements.
        const tmp = array[currentIndex - 1];
        array[currentIndex - 1] = array[currentIndex];
        array[currentIndex] = tmp;

        // Shift current index left.
        currentIndex -= 1;
      }
    }

    return array;
  }
}
```

