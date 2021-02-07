# 算法范式

算法范式是一种通用方法，基于一类算法的设计。这是比算法更高的抽象，就像算法是比计算机程序更高的抽象。

`B` - 初学者， `A` - 进阶

### 暴力匹配算法(Brute Force, BF) - `查找/搜索` 所有可能性并选择最佳解决方案

- `B` [线性查找](/search/linear-search.html) - 遍历查找匹配的元素 `O(n)`
- `B` [雨水收集](/uncategorized/rain-terraces.html) - 诱捕雨水问题 (动态编程和暴力版本)
- `B` [递归楼梯](/uncategorized/recursive-staircase.html) - 计算有共有多少种方法可以到达顶层 (4 种解题方案)
- `A` [最大子数列问题](/sets/maximum-subarray.html) - 数组中 `和最大` 的子数列
- `A` [旅行推销员问题](/graph/travelling-salesman.html) - 尽可能以最短的路线访问每个城市并返回原始城市
- `A` [离散傅里叶变换](/math/fourier-transform.html)

### 贪心算法(Greedy Algorithm) - 在当前选择最佳选项，不考虑以后情况

- `B` [跳跃游戏](/uncategorized/square-matrix-rotation.html) - 回溯,、动态编程 (自上而下+自下而上) 和贪婪的例子
- `A` [背包问题](/sets/knapsack-problem.html) - 向固定容量的背包（容器）填充尽可能大的值
- `A` [戴克斯特拉算法](/graph/dijkstra.html) - 找到图中所有顶点的最短路径
- `A` [普林姆算法](/graph/prim.html) - 寻找加权无向图的最小生成树 (MST)
- `B` [克鲁斯克尔演算法](/graph/kruskal.html) - 寻找加权无向图的最小生成树 (MST)

### 分治法(Divide-and-Conquer Algorithm) - 将问题分成较小的部分，然后解决这些部分

- `B` [二分查找](/search/binary-search.html) - 有序数组二分查找匹配的元素 `O(log(n))`
- `B` [汉诺塔](/uncategorized/hanoi-tower.html)
- `B` [杨辉三角形](/math/pascal-triangle.html)
- `B` [欧几里得算法](/math/euclidean.html) - 求两个数的最大公约数(GCD)
- `B` [归并排序](/sorting/merge-sort.html) - (递归)拆分比较后合并 `O(nlog(n))`
- `B` [快速排序](/sorting/quick-sort.html) - (递归)基于基数二分，大小各置一边 `O(nlog(n))`
- `B` [深度优先搜索](/tree/depth-first-search.html)（DFS）
- `B` [深度优先搜索](/graph/depth-first-search.html)（DFS）
- `B` [跳跃游戏](/uncategorized/square-matrix-rotation.html) - 回溯,、动态编程 (自上而下+自下而上) 和贪婪的例子
- `B` [快速算次方](/math/fast-powering.html) - 幂次方复杂度由 O(n) 降为 O(log(n))
- `A` [排列](/sets/permutations.html) - 有/无重复排列
- `A` [组合](/sets/combinations.html) - 有/无重复组合

### 动态规划算法(Dynamic programming, DP) - 使用以前找到的子解决方案构建解决方案

- `B` [斐波那契数列](/math/fibonacci.html) - `0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, ...`
- `B` [跳跃游戏](/uncategorized/square-matrix-rotation.html) - 回溯,、动态编程 (自上而下+自下而上) 和贪婪的例子
- `B` [独特(唯一) 路径](/uncategorized/unique-paths.html) - 回溯、动态编程和基于 Pascal 三角形的例子
- `B` [雨水收集](/uncategorized/rain-terraces.html) - 诱捕雨水问题 (动态编程和暴力版本)
- `B` [递归楼梯](/uncategorized/recursive-staircase.html) - 计算有共有多少种方法可以到达顶层 (4 种解题方案)
- `A` [莱温斯坦距离](/string/levenshtein-distance.html) - 两个字符串之间，由一个转成另一个所需的最少编辑操作次数。
- `A` [最长公共子序列](/sets/longest-common-subsequence.html) - 最长公共子序列（LCS）
- `A` [最长公共子串](/string/longest-common-substring.html) - 多个字符串的最长子串
- `A` [最长递增子序列](/sets/longest-increasing-subsequence.html) - 最长递增子序列
- `A` [最短公共父序列](/sets/shortest-common-supersequence.html) - 最短公共父序列（SCS）
- `A` [0-1背包问题](/sets/knapsack-problem.html) - 向固定容量的背包（容器）填充尽可能大的值
- `A` [整数拆分](/math/integer-partition.html)
- `A` [最大子数列问题](/sets/maximum-subarray.html) - 数组中 `和最大` 的子数列
- `A` [贝尔曼-福特算法](/graph/bellman-ford.html) - 找到图中所有顶点的最短路径
- `A` [弗洛伊德算法](/graph/floyd-warshall.html) - 找到所有 `顶点对` 之间的最短路径
- `A` [正则表达式匹配](/string/regular-expression-matching.html)

### 回溯法(Backtracking) - 类似于 BF 算法 试图产生所有可能的解决方案，但每次生成解决方案测试如果它满足所有条件，那么只有继续生成后续解决方案。否则回溯并继续寻找不同路径的解决方案。

- `B` [跳跃游戏](/uncategorized/square-matrix-rotation.html) - 回溯,、动态编程 (自上而下+自下而上) 和贪婪的例子
- `B` [独特(唯一) 路径](/uncategorized/unique-paths.html) - 回溯、动态编程和基于 Pascal 三角形的例子
- `A` [幂集](/sets/power-set.html) - 集合的所有子集
- `A` [哈密顿图](/graph/hamiltonian-cycle.html) - 恰好访问每个顶点一次
- `A` [八皇后问题](/uncategorized/n-queens.html)
- `A` [骑士巡逻](/uncategorized/knight-tour.html)
- `A` [组合求和](/sets/combination-sum.html) - `数列中总和等于目标值` 的所有可能的组合

### 分支定界法(branch and bound) - 记住在回溯搜索的每个阶段找到的成本最低的解决方案，并使用到目前为止找到的成本最小值作为下限。以便丢弃成本大于最小值的解决方案。通常，使用 BFS 遍历以及状态空间树的 DFS 遍历。
