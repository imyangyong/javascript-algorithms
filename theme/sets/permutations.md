# 排列

当顺序无关时，它是一个**组合**；当顺序有关时，那就是**排列**。

保险箱的密码是 472，我们关心的是顺序。724 不行，247 也不行。必须是 4-7-2。

## 无重复排列

排列，也称为“排列数”或“顺序”，是对一个有序列表 `S` 的元素进行重新排列，使其与 `S` 本身一一对应。

下面是字符串 `ABC` 的排列。

```bash
ABC ACB BAC BCA CBA CAB
```

### 组合的数量

```javascript
n * (n-1) * (n -2) * ... * 1 = n!
```

## 重复排列

当允许重复时，我们就用重复排列。比如密码锁可以是 `333`。

![img](http://img.90paw.com/AngusYang9/2020-07-08%2016-11-12.png)

### 组合的数量

```javascript
n * n * n ... (r times) = n^r
```

## 代码

### 1. 无重复排列

```javascript
/**
 * @param {*[]} permutationOptions
 * @return {*[]}
 */
export default function permutateWithoutRepetitions(permutationOptions) {
  if (permutationOptions.length === 1) {
    return [permutationOptions];
  }

  // Init permutations array.
  const permutations = [];

  // Get all permutations for permutationOptions excluding the first element.
  const smallerPermutations = permutateWithoutRepetitions(permutationOptions.slice(1));

  // Insert first option into every possible position of every smaller permutation.
  const firstOption = permutationOptions[0];

  for (let permIndex = 0; permIndex < smallerPermutations.length; permIndex += 1) {
    const smallerPermutation = smallerPermutations[permIndex];

    // Insert first option into every possible position of smallerPermutation.
    for (let positionIndex = 0; positionIndex <= smallerPermutation.length; positionIndex += 1) {
      const permutationPrefix = smallerPermutation.slice(0, positionIndex);
      const permutationSuffix = smallerPermutation.slice(positionIndex);
      permutations.push(permutationPrefix.concat([firstOption], permutationSuffix));
    }
  }

  return permutations;
}
```

### 2. 重复排列

```javascript
/**
 * @param {*[]} permutationOptions
 * @param {number} permutationLength
 * @return {*[]}
 */
export default function permutateWithRepetitions(
permutationOptions,
 permutationLength = permutationOptions.length,
) {
  if (permutationLength === 1) {
    return permutationOptions.map(permutationOption => [permutationOption]);
  }

  // Init permutations array.
  const permutations = [];

  // Get smaller permutations.
  const smallerPermutations = permutateWithRepetitions(
    permutationOptions,
    permutationLength - 1,
  );

  // Go through all options and join it to the smaller permutations.
  permutationOptions.forEach((currentOption) => {
    smallerPermutations.forEach((smallerPermutation) => {
      permutations.push([currentOption].concat(smallerPermutation));
    });
  });

  return permutations;
}
```

