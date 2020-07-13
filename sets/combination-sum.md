# 组合求和

给定一组数列(没有重复)  和 一个目标值，查找 **数列中总和等于目标值** 的所有可能的组合。

相同的重复数可以从数列中无限次选择。

注意！

- 所有的数字（包括目标值）将是正整数。
- 组合方案不能包含重复的组合。

## 示例

```bash
Input: candidates = [2,3,6,7], target = 7,

A solution set is:
[
  [7],
  [2,2,3]
]
```

```bash
Input: candidates = [2,3,5], target = 8,

A solution set is:
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
```

## 说明

由于问题是要得到所有可能的结果，而不是最好的或组合方案的数量，因此我们不需要考虑DP (dynamic programming，动态规划)，需要使用递归的回溯方法来处理它。

下面是 `数列=[2, 3]` 和 `目标= 6` 情况下的决策树示例:

```bash
           		0
              /   \
           +2      +3
          /   \      \
       +2       +3    +3
      /  \     /  \     \
    +2    ✘   ✘   ✘     ✓
   /  \
  ✓    ✘   
```

## 代码

```javascript
/**
 * @param {number[]} candidates - candidate numbers we're picking from.
 * @param {number} remainingSum - remaining sum after adding candidates to currentCombination.
 * @param {number[][]} finalCombinations - resulting list of combinations.
 * @param {number[]} currentCombination - currently explored candidates.
 * @param {number} startFrom - index of the candidate to start further exploration from.
 * @return {number[][]}
 */
function combinationSumRecursive(
candidates,
 remainingSum,
 finalCombinations = [],
 currentCombination = [],
 startFrom = 0,
) {
  if (remainingSum < 0) {
    // By adding another candidate we've gone below zero.
    // This would mean that the last candidate was not acceptable.
    return finalCombinations;
  }

  if (remainingSum === 0) {
    // If after adding the previous candidate our remaining sum
    // became zero - we need to save the current combination since it is one
    // of the answers we're looking for.
    finalCombinations.push(currentCombination.slice());

    return finalCombinations;
  }

  // If we haven't reached zero yet let's continue to add all
  // possible candidates that are left.
  for (let candidateIndex = startFrom; candidateIndex < candidates.length; candidateIndex += 1) {
    const currentCandidate = candidates[candidateIndex];

    // Let's try to add another candidate.
    currentCombination.push(currentCandidate);

    // Explore further option with current candidate being added.
    combinationSumRecursive(
      candidates,
      remainingSum - currentCandidate,
      finalCombinations,
      currentCombination,
      candidateIndex,
    );

    // BACKTRACKING.
    // Let's get back, exclude current candidate and try another ones later.
    currentCombination.pop();
  }

  return finalCombinations;
}

/**
 * Backtracking algorithm of finding all possible combination for specific sum.
 *
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
 */
export default function combinationSum(candidates, target) {
  return combinationSumRecursive(candidates, target);
}
```

