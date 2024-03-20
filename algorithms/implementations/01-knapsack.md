[Home](../../README.md) | [Dynamic Programming](../theories/dynamic-programming.md)

# 0/1 Knapsack

## Overview

Given N items where each item has some weight and profit associated with it and also given a bag with capacity M. The task is to put the items into the bag such that the sum of profits associated with them is the maximum possible.

## Given

- No of items `n`
- Capacity `m`
- Set of weights `w1, w2, ... wn`
- Set of profits `p1, p2, ... pn`

## Procedure

1. Initialize a table b of dimensions (n+1) by (m+1).
2. Set the values in the 0th row and column of the table to 0.
3. For each row (n<sub>i</sub>):
   1. Navigate to the corresponding weight column (m<sub>j</sub>) and copy values from the previous row up to that point.
   2. For subsequent columns, calculate the value using the formula:
      ```
      b[i, w] = max(b[i - 1, w], b[i - 1, w - weight[i]] + p[i])
      ```
4. The bottom right corner of the table now holds the maximum profit.
5. To identify the optimal items, employ backtracking:

   1. Begin from the bottom right corner and check if the current value matches the one in the previous row:
      1. If true, exclude the corresponding item and move to the previous row.
      2. If false, select the item, deduct its profit from the current value, and search for the result in the previous row (consider this as the new column).
   2. Repeat this process until reaching the top left corner.

## Simulation

```
n = 3
m = 6
w = [2, 3, 4]
p = [1, 2, 5]
```

|       | 0   | 1   | 2   | 3   | 4   | 5   | 6   |
| ----- | --- | --- | --- | --- | --- | --- | --- |
| **0** | 0   | 0   | 0   | 0   | 0   | 0   | 0   |
| **1** | 0   | 0   | 1   | 1   | 1   | 1   | 1   |
| **2** | 0   | 0   | 1   | 2   | 2   | 3   | 3   |
| **3** | 0   | 0   | 1   | 2   | 5   | 5   | 6   |

**Max profit** = 6

**Optimal items**:

| Item 1 | Item 2 | Item 3 |
| ------ | ------ | ------ |
| 1      | 0      | 1      |

## Code

```cpp
#include <bits/stdc++.h>
using namespace std;

int knapsack(int capacity, int weight[], int profit[], int n) {
  int dp_table[n + 1][capacity + 1];

  for (int i = 0; i <= n; i++) {
    // because we are adding an extra 0th item and 0 weight
    int idx = i - 1;
    for (int j = 0; j <= capacity; j++) {
      // Set the values in the 0th row and column of the table to 0
      if (i == 0 || j == 0)
        dp_table[i][j] = 0;

      // copy the value from the previous row up to the corresponding weight
      else if (j < weight[idx])
        dp_table[i][j] = dp_table[i - 1][j];

      // apply formula
      else
        dp_table[i][j] = max(dp_table[i - 1][j],
                             dp_table[i - 1][j - weight[idx]] + profit[idx]);
    }
  }
  // return bottom right corner
  return dp_table[n][capacity];
}

int main() {
  int n, capacity;

  printf("Enter the number of items and capacity: ");
  cin >> n >> capacity;

  int weight[n], profit[n];

  for (int i = 0; i < n; i++) {
    printf("Enter the profit and weight of item %d: ", i + 1);
    cin >> profit[i] >> weight[i];
  }

  printf("Maximum profit: %d\n", knapsack(capacity, weight, profit, n));

  return 0;
}
```

### IO

```
Enter the number of items and capacity: 3 50
Enter the profit and weight of item 1: 60 10
Enter the profit and weight of item 2: 100 20
Enter the profit and weight of item 3: 120 30
Maximum profit: 220

```
