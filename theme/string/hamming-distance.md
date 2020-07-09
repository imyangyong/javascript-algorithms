# 汉明距离

在[信息论](https://zh.wikipedia.org/wiki/信息论)中，**汉明距离**（英语：Hamming distance）是指两个等长字符串对应位置的不同字符的个数。换句话说，它就是将一个字符串变换成另外一个字符串所需要*替换*的字符个数。

## 示例

- "ka**rol**in" 和 "ka**thr**in" 汉明距离是 **3**.
- "k**a**r**ol**in" 和 "k**e**r**st**in" 汉明距离是 **3**.
- 10**1**1**1**01 和 10**0**1**0**01 汉明距离是 **2**.
- 2**17**3**8**96 和 2**23**3**7**96 汉明距离是 **3**.

## 代码

```javascript
/**
 * @param {string} a
 * @param {string} b
 * @return {number}
 */
export default function hammingDistance(a, b) {
  if (a.length !== b.length) {
    throw new Error('Strings must be of the same length');
  }

  let distance = 0;

  for (let i = 0; i < a.length; i += 1) {
    if (a[i] !== b[i]) {
      distance += 1;
    }
  }

  return distance;
}
```

