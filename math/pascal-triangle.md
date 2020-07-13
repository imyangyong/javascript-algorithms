# 杨辉三角形

在数学中，杨辉三角形（又称帕斯卡三角形）是[二项式系数](https://en.wikipedia.org/wiki/Binomial_coefficient)的三角形数组。

杨辉三角形的行通常从顶部的第 `n = 0` 行开始枚举（第 `0` 行）。每行中的条目从左开始编号 `k = 0`，通常与相邻行中的数字交错。三角形可以按照以下方式构造：在第 `0` 行（最上面的行）中，有一个唯一的非零项 `1`。后面每一行的每个条目都是通过将上面和左边的数字与上面和右边的数字相加来构建的，将空白条目视为 `0` 。例如，第 `1` 行（或任何其他行）中的初始数字是 `1` (`0` 和 `1` 的和)，而第三行中的数字 `1` 和 `3` 被加起来产生第四行中的数字 `4`。

![img](http://img.90paw.com/AngusYang9/2020-07-07%2017-37-20.gif)

## Formula

![img](http://img.90paw.com/AngusYang9/2020-07-07%2017-41-46.png)表示杨辉三角形的第 `n` 行第 `k` 列的项。比如，最上层行的唯一非零项是![img](http://img.90paw.com/AngusYang9/2020-07-07%2017-43-35.png)。

用这种符号，结构可以写成如下：

![img](http://img.90paw.com/AngusYang9/2020-07-07%2017-52-35.png)

对于任意非负整数 `n` 以及 `0` 到 `n` 之间的任意整数 `k`，包括在内：

![img](http://img.90paw.com/AngusYang9/2020-07-07%2017-56-44.png)

## 在 O(n) 复杂度时间内计算三角形

我们知道行号 `lineNumber` 中的第 `i` 项是二项式系数 `C(lineNumber, i)`，并且所有行都从值 `1` 开始。思路是使用 `C(lineNumber, i-1)` 计算 `C(lineNumber, i)`。这可在 `O(1)` 时间内通过以下方法计算：

```javascript
C(lineNumber, i)   = lineNumber! / ((lineNumber - i)! * i!)
C(lineNumber, i - 1) = lineNumber! / ((lineNumber - i + 1)! * (i - 1)!)
```

由以上两个表达式可以推导出以下表达式：

```javascript
C(lineNumber, i) = C(lineNumber, i - 1) * (lineNumber - i + 1) / i
```

所以 `C(lineNumber, i)` 可以由 `C(lineNumber, i - 1)` 在 `O(1)` 时间内计算出来。

## 代码

### 1. 循环实现

```javascript
/**
 * @param {number} lineNumber - zero based.
 * @return {number[]}
 */
export default function pascalTriangle(lineNumber) {
  const currentLine = [1];

  const currentLineSize = lineNumber + 1;

  for (let numIndex = 1; numIndex < currentLineSize; numIndex += 1) {
    // See explanation of this formula at the above.
    currentLine[numIndex] = currentLine[numIndex - 1] * (lineNumber - numIndex + 1) / numIndex;
  }

  return currentLine;
}
```

### 2. 递归实现

```javascript
/**
 * @param {number} lineNumber - zero based.
 * @return {number[]}
 */
export default function pascalTriangleRecursive(lineNumber) {
  if (lineNumber === 0) {
    return [1];
  }

  const currentLineSize = lineNumber + 1;
  const previousLineSize = currentLineSize - 1;

  // Create container for current line values.
  const currentLine = [];

  // We'll calculate current line based on previous one.
  const previousLine = pascalTriangleRecursive(lineNumber - 1);

  // Let's go through all elements of current line except the first and
  // last one (since they were and will be filled with 1's) and calculate
  // current coefficient based on previous line.
  for (let numIndex = 0; numIndex < currentLineSize; numIndex += 1) {
    const leftCoefficient = (numIndex - 1) >= 0 ? previousLine[numIndex - 1] : 0;
    const rightCoefficient = numIndex < previousLineSize ? previousLine[numIndex] : 0;

    currentLine[numIndex] = leftCoefficient + rightCoefficient;
  }

  return currentLine;
}
```

