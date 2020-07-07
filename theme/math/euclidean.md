# 欧几里得算法

**欧几里德算法是用来求两个正整数最大公约数的算法。**

在数学中，欧几里得算法是计算两个数的最大公约数(GCD)的一种有效方法，最大的公约数能同时除以这两个数而不留下余数。

欧几里得算法是基于两个数的最大公约数不改变的原理，如果较大的数被它与较小的数的差所代替。例如，`21`是`252`和`105`的GCD(即`252 = 21×12`，`105 = 21×5`)，同样的`21`也是`105` 和 `252 - 105 = 147` 的 GCD。由于这个替换刨去了两个数中较大的一个，重复这个过程会得到连续的较小的数对，直到两个数相等。当这种情况发生时，它们就是原始两个数字的GCD。

通过倒转步骤，GCD可以表示为两个原始数各自乘以一个正整数或负整数，如`21 = 5×105 +(−2)×252`。事实上，GCD总是可以用这种方式来表示，这被称为Bezout的身份。

![img](http://img.90paw.com/AngusYang9/2020-07-07%2011-24-28.png)

欧几里得寻找两个起始长度 `BA` 和 `DC` 的最大公约数(GCD)的方法，两者都被定义为公共“单位”长度的倍数。由于 `DC` 的长度较短，它被用来“测量” `BA`，但只有一次，因为剩余的 `EA`小于 `DC`。`EA` 现在测量(两次)较短的 `DC` 长度，剩余的 `FC` 比 `EA` 短。然后 `FC` 测量(三倍)`EA`长度。因为没有剩余，进程以 `FC` 作为 **GCD** 结束。右边是 Nicomachus 的例子，数字 `49` 和 `21` 的 GCD 为 `7` (源自Heath 1908:300)。

![img](http://img.90paw.com/AngusYang9/2020-07-07%2011-44-34.gif )

基于减法的动画欧几里得算法。初始矩形的尺寸为 `a = 1071`, `b = 462`。在其中放置大小为 `462×462` 的正方形，留下一个 `462×147` 的矩形。将该矩形平铺 `147×147` 个正方形，直到留下一个 `21×147` 的矩形，再将该矩形平铺 `21×21` 个正方形，不留下未覆盖的区域。最小的正方形尺寸 `21` 是 `1071` 和 `462` 的GCD。

## 代码

### 1. 递归实现

```javascript
/**
 * Recursive version of Euclidean Algorithm of finding greatest common divisor (GCD).
 * @param {number} originalA
 * @param {number} originalB
 * @return {number}
 */
export default function euclideanAlgorithm(originalA, originalB) {
  // Make input numbers positive.
  const a = Math.abs(originalA);
  const b = Math.abs(originalB);

  // To make algorithm work faster instead of subtracting one number from the other
  // we may use modulo operation.
  return (b === 0) ? a : euclideanAlgorithm(b, a % b);
}
```

### 2. 循环实现

```javascript
/**
 * Iterative version of Euclidean Algorithm of finding greatest common divisor (GCD).
 * @param {number} originalA
 * @param {number} originalB
 * @return {number}
 */
export default function euclideanAlgorithmIterative(originalA, originalB) {
  // Make input numbers positive.
  let a = Math.abs(originalA);
  let b = Math.abs(originalB);

  // Subtract one number from another until both numbers would become the same.
  // This will be out GCD. Also quit the loop if one of the numbers is zero.
  while (a && b && a !== b) {
    [a, b] = a > b ? [a - b, b] : [a, b - a];
  }

  // Return the number that is not equal to zero since the last subtraction (it will be a GCD).
  return a || b;
}
```

