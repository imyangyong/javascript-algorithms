# 广度优先搜索

广度优先搜索是一种遍历搜索树或图数据结构的算法。它从树的根（或图中的某个任意节点，有时被称为“搜索键”）开始，在移动到下一层节点之前，首先探索同层节点。

![img](https://img.imyangyong.com/blog/2020-07-13%2019-28-17.gif)

## 代码

```javascript
import Queue from '../../../data-structures/queue/Queue';
// https://github.com/trekhleb/javascript-algorithms/blob/master/src/data-structures/queue/Queue.js

/**
 * @typedef {Object} Callbacks
 *
 * @property {function(vertices: Object): boolean} [allowTraversal] -
 *   Determines whether DFS should traverse from the vertex to its neighbor
 *   (along the edge). By default prohibits visiting the same vertex again.
 *
 * @property {function(vertices: Object)} [enterVertex] - Called when BFS enters the vertex.
 *
 * @property {function(vertices: Object)} [leaveVertex] - Called when BFS leaves the vertex.
 */

/**
 * @param {Callbacks} [callbacks]
 * @returns {Callbacks}
 */
function initCallbacks(callbacks = {}) {
  const initiatedCallback = callbacks;

  const stubCallback = () => {};

  const allowTraversalCallback = (
    () => {
      const seen = {};
      return ({ nextVertex }) => {
        if (!seen[nextVertex.getKey()]) {
          seen[nextVertex.getKey()] = true;
          return true;
        }
        return false;
      };
    }
  )();

  initiatedCallback.allowTraversal = callbacks.allowTraversal || allowTraversalCallback;
  initiatedCallback.enterVertex = callbacks.enterVertex || stubCallback;
  initiatedCallback.leaveVertex = callbacks.leaveVertex || stubCallback;

  return initiatedCallback;
}

/**
 * @param {Graph} graph
 * @param {GraphVertex} startVertex
 * @param {Callbacks} [originalCallbacks]
 */
export default function breadthFirstSearch(graph, startVertex, originalCallbacks) {
  const callbacks = initCallbacks(originalCallbacks);
  const vertexQueue = new Queue();

  // Do initial queue setup.
  vertexQueue.enqueue(startVertex);

  let previousVertex = null;

  // Traverse all vertices from the queue.
  while (!vertexQueue.isEmpty()) {
    const currentVertex = vertexQueue.dequeue();
    callbacks.enterVertex({ currentVertex, previousVertex });

    // Add all neighbors to the queue for future traversals.
    graph.getNeighbors(currentVertex).forEach((nextVertex) => {
      if (callbacks.allowTraversal({ previousVertex, currentVertex, nextVertex })) {
        vertexQueue.enqueue(nextVertex);
      }
    });

    callbacks.leaveVertex({ currentVertex, previousVertex });

    // Memorize current vertex before next loop.
    previousVertex = currentVertex;
  }
}
```

