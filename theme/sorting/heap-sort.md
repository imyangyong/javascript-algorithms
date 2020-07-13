# 堆排序

**堆排序**（英语：Heapsort）是指利用[堆](https://baike.baidu.com/item/堆)这种数据结构所设计的一种排序算法。堆是一个近似[完全二叉树](https://baike.baidu.com/item/完全二叉树)的结构，并同时满足**堆积的性质**：即子结点的键值或索引总是小于（或者大于）它的父节点。

堆排序可以被认为是一种改进的[选择排序](/theme/sorting/selection-sort.html)：它把输入分为一个已排序的区域和一个未排序的区域，然后通过提取最大的元素并将其移动到已排序的区域，迭代地缩小未排序的区域。改进为使用堆数据结构，而不是使用线性时间搜索来查找最大或值。

![img](http://img.90paw.com/AngusYang9/2020-07-11%2019-04-32.gif)

![img](http://img.90paw.com/AngusYang9/2020-07-11%2019-05-08.gif)

## 时间复杂度

`O(nlog(n))`

## 代码

[code](https://github.com/trekhleb/javascript-algorithms/tree/master/src/algorithms/sorting/heap-sort)