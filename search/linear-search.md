# 线性查找

在计算机科学中，线性查找或顺序查找是在列表中查找目标值的一种方法。它按顺序检查列表中的每个元素，直到找到匹配的元素或搜索完所有元素为止。线性搜索最差的时间为 `n` 次比较，其中 `n` 是列表的长度。

![img](https://img.imyangyong.com/blog/2020-07-10%2014-28-10.gif)

## 时间复杂度

`O(n)` - 因为在最差的情况下，每个元素都会进行比较。 

## 代码

```javascript
import Comparator from myComparatorUtil;
// https://github.com/AngusYang9/javascript-algorithms/blob/master/src/utils/comparator/Comparator.js

/**
 * Linear search implementation.
 *
 * @param {*[]} array
 * @param {*} seekElement
 * @param {function(a, b)} [comparatorCallback]
 * @return {number[]}
 */
export default function linearSearch(array, seekElement, comparatorCallback) {
  const comparator = new Comparator(comparatorCallback);
  const foundIndices = [];

  array.forEach((element, index) => {
    if (comparator.equal(element, seekElement)) {
      foundIndices.push(index);
    }
  });

  return foundIndices;
}
```

