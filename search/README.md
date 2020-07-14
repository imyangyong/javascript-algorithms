# 搜索

时间复杂度效率排名：

① [插值查找](/search/interpolation-search.html) - `O(log(log(n)))`

② [二分查找](/search/binary-search.html) - `O(log(n))`

③ [跳跃查找/块查找](/search/jump-search.html) - `O(√n)`

④ [线性查找](/search/linear-search.html) - `O(n)`

描述：

- `B` [线性查找](/search/linear-search.html) - 遍历查找匹配的元素 `O(n)`
- `B` [跳跃查找/块查找](/search/jump-search.html) - 有序数组跳跃查找匹配的元素 `O(√n)`
- `B` [二分查找](/search/binary-search.html) - 有序数组二分查找匹配的元素 `O(log(n))`
- `B` [插值查找](/search/interpolation-search.html) - 有序数组依据`插值公式`定位查找 `O(log(log(n)))`
