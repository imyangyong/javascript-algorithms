# 背包问题

背包问题是一个组合优化问题：给定一组项目，每个项目都有`一个重量` 和 `一个值`，总重量小于等于给定的限制，并且总值尽可能大。

它的名字来源于一个人所面临的问题，这个人被一个固定大小的背包所困扰，必须把最有价值的东西装进去。

下面就是背包问题的示例：应该选择哪些箱子来最大限度地增加钱的数量，同时保持总重量小于等于 15 公斤?

![img](https://img.imyangyong.com/blog/2020-07-08%2019-31-35.png)

## 定义

### 0/1 背包问题

最常见的问题是 **0/1 背包问题**，它将每种项目的数量 `xi` 限制为 `0` 或 `1`。

给定一组从 `1` 到 `n` 的 `n` 个项目，每个项目的重量 `wi` 和值 `vi`，以及最大重量的容量 `W`，

最大值 ![img](https://img.imyangyong.com/blog/2020-07-08%2019-38-10.png)

受到 ![img](https://img.imyangyong.com/blog/2020-07-08%2019-38-51.png) 和 ![img](https://img.imyangyong.com/blog/2020-07-08%2019-39-24.png) 限制

这里 `xi` 表示要包含在背包中的项目 `i` 的数量（这里只能为 0 或 1，要么有要么没有）。那么，问题是最大化背包中物品的价值总和，使重量总和小于等于背包的容量。

### 有界背包问题(BKP)

有界背包问题(BKP) 消除了每一项只有一个的限制，但将每一种项的数量 `xi` 限制为最大的非负整数值 `c`：

最大值 ![img](https://img.imyangyong.com/blog/2020-07-08%2019-45-38.png)

受到 ![img](https://img.imyangyong.com/blog/2020-07-08%2019-38-51.png) 和 ![img](https://img.imyangyong.com/blog/2020-07-08%2019-46-37.png) 限制

### 无界背包问题(UKP)

无界背包问题(UKP) 对每种项的数量没有限制且无上界，可以用上述公式表示，但对 `xi` 必须是非负整数。

最大值 ![img](https://img.imyangyong.com/blog/2020-07-08%2019-45-38.png)

受到 ![img](https://img.imyangyong.com/blog/2020-07-08%2019-38-51.png) 和 ![img](https://img.imyangyong.com/blog/2020-07-08%2019-48-54.png) 限制

## 代码

- KnapsackItem 

```javascript
export default class KnapsackItem {
  /**
   * @param {Object} itemSettings - knapsack item settings,
   * @param {number} itemSettings.value - value of the item.
   * @param {number} itemSettings.weight - weight of the item.
   * @param {number} itemSettings.itemsInStock - how many items are available to be added.
   */
  constructor({ value, weight, itemsInStock = 1 }) {
    this.value = value;
    this.weight = weight;
    this.itemsInStock = itemsInStock;
    // Actual number of items that is going to be added to knapsack.
    this.quantity = 1;
  }

  get totalValue() {
    return this.value * this.quantity;
  }

  get totalWeight() {
    return this.weight * this.quantity;
  }

  // This coefficient shows how valuable the 1 unit of weight is
  // for current item.
  get valuePerWeightRatio() {
    return this.value / this.weight;
  }

  toString() {
    return `v${this.value} w${this.weight} x ${this.quantity}`;
  }
}
```

- Knapsack

```javascript
import MergeSort from utils;
// https://github.com/AngusYang9/javascript-algorithms/blob/master/src/algorithms/sorting/merge-sort/MergeSort.js

export default class Knapsack {
  /**
   * @param {KnapsackItem[]} possibleItems
   * @param {number} weightLimit
   */
  constructor(possibleItems, weightLimit) {
    this.selectedItems = [];
    this.weightLimit = weightLimit;
    this.possibleItems = possibleItems;
  }

  sortPossibleItemsByWeight() {
    this.possibleItems = new MergeSort({
      /**
       * @var KnapsackItem itemA
       * @var KnapsackItem itemB
       */
      compareCallback: (itemA, itemB) => {
        if (itemA.weight === itemB.weight) {
          return 0;
        }

        return itemA.weight < itemB.weight ? -1 : 1;
      },
    }).sort(this.possibleItems);
  }

  sortPossibleItemsByValue() {
    this.possibleItems = new MergeSort({
      /**
       * @var KnapsackItem itemA
       * @var KnapsackItem itemB
       */
      compareCallback: (itemA, itemB) => {
        if (itemA.value === itemB.value) {
          return 0;
        }

        return itemA.value > itemB.value ? -1 : 1;
      },
    }).sort(this.possibleItems);
  }

  sortPossibleItemsByValuePerWeightRatio() {
    this.possibleItems = new MergeSort({
      /**
       * @var KnapsackItem itemA
       * @var KnapsackItem itemB
       */
      compareCallback: (itemA, itemB) => {
        if (itemA.valuePerWeightRatio === itemB.valuePerWeightRatio) {
          return 0;
        }

        return itemA.valuePerWeightRatio > itemB.valuePerWeightRatio ? -1 : 1;
      },
    }).sort(this.possibleItems);
  }

  // Solve 0/1 knapsack problem
  // Dynamic Programming approach.
  solveZeroOneKnapsackProblem() {
    // We do two sorts because in case of equal weights but different values
    // we need to take the most valuable items first.
    this.sortPossibleItemsByValue();
    this.sortPossibleItemsByWeight();

    this.selectedItems = [];

    // Create knapsack values matrix.
    const numberOfRows = this.possibleItems.length;
    const numberOfColumns = this.weightLimit;
    const knapsackMatrix = Array(numberOfRows).fill(null).map(() => {
      return Array(numberOfColumns + 1).fill(null);
    });

    // Fill the first column with zeros since it would mean that there is
    // no items we can add to knapsack in case if weight limitation is zero.
    for (let itemIndex = 0; itemIndex < this.possibleItems.length; itemIndex += 1) {
      knapsackMatrix[itemIndex][0] = 0;
    }

    // Fill the first row with max possible values we would get by just adding
    // or not adding the first item to the knapsack.
    for (let weightIndex = 1; weightIndex <= this.weightLimit; weightIndex += 1) {
      const itemIndex = 0;
      const itemWeight = this.possibleItems[itemIndex].weight;
      const itemValue = this.possibleItems[itemIndex].value;
      knapsackMatrix[itemIndex][weightIndex] = itemWeight <= weightIndex ? itemValue : 0;
    }

    // Go through combinations of how we may add items to knapsack and
    // define what weight/value we would receive using Dynamic Programming
    // approach.
    for (let itemIndex = 1; itemIndex < this.possibleItems.length; itemIndex += 1) {
      for (let weightIndex = 1; weightIndex <= this.weightLimit; weightIndex += 1) {
        const currentItemWeight = this.possibleItems[itemIndex].weight;
        const currentItemValue = this.possibleItems[itemIndex].value;

        if (currentItemWeight > weightIndex) {
          // In case if item's weight is bigger then currently allowed weight
          // then we can't add it to knapsack and the max possible value we can
          // gain at the moment is the max value we got for previous item.
          knapsackMatrix[itemIndex][weightIndex] = knapsackMatrix[itemIndex - 1][weightIndex];
        } else {
          // Else we need to consider the max value we can gain at this point by adding
          // current value or just by keeping the previous item for current weight.
          knapsackMatrix[itemIndex][weightIndex] = Math.max(
            currentItemValue + knapsackMatrix[itemIndex - 1][weightIndex - currentItemWeight],
            knapsackMatrix[itemIndex - 1][weightIndex],
          );
        }
      }
    }

    // Now let's trace back the knapsack matrix to see what items we're going to add
    // to the knapsack.
    let itemIndex = this.possibleItems.length - 1;
    let weightIndex = this.weightLimit;

    while (itemIndex > 0) {
      const currentItem = this.possibleItems[itemIndex];
      const prevItem = this.possibleItems[itemIndex - 1];

      // Check if matrix value came from top (from previous item).
      // In this case this would mean that we need to include previous item
      // to the list of selected items.
      if (
        knapsackMatrix[itemIndex][weightIndex]
        && knapsackMatrix[itemIndex][weightIndex] === knapsackMatrix[itemIndex - 1][weightIndex]
      ) {
        // Check if there are several items with the same weight but with the different values.
        // We need to add highest item in the matrix that is possible to get the highest value.
        const prevSumValue = knapsackMatrix[itemIndex - 1][weightIndex];
        const prevPrevSumValue = knapsackMatrix[itemIndex - 2][weightIndex];
        if (
          !prevSumValue
          || (prevSumValue && prevPrevSumValue !== prevSumValue)
        ) {
          this.selectedItems.push(prevItem);
        }
      } else if (knapsackMatrix[itemIndex - 1][weightIndex - currentItem.weight]) {
        this.selectedItems.push(prevItem);
        weightIndex -= currentItem.weight;
      }

      itemIndex -= 1;
    }
  }


  // Solve unbounded knapsack problem.
  // Greedy approach.
  solveUnboundedKnapsackProblem() {
    this.sortPossibleItemsByValue();
    this.sortPossibleItemsByValuePerWeightRatio();

    for (let itemIndex = 0; itemIndex < this.possibleItems.length; itemIndex += 1) {
      if (this.totalWeight < this.weightLimit) {
        const currentItem = this.possibleItems[itemIndex];

        // Detect how much of current items we can push to knapsack.
        const availableWeight = this.weightLimit - this.totalWeight;
        const maxPossibleItemsCount = Math.floor(availableWeight / currentItem.weight);

        if (maxPossibleItemsCount > currentItem.itemsInStock) {
          // If we have more items in stock then it is allowed to add
          // let's add the maximum allowed number of them.
          currentItem.quantity = currentItem.itemsInStock;
        } else if (maxPossibleItemsCount) {
          // In case if we don't have specified number of items in stock
          // let's add only items we have in stock.
          currentItem.quantity = maxPossibleItemsCount;
        }

        this.selectedItems.push(currentItem);
      }
    }
  }

  get totalValue() {
    /** @var {KnapsackItem} item */
    return this.selectedItems.reduce((accumulator, item) => {
      return accumulator + item.totalValue;
    }, 0);
  }

  get totalWeight() {
    /** @var {KnapsackItem} item */
    return this.selectedItems.reduce((accumulator, item) => {
      return accumulator + item.totalWeight;
    }, 0);
  }
}
```

