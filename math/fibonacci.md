# 斐波那契数列

在数学中，斐波那契数列是下面这个整数序列中的数，称为斐波那契数列，其特征是前两个数字之后的每一个数字都是`前两个数字的和`:

`0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, ...`

以斐波那契数为边的正方形拼成的近似的[黄金矩形](https://zh.wikipedia.org/wiki/黃金矩形)(1:1.618)

![img](https://img.imyangyong.com/blog/2020-07-06%2015-16-31.png)

斐波那契螺旋：一种近似的[黄金螺旋线](https://en.wikipedia.org/wiki/Golden_spiral)，通过在斐波那契花砖中画出连接正方形对角的圆弧而形成。这个用了大小为1 1 2 3 5 8 13 和21的正方形。

![img](https://img.imyangyong.com/blog/2020-07-06%2015-21-44.png)

## 代码

### 1. 返回斐波那契数列数组

```javascript
/**
 * Return a fibonacci sequence as an array.
 *
 * @param n
 * @return {number[]}
 */
export default function fibonacci(n) {
  const fibSequence = [1];

  let currentValue = 1;
  let previousValue = 0;

  if (n === 1) {
    return fibSequence;
  }

  let iterationsCounter = n - 1;

  while (iterationsCounter) {
    currentValue += previousValue;
    previousValue = currentValue - previousValue;

    fibSequence.push(currentValue);

    iterationsCounter -= 1;
  }

  return fibSequence;
}
```

### 2. 计算特定位置的斐波那契数

```javascript
/**
 * Calculate fibonacci number at specific position using Dynamic Programming approach.
 *
 * @param n
 * @return {number}
 */
export default function fibonacciNth(n) {
  let currentValue = 1;
  let previousValue = 0;

  if (n === 1) {
    return 1;
  }

  let iterationsCounter = n - 1;

  while (iterationsCounter) {
    currentValue += previousValue;
    previousValue = currentValue - previousValue;

    iterationsCounter -= 1;
  }

  return currentValue;
}
```

亦可用递归，不过数目大容易爆栈。

```javascript
/**
 * method 计算斐波那契数列某一位置值.
 * @param {Number} number 数列的位置.
 * @return {Number} return 位置对应的值.
 */
function fibonacc(number){
  if(number === 0){
    return 0;
  }else if(number === 1){
    return 1;
  }
  
  return fibonacc(number - 1) + fibonacc(number - 2);
}
```

