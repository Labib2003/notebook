[Home](../../README.md) | [Greedy Method](../theories/greedy-method.md)

# Fractional Knapsack

Given a set of items with their weights and profits and a maximum weight, the task is to find the maximum profit that can be obtained from the items using the given capacity.

## Given

- No of items `n`
- Capacity `m`
- Set of weights `w1, w2, ... wn`
- Set of profits `p1, p2, ... pn`

## Procedure

- Sort the items based on their profit / weight ratio.
- Keep taking the items with the highest profit / weight ratio until the capacity is reached (fractions allowd).

## Simulation

```
n = 5
m = 10
p = {12, 32, 40, 30, 50}
w = {4, 8, 2, 6, 1}
```

| Item | Profit | Weight | Profit/Weight |
| ---- | ------ | ------ | ------------- |
| 1    | 12     | 4      | 3             |
| 2    | 32     | 8      | 4             |
| 3    | 40     | 2      | 20            |
| 4    | 30     | 6      | 5             |
| 5    | 50     | 1      | 50            |

The sorted order: [5, 3, 4, 2, 1]

**Solution**:

| Item | Weight Taken (x<sub>i</sub>) | Remaining Space | Profit Gained (p<sub>i</sub>x<sub>i</sub>) |
| ---- | ---------------------------- | --------------- | ------------------------------------------ |
| 5    | 1/1                          | 10 - 1 = 9      | 50                                         |
| 3    | 2/2                          | 9 - 2 = 7       | 40                                         |
| 4    | 6/6                          | 7 - 6 = 1       | 30                                         |
| 2    | 1/8                          | 1 - 1 = 0       | (1/8)\*32 = 4                              |
|      |                              |                 | Total = 124                                |

**Max Profit** = 124

**Optimal Solution Set**: {0, 1/8, 1, 1, 1}

## Code

```cpp
#include <bits/stdc++.h>
using namespace std;

typedef struct Item {
  int no, weight, profit;
} Item;

vector<Item> items;

bool compareItems(Item a, Item b) {
  //    a1.p / a1.w > a2.p / a2.w
  // => a1.p * a2.w > a2.p / a1.w
  return a.profit * b.weight > b.profit * a.weight;
}

int main() {
  int n, capacity;
  double  profit = 0;

  printf("Enter the number of items and capacity: ");
  cin >> n >> capacity;

  for (int i = 0; i < n; i++) {
    int w, p;
    printf("Enter the weight and profit of item %d: ", i + 1);
    cin >> w >> p;
    items.push_back({i, w, p});
  }

  sort(items.begin(), items.end(), compareItems);

  printf("Items taken:\n");
  for (Item &item : items) {
    int taken = min(capacity, item.weight);

    double fraction_taken = (double)taken / item.weight;

    profit += item.profit * fraction_taken;
    capacity -= taken;

    printf("Item %d: %lf unit(s)\n", item.no + 1, fraction_taken);
  }

  printf("Profit: %lf\n", profit);

  return 0;
}
```

### IO

```
Enter the number of items and capacity: 3 50
Enter the weight and profit of item 1: 10 60
Enter the weight and profit of item 2: 20 100
Enter the weight and profit of item 3: 30 120
Items taken:
Item 1: 1.000000 unit(s)
Item 2: 1.000000 unit(s)
Item 3: 0.666667 unit(s)
Profit: 240.000000
```
