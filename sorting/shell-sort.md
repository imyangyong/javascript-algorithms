# 希尔排序

**希尔排序**（Shellsort），也称**递减增量排序算法**，是[插入排序](/sorting/insertion-sort.html)的一种更高效的改进版本。希尔排序是[非稳定排序算法](https://baike.baidu.com/item/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95%E7%A8%B3%E5%AE%9A%E6%80%A7)。

希尔排序是把元素按下标的一定增量分组，对每组使用直接插入排序算法排序；随着增量逐渐减少，每组包含的元素越来越多，当增量减至1时，整个列表恰被分成一组，最后执行一次插入排序算法便终止。

![img](http://img.90paw.com/AngusYang9/2020-07-12%2001-41-05.gif)

## 希尔算法如何实现

为了便于理解，我们取间隔为 `4`。创建一个包含间隔为 `4` 个位置的所有值的虚拟子列表。

那么这些列表值为 `{35, 14}`, `{33, 19}`, `{42, 27}` 和 `{10, 44}`。

![img](http://img.90paw.com/AngusYang9/2020-07-12%2011-23-44.png)

我们比较每个子列表中的值，如果需要则在原始列表中交换它们。在这一步之后，新的数组应该是这样的：

![img](http://img.90paw.com/AngusYang9/2020-07-12%2011-30-15.png)

然后，我们取区间为 `2`，这个间隔生成两个子列表：

- `{14, 27, 35, 42}`, `{19, 10, 33, 44}`

![img](http://img.90paw.com/AngusYang9/2020-07-12%2011-38-00.png)

继续比较每个子列表中的值，如需要则交换。那么现在数组应该是这样：

<img src="http://img.90paw.com/AngusYang9/2020-07-12%2011-57-06.png" alt="img" style="zoom: 40%;" />

最后，我们使用 `1` 的间隔对数组的其余部分进行排序。希尔排序使用插入排序对数组进行排序。

![img](http://img.90paw.com/AngusYang9/2020-07-12%2012-06-39.png)

> 这里的 10 和 19 初始顺序有误，但不影响理解。

## 时间复杂度

- 最优：`O(nlog(n))`
- 最差：`O(n(log(n))^2)`

`O(n^(1.3—2))`

## 代码

```javascript
import Sort from '../Sort';
// // https://github.com/AngusYang9/javascript-algorithms/blob/master/src/algorithms/sorting/Sort.js 

export default class ShellSort extends Sort {
  sort(originalArray) {
    // Prevent original array from mutations.
    const array = [...originalArray];

    // Define a gap distance.
    let gap = Math.floor(array.length / 2);

    // Until gap is bigger then zero do elements comparisons and swaps.
    while (gap > 0) {
      // Go and compare all distant element pairs.
      for (let i = 0; i < (array.length - gap); i += 1) {
        let currentIndex = i;
        let gapShiftedIndex = i + gap;

        while (currentIndex >= 0) {
          // Call visiting callback.
          this.callbacks.visitingCallback(array[currentIndex]);

          // Compare and swap array elements if needed.
          if (this.comparator.lessThan(array[gapShiftedIndex], array[currentIndex])) {
            const tmp = array[currentIndex];
            array[currentIndex] = array[gapShiftedIndex];
            array[gapShiftedIndex] = tmp;
          }

          gapShiftedIndex = currentIndex;
          currentIndex -= gap;
        }
      }

      // Shrink the gap.
      gap = Math.floor(gap / 2);
    }

    // Return sorted copy of an original array.
    return array;
  }
}
```

