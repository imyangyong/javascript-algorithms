# 最小公倍数

在算术和数论中，两个整数a和b的最小公倍数，通常用 `LCM(a, b)` 表示，是能被 `a` 和 `b` 整除的最小正整数。

由于整数除以 `0` 是没有定义的，这个定义只有在 a 和 b 都不等于 0 时才有意义。但也有一些人将所有 a 的 `lcm(a,0)` 定义为 0，这是取 lcm 为可整除格的最小上边界的结果。

## example

4 和 6 的 LCM 是什么？

4 的倍数为：

```bas
4, 8, 12, 16, 20, 24, 28, 32, 36, 40, 44, 48, 52, 56, 60, 64, 68, 72, 76, ...
```

6 的倍数为：

```bash
6, 12, 18, 24, 30, 36, 42, 48, 54, 60, 66, 72, ...
```

4 和 6 的公倍数就是两个列表中相同的数字:

```bash
12, 24, 36, 48, 60, 72, ....
```

所以，它们的最小公倍数是 12。

## 计算最小公倍数

下式将最小公倍数的计算简化为[最大公约数(GCD)](/theme/math/euclidean.html)的计算，又称最大公因数:

```javascript
lcm(a, b) = |a * b| / gcd(a, b)
```

![img](https://img.imyangyong.com/blog/2020-07-07%2014-13-01.png)

维恩图显示2、3、4、5和7组合的最小公倍数(6被跳过，因为它是2×3，两者都已经表示出来了)。

例如，一场纸牌游戏需要在少于等于 5 名玩家中平分，至少需要60张牌，即 2, 3, 4 和 5 交集的数字，而不是7。

## 代码

```javascript
// euclideanAlgorithm 请参考最大公约数 https://www.90paw.com/javascript-algorithms/theme/math/euclidean.html

/**
 * @param {number} a
 * @param {number} b
 * @return {number}
 */

export default function leastCommonMultiple(a, b) {
  return ((a === 0) || (b === 0)) ? 0 : Math.abs(a * b) / euclideanAlgorithm(a, b);
}
```

