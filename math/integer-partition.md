# 整数拆分

在数论和组合学中，正整数 `n` 的拆分，也称为**整数拆分**，是把 `n` 写成正整数和的一种方式。 

只在求和顺序上不同的和被认为是同一个拆分。例如，`4` 可以用五种不同的方式进行拆分：

```bash
4
3 + 1
2 + 2
2 + 1 + 1
1 + 1 + 1 + 1
```

排序相关 `1+3` 与 `3+1` 是相同的拆分，同样 `1+2+1` 和 `1+1+2` 也代表相同的 `2+1+1` 拆分。

与正整数 `1` 到 `8` 的拆分有关的图。它们的排列表示在关于正方形主对角线的反射下的图像是[共轭](https://baike.baidu.com/item/%E5%85%B1%E8%BD%AD/31802)拆分。

![img](https://img.imyangyong.com/blog/2020-07-08%2011-20-47.png)

## 代码

```javascript
/**
 * @param {number} number
 * @return {number}
 */
export default function integerPartition(number) {
  // Create partition matrix for solving this task using Dynamic Programming.
  const partitionMatrix = Array(number + 1).fill(null).map(() => {
    return Array(number + 1).fill(null);
  });

  // Fill partition matrix with initial values.

  // Let's fill the first row that represents how many ways we would have
  // to combine the numbers 1, 2, 3, ..., n with number 0. We would have zero
  // ways obviously since with zero number we may form only zero.
  for (let numberIndex = 1; numberIndex <= number; numberIndex += 1) {
    partitionMatrix[0][numberIndex] = 0;
  }

  // Let's fill the first column. It represents the number of ways we can form
  // number zero out of numbers 0, 0 and 1, 0 and 1 and 2, 0 and 1 and 2 and 3, ...
  // Obviously there is only one way we could form number 0
  // and it is with number 0 itself.
  for (let summandIndex = 0; summandIndex <= number; summandIndex += 1) {
    partitionMatrix[summandIndex][0] = 1;
  }

  // Now let's go through other possible options of how we could form number m out of
  // summands 0, 1, ..., m using Dynamic Programming approach.
  for (let summandIndex = 1; summandIndex <= number; summandIndex += 1) {
    for (let numberIndex = 1; numberIndex <= number; numberIndex += 1) {
      if (summandIndex > numberIndex) {
        // If summand number is bigger then current number itself then just it won't add
        // any new ways of forming the number. Thus we may just copy the number from row above.
        partitionMatrix[summandIndex][numberIndex] = partitionMatrix[summandIndex - 1][numberIndex];
      } else {
        /*
         * The number of combinations would equal to number of combinations of forming the same
         * number but WITHOUT current summand number PLUS number of combinations of forming the
         * <current number - current summand> number but WITH current summand.
         *
         * Example:
         * Number of ways to form 5 using summands {0, 1, 2} would equal the SUM of:
         * - number of ways to form 5 using summands {0, 1} (we've excluded summand 2)
         * - number of ways to form 3 (because 5 - 2 = 3) using summands {0, 1, 2}
         * (we've included summand 2)
        */
        const combosWithoutSummand = partitionMatrix[summandIndex - 1][numberIndex];
        const combosWithSummand = partitionMatrix[summandIndex][numberIndex - summandIndex];

        partitionMatrix[summandIndex][numberIndex] = combosWithoutSummand + combosWithSummand;
      }
    }
  }

  return partitionMatrix[number][number];
}
```



