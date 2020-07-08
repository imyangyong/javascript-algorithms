# 洗牌算法

洗牌算法是一种将 `有限序列` `随机排列` 的算法——简单地说，就是对序列进行洗牌。

该算法有效地将所有元素放入一个 hat 中；它通过从 hat 中随机抽取一个元素来不断地确定下一个元素，直到元素为空。该算法产生一个随机排列：每个排列概率相同。该算法的现代版本是有效的：它所花费的时间与被洗牌的条目数量成比例，并将它们洗牌到位。

## 代码

```javascript
/**
 * @param {*[]} originalArray
 * @return {*[]}
 */
export default function fisherYates(originalArray) {
  // Clone array from preventing original array from modification (for testing purpose).
  const array = originalArray.slice(0);

  for (let i = (array.length - 1); i > 0; i -= 1) {
    const randomIndex = Math.floor(Math.random() * (i + 1));
    [array[i], array[randomIndex]] = [array[randomIndex], array[i]];
  }

  return array;
}
```

