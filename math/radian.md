# 弧度和角

**弧度**（符号 rad）是测量角度的单位，也是在许多数学领域中使用的角度测量的标准单位。

**圆的弧度（rad）等于圆半径（r）长度的弧长对应的角**；一个弧度刚好低于 `57.3` 度。

圆周为一个 `2π` 弧度的角；周长为 `2πr`。

![img](https://img.imyangyong.com/blog/2020-07-07%2020-37-28.gif)

一个完整的旋转是 `2π` 弧度。

![img](https://img.imyangyong.com/blog/2020-07-07%2020-41-11.gif)

## 换算

| Radians | Degrees |
| ------- | ------- |
| 0       | 0°      |
| π/12    | 15°     |
| π/6     | 30°     |
| π/4     | 45°     |
| 1       | 57.3°   |
| π/3     | 60°     |
| π/2     | 90°     |
| π       | 180°    |
| 2π      | 360°    |

## 代码

### 1. 角度 => 弧度

```javascript
/**
 * @param {number} degree
 * @return {number}
 */
export default function degreeToRadian(degree) {
  return degree * (Math.PI / 180);
}
```

### 2. 弧度 => 角度

```javascript
/**
 * @param {number} radian
 * @return {number}
 */
export default function radianToDegree(radian) {
  return radian * (180 / Math.PI);
}
```

