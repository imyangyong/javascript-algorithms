# 复数

复数是 `a + b * i` 的形式，其中 `a` 和 `b` 是实数，`i` 是方程 `i^2 = −1` 的解。因为没有实数满足这个方程，所以 `i` 被称为虚数。对于复数 `a + b * i` ， `a` 称为实部，`b` 称为虚部。

![img](https://img.imyangyong.com/blog/2020-07-07%2019-10-15.png)

复数是实数和虚数的组合：

![img](https://img.imyangyong.com/blog/2020-07-07%2019-10-59.png)



几何上，复数以实部为横轴，虚部为纵轴，将一维数轴的概念扩展到二维复平面。复数 `a + b * i` 与复平面上的点 `(a, b)` 相同。

实部为 0 的复数是纯虚数；这些数字的点位于复平面的垂直轴上。虚部为 0 的复数可以看成是纯实数；它的点位于复平面的水平轴上。

| Complex Number | Real Part | Imaginary Part |                  |
| -------------- | --------- | -------------- | ---------------- |
| 3 + 2i         | 3         | 2              |                  |
| 5              | 5         | **0**          | Purely Real      |
| −6i            | **0**     | -6             | Purely Imaginary |

一个复数可以被直观地表示为一对数字 `(a, b)`，在表示复平面的阿根图上形成一个向量。`Re` 为实轴，`Im` 为虚轴，`i` 满足 `i² = −1`。

![img](https://img.imyangyong.com/blog/2020-07-07%2019-15-50.png)

> 复数并不意味着复杂。它的意思是实数和虚数这两种数字一起构成一个复数，就像建筑物的复数一样（建筑物连在一起）。

## 极坐标

另一种定义在复平面上点 `P` 的方法：除了使用 `x` ，`y` 坐标，还可以使用从 `0` 点出发与正实轴之间的角度，逆时针方向的线段 `OP`。这个想法引出了复数的极坐标形式。

![img](https://img.imyangyong.com/blog/2020-07-07%2019-44-31.png)

复数 `z = x + y*i` 的绝对值为：

![img](https://img.imyangyong.com/blog/2020-07-07%2019-45-38.png)

`z` 的辐角（在许多应用中称为“相位”）是半径 `OP` 与正实轴的夹角，并且表示为 `arg(z)` 。和模数一样，可以从矩形 `x + y*i` 中找到：

![img](https://img.imyangyong.com/blog/2020-07-07%2019-51-01.png)

`r` 和 `φ` 给出了复数的另一种表示方式，即极坐标形式，因为模和辐角的组合完全表示了平面上一点的位置。从极坐标形式中恢复出原来的直角坐标，用三角形式的公式：

![img](https://img.imyangyong.com/blog/2020-07-07%2019-53-53.png)

用欧拉公式可以写成：

![img](https://img.imyangyong.com/blog/2020-07-07%2019-54-27.png)

## 基本操作

### 1. 相加

两个复数相加，我们将每一部分分别相加：

```javascript
(a + b * i) + (c + d * i) = (a + c) + (b + d) * i
```

#### 示例

```javascript
(3 + 5i) + (4 − 3i) = (3 + 4) + (5 − 3)i = 7 + 2i
```

在复杂平面上，相加操作如下：

![img](https://img.imyangyong.com/blog/2020-07-07%2019-57-21.png)

### 2. 相减

两个复数相减，我们要分别减去每一部分：

```javascript
(a + b * i) - (c + d * i) = (a - c) + (b - d) * i
```

#### 示例

```javascript
(3 + 5i) - (4 − 3i) = (3 - 4) + (5 + 3)i = -1 + 8i
```

### 3. 相乘

第一个复数的每一部分都要乘以第二个复数的每一部分：

就用 “FOIL” 吧，它代表 “First, Out, Inners, Last” (详见二项式乘法):

![img](https://img.imyangyong.com/blog/2020-07-07%2020-01-29.png)

- Firsts: `a × c`
- Outers: `a × di`
- Inners: `bi × c`
- Lasts: `bi × di`

所以应该是这样：

```javascript
(a + bi)(c + di) = ac + adi + bci + bdi^2
```

但是还有更简便的方法！

```javascript
(a + bi)(c + di) = (ac − bd) + (ad + bc)i
```

#### 示例

```javascript
(3 + 2i)(1 + 7i)
= 3×1 + 3×7i + 2i×1+ 2i×7i
= 3 + 21i + 2i + 14i^2
= 3 + 21i + 2i − 14   (because i^2 = −1)
= −11 + 23i
```

```javascript
(3 + 2i)(1 + 7i) = (3×1 − 2×7) + (3×7 + 2×1)i = −11 + 23i
```

### 4. 共轭

什么是共轭？马上会知道！

共轭就是我们像这样改变中间的符号。

![img](https://img.imyangyong.com/blog/2020-07-07%2020-04-54.png)

共轭复数通常用横杠表示：

```javascript
______
5 − 3i   =   5 + 3i
```

在复平面上，共轭数将与实轴相反。

![img](https://img.imyangyong.com/blog/2020-07-07%2020-05-46.png)

### 5. 相除

共轭用来帮助复数除法。

技巧是上下同时乘以分母的共轭。

#### 示例

```javascript
2 + 3i
------
4 − 5i
```

上下乘以 `4−5i` 的共轭：

```javascript
  (2 + 3i) * (4 + 5i)   8 + 10i + 12i + 15i^2
= ------------------- = ----------------------
  (4 − 5i) * (4 + 5i)   16 + 20i − 20i − 25i^2
```

记住 `i²= -1`，所以：

```javascript
  8 + 10i + 12i − 15    −7 + 22i   −7   22
= ------------------- = -------- = -- + -- * i
  16 + 20i − 20i + 25      41      41   41
```

不过还有更快的方法。

在前面的例子中，下面发生的事情很有趣：

```javascript
(4 − 5i)(4 + 5i) = 16 + 20i − 20i − 25i
```

中间项 `(20i - 20i)` 可以消去 `i²= -1`，所以我们得到：

```javascript
(4 − 5i)(4 + 5i) = 4^2 + 5^2
```

这是一个非常简单的结果。一般规则是：

```javascript
(a + bi)(a − bi) = a^2 + b^2
```

## 代码

```javascript
export default class ComplexNumber {
  /**
   * z = re + im * i
   * z = radius * e^(i * phase)
   *
   * @param {number} [re]
   * @param {number} [im]
   */
  constructor({ re = 0, im = 0 } = {}) {
    this.re = re;
    this.im = im;
  }

  /**
   * @param {ComplexNumber|number} addend
   * @return {ComplexNumber}
   */
  add(addend) {
    // Make sure we're dealing with complex number.
    const complexAddend = this.toComplexNumber(addend);

    return new ComplexNumber({
      re: this.re + complexAddend.re,
      im: this.im + complexAddend.im,
    });
  }

  /**
   * @param {ComplexNumber|number} subtrahend
   * @return {ComplexNumber}
   */
  subtract(subtrahend) {
    // Make sure we're dealing with complex number.
    const complexSubtrahend = this.toComplexNumber(subtrahend);

    return new ComplexNumber({
      re: this.re - complexSubtrahend.re,
      im: this.im - complexSubtrahend.im,
    });
  }

  /**
   * @param {ComplexNumber|number} multiplicand
   * @return {ComplexNumber}
   */
  multiply(multiplicand) {
    // Make sure we're dealing with complex number.
    const complexMultiplicand = this.toComplexNumber(multiplicand);

    return new ComplexNumber({
      re: this.re * complexMultiplicand.re - this.im * complexMultiplicand.im,
      im: this.re * complexMultiplicand.im + this.im * complexMultiplicand.re,
    });
  }

  /**
   * @param {ComplexNumber|number} divider
   * @return {ComplexNumber}
   */
  divide(divider) {
    // Make sure we're dealing with complex number.
    const complexDivider = this.toComplexNumber(divider);

    // Get divider conjugate.
    const dividerConjugate = this.conjugate(complexDivider);

    // Multiply dividend by divider's conjugate.
    const finalDivident = this.multiply(dividerConjugate);

    // Calculating final divider using formula (a + bi)(a − bi) = a^2 + b^2
    const finalDivider = (complexDivider.re ** 2) + (complexDivider.im ** 2);

    return new ComplexNumber({
      re: finalDivident.re / finalDivider,
      im: finalDivident.im / finalDivider,
    });
  }

  /**
   * @param {ComplexNumber|number} number
   */
  conjugate(number) {
    // Make sure we're dealing with complex number.
    const complexNumber = this.toComplexNumber(number);

    return new ComplexNumber({
      re: complexNumber.re,
      im: -1 * complexNumber.im,
    });
  }

  /**
   * @return {number}
   */
  getRadius() {
    return Math.sqrt((this.re ** 2) + (this.im ** 2));
  }

  /**
   * @param {boolean} [inRadians]
   * @return {number}
   */
  getPhase(inRadians = true) {
    let phase = Math.atan(Math.abs(this.im) / Math.abs(this.re));

    if (this.re < 0 && this.im > 0) {
      phase = Math.PI - phase;
    } else if (this.re < 0 && this.im < 0) {
      phase = -(Math.PI - phase);
    } else if (this.re > 0 && this.im < 0) {
      phase = -phase;
    } else if (this.re === 0 && this.im > 0) {
      phase = Math.PI / 2;
    } else if (this.re === 0 && this.im < 0) {
      phase = -Math.PI / 2;
    } else if (this.re < 0 && this.im === 0) {
      phase = Math.PI;
    } else if (this.re > 0 && this.im === 0) {
      phase = 0;
    } else if (this.re === 0 && this.im === 0) {
      // More correctly would be to set 'indeterminate'.
      // But just for simplicity reasons let's set zero.
      phase = 0;
    }

    if (!inRadians) {
      phase = radianToDegree(phase);
    }

    return phase;
  }

  /**
   * @param {boolean} [inRadians]
   * @return {{radius: number, phase: number}}
   */
  getPolarForm(inRadians = true) {
    return {
      radius: this.getRadius(),
      phase: this.getPhase(inRadians),
    };
  }

  /**
   * Convert real numbers to complex number.
   * In case if complex number is provided then lefts it as is.
   *
   * @param {ComplexNumber|number} number
   * @return {ComplexNumber}
   */
  toComplexNumber(number) {
    if (number instanceof ComplexNumber) {
      return number;
    }

    return new ComplexNumber({ re: number });
  }
}

/**
 * @param {number} radian
 * @return {number}
 */
function radianToDegree(radian) {
  return radian * (180 / Math.PI);
}
```

