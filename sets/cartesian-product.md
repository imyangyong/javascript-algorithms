# 笛卡尔积

在集合论中，笛卡尔积是一种数学运算，它从多个集合中生成一个集合（或乘积集或简单的乘积）。即对于集合 `A` 和 `B`，笛卡尔积 `A×B` 是所有有序对 `(A, B)` 的集合，其中 A∈A，B∈B。

`A={x,y,z}` 和 `B={1,2,3}` 的笛卡尔积 `AxB`：

![img](http://img.90paw.com/AngusYang9/2020-07-08%2013-37-12.png)

## 代码

```javascript
/**
 * Generates Cartesian Product of two sets.
 * @param {*[]} setA
 * @param {*[]} setB
 * @return {*[]}
 */
export default function cartesianProduct(setA, setB) {
  // Check if input sets are not empty.
  // Otherwise return null since we can't generate Cartesian Product out of them.
  if (!setA || !setB || !setA.length || !setB.length) {
    return null;
  }

  // Init product set.
  const product = [];

  // Now, let's go through all elements of a first and second set and form all possible pairs.
  for (let indexA = 0; indexA < setA.length; indexA += 1) {
    for (let indexB = 0; indexB < setB.length; indexB += 1) {
      // Add current product pair to the product set.
      product.push([setA[indexA], setB[indexB]]);
    }
  }

  // Return cartesian product set.
  return product;
}
```

