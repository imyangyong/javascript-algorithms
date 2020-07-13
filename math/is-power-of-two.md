# 判断2次方数

给出一个正整数，写一个函数来找出它是否是 `2` 的幂。

## 一、常规方案

在常规方案中，我们就一直除以 `2` 直到这个数变成 `1` ，与此同时，我们检查除法后的余数总是 `0`。否则这个数不可能是 `2` 的幂。

## 二、位操作方案

二进制形式的 `2` 的幂总是只有一个 `bit` 。唯一的例外是有符号整数 (例如，值为 -128 的 8 位有符号整数是: 10000000)。

```bash
1: 0001
2: 0010
4: 0100
8: 1000
```

因此，在检查数字大于零之后，我们可以使用逐位 hack 来测试只设置了一位 bit。

```javascript
number & (number - 1)
```

例如，数字 8 的操作是这样的：

```javascript
  1000
- 0001
  ----
  0111
  
  1000
& 0111
  ----
  0000 
```

## 代码

### 1. 常规实现

```javascript
/**
 * @param {number} number
 * @return {boolean}
 */
export default function isPowerOfTwo(number) {
  // 1 (2^0) is the smallest power of two.
  if (number < 1) {
    return false;
  }

  // Let's find out if we can divide the number by two
  // many times without remainder.
  let dividedNumber = number;
  while (dividedNumber !== 1) {
    if (dividedNumber % 2 !== 0) {
      // For every case when remainder isn't zero we can say that this number
      // couldn't be a result of power of two.
      return false;
    }

    dividedNumber /= 2;
  }

  return true;
}
```

### 2. 位操作实现

```javascript
/**
 * @param {number} number
 * @return {boolean}
 */
export default function isPowerOfTwoBitwise(number) {
  // 1 (2^0) is the smallest power of two.
  if (number < 1) {
    return false;
  }

  /*
   * Powers of two in binary look like this:
   * 1: 0001
   * 2: 0010
   * 4: 0100
   * 8: 1000
   *
   * Note that there is always exactly 1 bit set. The only exception is with a signed integer.
   * e.g. An 8-bit signed integer with a value of -128 looks like:
   * 10000000
   *
   * So after checking that the number is greater than zero, we can use a clever little bit
   * hack to test that one and only one bit is set.
   */
  return (number & (number - 1)) === 0;
}
```

