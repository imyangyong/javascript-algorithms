# 阶乘

在数学上, 一个正整数 `n` 的阶乘 (写作 `n!`)，就是所有小于等于 `n` 的正整数的乘积。 比如:

```javascript
5! = 5 * 4 * 3 * 2 * 1 = 120
```

| n    | n!   |
| ---- | ---- |
| 0    | 1    |
| 1    | 1    |
| 2    | 2    |
| 3    | 6    |
| 4    | 24   |
| 5    | 120  |

## 代码

### 1. 循环实现

```javascript
/**
 * @param {number} number
 * @return {number}
 */
export default function factorial(number) {
  let result = 1;

  for (let i = 2; i <= number; i += 1) {
    result *= i;
  }

  return result;
}
```

### 2. 递归实现

```javascript
/**
 * @param {number} number
 * @return {number}
 */
export default function factorialRecursive(number) {
  return number > 1 ? number * factorialRecursive(number - 1) : 1;
}
```

