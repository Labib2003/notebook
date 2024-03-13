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
