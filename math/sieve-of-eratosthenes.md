# 素数筛

Eratosthenes 筛选法是一种寻找 n 以下所有质数的算法。

它源于 Eratosthenes of Cyrene，一位古希腊数学家。

## 如何实现

1. 创建一个有 `n + 1` 个位置的布尔数组(用于表示从 `0` 到 `n` 的数字)

2. 将数组 `0` 和 `1` 设置为 false，其余设置为 `true`
3. 从位置 `p = 2` (第一个素数)开始
4. 将所有 `p` (即位置 `2 * p`，位置 `3 * p`，位置 `4 * p`…直到数组的末尾)的倍数标记为 `false`

5. 找出数组中位置大于 p 且为 `true` 的第一个位置。如果没有这样的位置，停止。否则，让 p 等于这个新数字(它是下一个质数)，并重复步骤 4

当算法结束时，数组中所有小于 `n` 的质数都为 `true`。

对该算法的一个改进是，在步骤 4 中，从 `p * p` 开始标记 `p` 的倍数，而不是从 `2 * p` 开始标记 `p` 的倍数。之所以有效是因为在那个时候，更小的 `p` 的倍数已经被标记为 `false`。

## Example

![img](https://img.imyangyong.com/blog/2020-07-07%2015-48-19.gif)

## 复杂度

该算法的复杂度为 `O(n log(log n))`。

## 代码

```javascript
/**
 * @param {number} maxNumber
 * @return {number[]}
 */
export default function sieveOfEratosthenes(maxNumber) {
  const isPrime = new Array(maxNumber + 1).fill(true);
  isPrime[0] = false;
  isPrime[1] = false;

  const primes = [];

  for (let number = 2; number <= maxNumber; number += 1) {
    if (isPrime[number] === true) {
      primes.push(number);

      /*
       * Optimisation.
       * Start marking multiples of `p` from `p * p`, and not from `2 * p`.
       * The reason why this works is because, at that point, smaller multiples
       * of `p` will have already been marked `false`.
       *
       * Warning: When working with really big numbers, the following line may cause overflow
       * In that case, it can be changed to:
       * let nextNumber = 2 * number;
       */
      let nextNumber = number * number;

      while (nextNumber <= maxNumber) {
        isPrime[nextNumber] = false;
        nextNumber += number;
      }
    }
  }

  return primes;
}
```

