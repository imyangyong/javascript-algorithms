# 素数检测

`质数(素数)`是大于 1 的自然数，不能由两个较小的自然数相乘得到。大于 1 的非质数的自然数称为`合数`。

例如：5 是质数，因为它只可被 5 和 1 整除，也就是自身和 1；6 是合数，是因为它不但可被自身和 1 整除，还可被 2 和 3 整除。

![img](http://img.90paw.com/AngusYang9/2020-07-06%2016-44-44.png)

**素数检测是一种确定输入数是否是素数的算法。**在数学的其他领域中，它被用于密码学。与整数因式分解不同，素数检测一般不给出质数因子，只是要说明输入数是否是质数。因式分解被认为是一个计算上困难的问题，而素数检测则相对简单(它的执行过程是输入数的多项式)。

## 代码

```javascript
/**
 * @param {number} number
 * @return {boolean}
 */
export default function trialDivision(number) {
  // Check if number is integer.
  if (number % 1 !== 0) {
    return false;
  }

  if (number <= 1) {
    // If number is less than one then it isn't prime by definition.
    return false;
  }

  if (number <= 3) {
    // All numbers from 2 to 3 are prime.
    return true;
  }

  // If the number is not divided by 2 then we may eliminate all further even dividers.
  if (number % 2 === 0) {
    return false;
  }

  // If there is no dividers up to square root of n then there is no higher dividers as well.
  const dividerLimit = Math.sqrt(number);
  for (let divider = 3; divider <= dividerLimit; divider += 2) {
    if (number % divider === 0) {
      return false;
    }
  }

  return true;
}
```

