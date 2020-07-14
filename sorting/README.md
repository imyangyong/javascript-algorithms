# 排序

时间复杂度效率排名：

① [基数排序](/sorting/radix-sort.html) -  `O(n * k)`  k 为整数的位数

② [快速排序](/sorting/quick-sort.html) -  `O(nlog(n))`

② [归并排序](/sorting/merge-sort.html) -  `O(nlog(n))`

③ [希尔排序](/sorting/shell-sort.html) -  `O(n^(1.3—2))`

④ [冒泡排序](/sorting/bubble-sort.html) -  `O(n^2)`

④ [插入排序](/sorting/insertion-sort.html) -  `O(n^2)`

④ [选择排序](/sorting/selection-sort.html) -  `O(n^2)`

描述：

- `B` [冒泡排序](/sorting/bubble-sort.html) - `O(n^2)`
- `B` [快速排序](/sorting/quick-sort.html) - (递归)基于基数二分，大小各置一边 `O(nlog(n))`
- `B` [归并排序](/sorting/merge-sort.html) - (递归)拆分比较后合并 `O(nlog(n))`
- `B` [计数排序](/sorting/counting-sort.html) - (非比较型)适用于数值范围较小的整数排序 `O(n + r)` r 为数值最大与最小的差值
- `B` [基数排序](/sorting/radix-sort.html) - (非比较型)整数位数分隔，按位比较 `O(n * k)` k 为整数的位数
- `B` [插入排序](/sorting/insertion-sort.html) - 适用于少量元素排序 `O(n^2)`
- `B` [希尔排序](/sorting/shell-sort.html) - 按增量分组排序，每组执行插入排序 `O(n^(1.3—2))`
- `B` [选择排序](/sorting/selection-sort.html) - `O(n^2)`
- `B` [堆排序](/sorting/heap-sort.html)
