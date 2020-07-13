# 正向遍历

**遍历给定的链表**。

例如下面的链表：

![img](http://img.90paw.com/AngusYang9/2020-07-13%2018-05-09.png)

遍历的顺序应该为：

```bash
12 → 99 → 37
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
 * @param {LinkedList} linkedList
 * @param {traversalCallback} callback
 */
export default function traversal(linkedList, callback) {
  let currentNode = linkedList.head;

  while (currentNode) {
    callback(currentNode.value);
    currentNode = currentNode.next;
  }
}
```

