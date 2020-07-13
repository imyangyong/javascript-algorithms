# 计数排序

**计数排序（Counting sort）**是一种稳定的线性时间 **整数** 排序算法。该算法于1954年由 Harold H. Seward 提出。计数排序使用一个额外的数组 `C`，`C` 的索引值为待排序数组的值，`C `的元素值为待排序数组中值等于该索引的个数。然后根据数组 `C` 来将 `A` 中的元素排到正确的位置。

计数排序的运行时间在列表项数和最大值与最小值差值范围之间是线性的，因此只适用于值变化不明显大于项数的情况下直接使用。然而，它经常被用作[基数排序](/sorting/radix-sort.html)算法的子程序，可以更有效地处理较大范围的值。

由于将数组元素值作为计数数组的下标(索引)，所以 **当数组元素的数值范围非常小时，计数排序的效果最好。** 注意！这里是指数值范围，不是最大值。

## 算法

### 第一步

在第一步中，我们计算数组 `A` 的所有元素的计数，然后将结果存储在计数数组 `C` 中。

![img](http://img.90paw.com/AngusYang9/2020-07-12%2018-17-21.gif)

### 第二步

在第二步中，我们计算数组 `A` 中有多少小于或等于给定索引的元素。

![img](http://img.90paw.com/AngusYang9/2020-07-12%2018-27-33.png)

### 第三步

在这一步中，我们遍历原数组 `A` 的元素，在计数数组 `C` 中找到与之对应的索引值，拿到该索引元素值作为结果数组 `B` 的坐标，把原数组中的元素放入 `B` 的这个坐标位置。 

![img](http://img.90paw.com/AngusYang9/2020-07-12%2020-02-04.gif)

## 时间复杂度

`O(n + r)` - r 为数组中的最大值与最小值差值

## 代码

```javascript
import Sort from '../Sort';
// https://github.com/AngusYang9/javascript-algorithms/blob/master/src/algorithms/sorting/Sort.js 

export default class CountingSort extends Sort {
  /**
   * @param {number[]} originalArray
   * @param {number} [smallestElement]
   * @param {number} [biggestElement]
   */
  sort(originalArray, smallestElement = undefined, biggestElement = undefined) {
    // Init biggest and smallest elements in array in order to build number bucket array later.
    let detectedSmallestElement = smallestElement || 0;
    let detectedBiggestElement = biggestElement || 0;

    if (smallestElement === undefined || biggestElement === undefined) {
      originalArray.forEach((element) => {
        // Visit element.
        this.callbacks.visitingCallback(element);

        // Detect biggest element.
        if (this.comparator.greaterThan(element, detectedBiggestElement)) {
          detectedBiggestElement = element;
        }

        // Detect smallest element.
        if (this.comparator.lessThan(element, detectedSmallestElement)) {
          detectedSmallestElement = element;
        }
      });
    }

    // Init buckets array.
    // This array will hold frequency of each number from originalArray.
    const buckets = Array(detectedBiggestElement - detectedSmallestElement + 1).fill(0);

    originalArray.forEach((element) => {
      // Visit element.
      this.callbacks.visitingCallback(element);

      buckets[element - detectedSmallestElement] += 1;
    });

    // Add previous frequencies to the current one for each number in bucket
    // to detect how many numbers less then current one should be standing to
    // the left of current one.
    for (let bucketIndex = 1; bucketIndex < buckets.length; bucketIndex += 1) {
      buckets[bucketIndex] += buckets[bucketIndex - 1];
    }

    // Now let's shift frequencies to the right so that they show correct numbers.
    // I.e. if we won't shift right than the value of buckets[5] will display how many
    // elements less than 5 should be placed to the left of 5 in sorted array
    // INCLUDING 5th. After shifting though this number will not include 5th anymore.
    buckets.pop();
    buckets.unshift(0);

    // Now let's assemble sorted array.
    const sortedArray = Array(originalArray.length).fill(null);
    for (let elementIndex = 0; elementIndex < originalArray.length; elementIndex += 1) {
      // Get the element that we want to put into correct sorted position.
      const element = originalArray[elementIndex];

      // Visit element.
      this.callbacks.visitingCallback(element);

      // Get correct position of this element in sorted array.
      const elementSortedPosition = buckets[element - detectedSmallestElement];

      // Put element into correct position in sorted array.
      sortedArray[elementSortedPosition] = element;

      // Increase position of current element in the bucket for future correct placements.
      buckets[element - detectedSmallestElement] += 1;
    }

    // Return sorted array.
    return sortedArray;
  }
}
```



