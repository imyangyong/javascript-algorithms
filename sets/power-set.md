# 幂集

集合 `S` 的幂集是集合 `S` 所有子集的集合，包括空集和 `S` 本身。集合 `S` 的幂集表示为 `P(S)`。

例如 {x, y, z}，其子集为：

```bash
{
  {}, // 也表示为空集（∅）或 null 集
  {x},
  {y},
  {z},
  {x, y},
  {x, z},
  {y, z},
  {x, y, z}
}
```

![img](https://img.imyangyong.com/blog/2020-07-08%2014-26-51.png)

下面图示用来说明集合 {x, y, z} 的幂集之间的包含关系：

![img](https://img.imyangyong.com/blog/2020-07-08%2014-31-50.png)

### 子集的数目

如果 `S` 是 `|S| = n` 个元素的有限集，则 `S` 的子集数为 `|P(S)| = 2^n`。

这个结论，也就是 `2^S` 的由来，可以简单地用下面的方法来证明：

> 首先，以任意方式对 `S` 中的元素排序。我们将 `S` 的任意子集写成如下格式 `{γ1, γ2, ..., γn}`，其中`γi , 1 ≤ i ≤ n` ，可取 0 或 1 的值。如果 `yi = 1`，则 `S` 的第 `i` 个元素在子集中；否则，第 `i` 个元素不在子集中。显然，通过这种方式可以构造的不同子集的数量为 `2^n` ，即 `yi ∈ {0, 1}`。

## 算法

### 1. 位操作方案

在 `0` 到 `2^n` 范围内的每一个二进制数字都能满足我们的需要：它通过它的位( `0` 或 `1` )来显示是否包含来自集合的相关元素。例如，对于集合 `{1,2,3}`，二进制数 `0b010` 意味着当前集合只需要包含 `2`。

| `abc` | Subset |             |
| ----- | ------ | ----------- |
| `0`   | `000`  | `{}`        |
| `1`   | `001`  | `{c}`       |
| `2`   | `010`  | `{b}`       |
| `3`   | `011`  | `{c, b}`    |
| `4`   | `100`  | `{a}`       |
| `5`   | `101`  | `{a, c}`    |
| `6`   | `110`  | `{a, b}`    |
| `7`   | `111`  | `{a, b, c}` |

### 2. 回溯方案

在回溯法中，我们不断地尝试将集合中的下一个元素添加到子集中，记住它，然后删除它，然后对下一个元素进行同样的尝试。

## 代码

### 1. 位操作实现

```javascript
/**
 * Find power-set of a set using BITWISE approach.
 *
 * @param {*[]} originalSet
 * @return {*[][]}
 */
export default function bwPowerSet(originalSet) {
  const subSets = [];

  // We will have 2^n possible combinations (where n is a length of original set).
  // It is because for every element of original set we will decide whether to include
  // it or not (2 options for each set element).
  const numberOfCombinations = 2 ** originalSet.length;

  // Each number in binary representation in a range from 0 to 2^n does exactly what we need:
  // it shows by its bits (0 or 1) whether to include related element from the set or not.
  // For example, for the set {1, 2, 3} the binary number of 0b010 would mean that we need to
  // include only "2" to the current set.
  for (let combinationIndex = 0; combinationIndex < numberOfCombinations; combinationIndex += 1) {
    const subSet = [];

    for (let setElementIndex = 0; setElementIndex < originalSet.length; setElementIndex += 1) {
      // Decide whether we need to include current element into the subset or not.
      if (combinationIndex & (1 << setElementIndex)) {
        subSet.push(originalSet[setElementIndex]);
      }
    }

    // Add current subset to the list of all subsets.
    subSets.push(subSet);
  }

  return subSets;
}
```

### 2. 回溯实现

```javascript
/**
 * @param {*[]} originalSet - Original set of elements we're forming power-set of.
 * @param {*[][]} allSubsets - All subsets that have been formed so far.
 * @param {*[]} currentSubSet - Current subset that we're forming at the moment.
 * @param {number} startAt - The position of in original set we're starting to form current subset.
 * @return {*[][]} - All subsets of original set.
 */
function btPowerSetRecursive(originalSet, allSubsets = [[]], currentSubSet = [], startAt = 0) {
  // Let's iterate over originalSet elements that may be added to the subset
  // without having duplicates. The value of startAt prevents adding the duplicates.
  for (let position = startAt; position < originalSet.length; position += 1) {
    // Let's push current element to the subset
    currentSubSet.push(originalSet[position]);

    // Current subset is already valid so let's memorize it.
    // We do array destruction here to save the clone of the currentSubSet.
    // We need to save a clone since the original currentSubSet is going to be
    // mutated in further recursive calls.
    allSubsets.push([...currentSubSet]);

    // Let's try to generate all other subsets for the current subset.
    // We're increasing the position by one to avoid duplicates in subset.
    btPowerSetRecursive(originalSet, allSubsets, currentSubSet, position + 1);

    // BACKTRACK. Exclude last element from the subset and try the next valid one.
    currentSubSet.pop();
  }

  // Return all subsets of a set.
  return allSubsets;
}

/**
 * Find power-set of a set using BACKTRACKING approach.
 *
 * @param {*[]} originalSet
 * @return {*[][]}
 */
export default function btPowerSet(originalSet) {
  return btPowerSetRecursive(originalSet);
}
```

