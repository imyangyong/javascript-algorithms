# 组合

当顺序无关时，它是一个**组合**；当顺序有关时，那就是**排列**。

“我的水果沙拉是苹果、葡萄和香蕉的混合物“。我们不在乎水果的顺序，它们也可以是“香蕉、葡萄和苹果”或“葡萄、苹果和香蕉”，这是同一种水果沙拉。

## 无重复组合

彩票就是这样运作的。一次抽一个号码，如果我们有幸运数字（不管是什么顺序），我们就赢了！

无重复：如彩票号码`（2,14,15,27,30,33）`

### 组合的数量

![img](http://img.90paw.com/AngusYang9/2020-07-08%2016-19-45.png)

其中 `n` 是元素的数量，我们选择 `r` 个，没有重复，顺序无关。

它通常被称为 “n 选 r”（如 “16选3”）。也被称为二项式系数。

## 重复组合

允许重复：例如你口袋里的硬币（5,5,5,10,10）。

假设说冰淇淋有五种口味：香蕉、巧克力、柠檬、草莓和香草。

我们可以吃三个，会有多少种类组合？

让我们用字母来表示口味：`{b，c，l，s，v}`。示例选择包括：

- `{c, c, c}` (3个巧克力)
- `{b, l, v}` (香蕉、柠檬和香草各一份)
- `{b, v, v}` (一份香蕉，两份香草)

### 组合的数量

![img](http://img.90paw.com/AngusYang9/2020-07-08%2016-33-41.png)

其中 `n` 是元素的数量，我们从中选择 `r` 个。允许重复，顺序无关。

## 代码

### 1. 无重复组合

```javascript
/**
 * @param {*[]} comboOptions
 * @param {number} comboLength
 * @return {*[]}
 */
export default function combineWithoutRepetitions(comboOptions, comboLength) {
  // If the length of the combination is 1 then each element of the original array
  // is a combination itself.
  if (comboLength === 1) {
    return comboOptions.map(comboOption => [comboOption]);
  }

  // Init combinations array.
  const combos = [];

  // Extract characters one by one and concatenate them to combinations of smaller lengths.
  // We need to extract them because we don't want to have repetitions after concatenation.
  comboOptions.forEach((currentOption, optionIndex) => {
    // Generate combinations of smaller size.
    const smallerCombos = combineWithoutRepetitions(
      comboOptions.slice(optionIndex + 1),
      comboLength - 1,
    );

    // Concatenate currentOption with all combinations of smaller size.
    smallerCombos.forEach((smallerCombo) => {
      combos.push([currentOption].concat(smallerCombo));
    });
  });

  return combos;
}
```

### 2. 重复组合

```javascript
/**
 * @param {*[]} comboOptions
 * @param {number} comboLength
 * @return {*[]}
 */
export default function combineWithRepetitions(comboOptions, comboLength) {
  // If the length of the combination is 1 then each element of the original array
  // is a combination itself.
  if (comboLength === 1) {
    return comboOptions.map(comboOption => [comboOption]);
  }

  // Init combinations array.
  const combos = [];

  // Remember characters one by one and concatenate them to combinations of smaller lengths.
  // We don't extract elements here because the repetitions are allowed.
  comboOptions.forEach((currentOption, optionIndex) => {
    // Generate combinations of smaller size.
    const smallerCombos = combineWithRepetitions(
      comboOptions.slice(optionIndex),
      comboLength - 1,
    );

    // Concatenate currentOption with all combinations of smaller size.
    smallerCombos.forEach((smallerCombo) => {
      combos.push([currentOption].concat(smallerCombo));
    });
  });

  return combos;
}
```

