[Home](../../README.md)

# Dynamic Programming

Dynamic programming is an algorithm design method that can be used when the solution can be viewed as a sequence of decisions. It breaks the problem down to a series of **overlapping** sub-problems and builds up solutions to longer and longer sub-problems. At the end, it chooses the most optimal solution sequence as the final result.

## Optimization

DP often drastically reduces the amount of enumeration by avoiding sequences that cannot possibly be optimal using the principle of optimality.

## Examples

### 0/1 Knapsack:

This solution uses the Tabulation method.

**Given:**

- No of items `n`
- Capacity `m`
- Set of weights `w1, w2, ... wn`
- Set of profits `p1, p2, ... pn`

**Solution:**

1. Create a n+1\*m+1 table b.
2. Set the 0th row and column to 0.
3. For each row (n<sub>i</sub>):
   1. Go to the corresponding weight column (m<sub>j</sub>) and copy the values from the previous row until that point.
   2. For the next columns, put the value
      ```
      b[i, w] = max(b[i - 1, w], b[i - 1, w - w[i]] + p[i])
      ```
4. The bottom right corner of the table contains the maximum profit.
5. To construct the list of optimal items, we use backtracking:
   1. Start from the bottom right corner and check if the current value and the previous row value are the same:
      1. If so, we eliminate that item and move to the previous row.
      2. If not, we select that item, subtract its profit from the current value, and search for the result in the previous row (this becomes the new column).
   2. Repeat this process until we reach the top left corner.
