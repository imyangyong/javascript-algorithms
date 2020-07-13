# 反向遍历

**反向遍历给定的链表。**

例如下面的链表：

![img](http://img.90paw.com/AngusYang9/2020-07-13%2018-05-09.png)

遍历的顺序应该为：

```bash
37 → 99 → 12
```

## 时间复杂度

`O(n)` - 我们只需一次遍历访问所有节点。

## 代码

```javascript
/**
 * Traversal callback function.
 * @callback traversalCallback
 * @param {*} nodeValue
 */

/**
 * @param {LinkedListNode} node
 * @param {traversalCallback} callback
 */
function reverseTraversalRecursive(node, callback) {
  if (node) {
    reverseTraversalRecursive(node.next, callback);
    callback(node.value);
  }
}

/**
 * @param {LinkedList} linkedList
 * @param {traversalCallback} callback
 */
export default function reverseTraversal(linkedList, callback) {
  reverseTraversalRecursive(linkedList.head, callback);
}
```

