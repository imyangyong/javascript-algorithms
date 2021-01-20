# 快速算次方

**一个数的幂**表示该数在乘法中乘了多少次。

它被写成一个小的数在基数的右边和上面。

![img](https://img.imyangyong.com/blog/2020-07-07%2020-52-29.png)

## 普通算法复杂度

如何求 `a` 的 `b` 次方?

我们将 `a` 和 `b` 相乘。即 `a^b = a * a * a * …a`  (b 个 a)。

这个操作将花费 `O(n)` 复杂度时间因为我们需要做 `n` 次乘法操作。

## 快速算法复杂度

我们能比普通算法做的更好吗？是的，我们可以在 `O(log(n))` 复杂度时间内解决乘法操作。

该算法采用分而治之的计算方法。目前，该算法适用于两个正整数 `X` 和 `Y`。

该算法背后的思想是基于以下用例：

For `偶数` Y：

```javascript
X^Y = X^(Y/2) * X^(Y/2) 
```

For `奇数` Y：

```javascript
X^Y = X^(Y//2) * X^(Y//2) * X
```

其中 Y//2 是 Y 除以 2 的结果。

### 示例

```javascript
2^4 = (2 * 2) * (2 * 2) = (2^2) * (2^2)
```

```javascript
2^5 = (2 * 2) * (2 * 2) * 2 = (2^2) * (2^2) * (2)
```

现在，因为在每一步我们都需要计算两次相同的 `X^(Y/2)` 次方，我们可以通过将它保存到某个中间变量来优化它，以避免重复计算。

### 时间复杂度

由于每次幂次方我们将幂减半，那么我们将递归地调用函数 `log(n)` 次。将算法的时间复杂度降为:

```javascript
O(log(n))
```

## 代码

```javascript
/**
 * Fast Powering Algorithm.
 * Recursive implementation to compute power.
 *
 * Complexity: log(n)
 *
 * @param {number} base - Number that will be raised to the power.
 * @param {number} power - The power that number will be raised to.
 * @return {number}
 */
export default function fastPowering(base, power) {
  if (power === 0) {
    // Anything that is raised to the power of zero is 1.
    return 1;
  }

  if (power % 2 === 0) {
    // If the power is even...
    // we may recursively redefine the result via twice smaller powers:
    // x^8 = x^4 * x^4.
    const multiplier = fastPowering(base, power / 2);
    return multiplier * multiplier;
  }

  // If the power is odd...
  // we may recursively redefine the result via twice smaller powers:
  // x^9 = x^4 * x^4 * x.
  const multiplier = fastPowering(base, Math.floor(power / 2));
  return multiplier * multiplier * base;
}
```



