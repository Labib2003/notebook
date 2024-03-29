[Home](../../README.md) | [Dynamic Programming](../theories/dynamic-programming.md)

# Optimal Binary Search Tree

Given a set of keys, successful and unsuccessful search probabilities, construct a BST with minimum possible total search cost.

## BST

A tree where for every node, all the nodes in the left subtree are less and all the nodes in the right subtree are greater than or equal value.

## Possible BSTs

For n keys, there are,

${2n_c}_n / (n + 1)$

valid BST combinations.

## Finding OBST using brute force

Generating all possible BSTs using brute force and comparing their cost.

## Finding OBST using DP

Finding the optimal root for a subset of keys and generate tree. To do this, we use tabulation method and find optimal roots of smaller subsets of keys and progressively calculate larger and larger subsets.

### Formula

```
c[i, j] = min{c[i, k - 1] + c[k, j]} + w[i, j]
where i < k <= j
```

For example, for 3 keys,

First we find the optimal root in the subsets of length 0, i.e. [0, 0], [1, 1], [2, 2], [3, 3] (j - i = 0).

Then we find the optimal root in the subsets of length 1, i.e. [0, 1], [1, 2], [2, 3] (j - i = 1).

Then we find the optimal root in the subsets of length 2, i.e. [0, 2], [1, 3] (j - i = 2).

Then we find the optimal root in the subsets of length 3, i.e. [0, 3] (j - i = 3) (this is our final root).

## Procedure

- Create a n + 1 x n + 1 table. We will record the sum of probabilities `w`, cost `c`, and optimal root `r` for each subset.
- Initiate the table by putting the default values in the first row:
  - w = q<sub>i</sub>
  - c = 0
  - r = 0
- For the rest, use these formulas:
  - w[i, j] = w[i, j - 1] + p<sub>j</sub> + q<sub>j</sub>
  - c[i, j] [Use this formula](#formula)
  - r[i, j] Is the value of j that produces the minimum cost.
- Only calculate the upper triangular part.

## Simulation

```
k = { , 10, 20, 30, 40}
p = { ,  3,  3,  1,  1} // successful search probability
q = {2,  3,  1,  1,  1} // unsuccessful search probability
```

### Table

| 0                                                                  | 1                                                                  | 2                                                                | 3                                                                | 4                                                                |
| ------------------------------------------------------------------ | ------------------------------------------------------------------ | ---------------------------------------------------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------- |
| w<sub>00</sub> = 2<br/>c<sub>00</sub> = 0<br/>r<sub>00</sub> = 0   | w<sub>11</sub> = 3<br/>c<sub>11</sub> = 0<br/>r<sub>11</sub> = 0   | w<sub>22</sub> = 1<br/>c<sub>22</sub> = 0<br/>r<sub>22</sub> = 0 | w<sub>33</sub> = 1<br/>c<sub>33</sub> = 0<br/>r<sub>33</sub> = 0 | w<sub>44</sub> = 1<br/>c<sub>44</sub> = 0<br/>r<sub>44</sub> = 0 |
| w<sub>01</sub> = 8<br/>c<sub>01</sub> = 8<br/>r<sub>01</sub> = 1   | w<sub>12</sub> = 7<br/>c<sub>12</sub> = 7<br/>r<sub>12</sub> = 2   | w<sub>23</sub> = 3<br/>c<sub>23</sub> = 3<br/>r<sub>23</sub> = 3 | w<sub>34</sub> = 3<br/>c<sub>34</sub> = 3<br/>r<sub>34</sub> = 4 |
| w<sub>02</sub> = 12<br/>c<sub>02</sub> = 19<br/>r<sub>02</sub> = 1 | w<sub>13</sub> = 9<br/>c<sub>13</sub> = 12<br/>r<sub>13</sub> = 2  | w<sub>24</sub> = 5<br/>c<sub>24</sub> = 8<br/>r<sub>24</sub> = 3 |
| w<sub>03</sub> = 14<br/>c<sub>03</sub> = 25<br/>r<sub>03</sub> = 2 | w<sub>14</sub> = 11<br/>c<sub>14</sub> = 19<br/>r<sub>14</sub> = 2 |
| w<sub>04</sub> = 16<br/>c<sub>04</sub> = 32<br/>r<sub>04</sub> = 2 |

### Example calculation

```
// after calculating until row 3
c[0, 4] = min{
            c[0, 0] + c[1, 4],
            c[0, 1] + c[2, 4],
            c[0, 2] + c[3, 4],
            c[0, 3] + c[4, 4]
        } + w[0, 4]
        = min{19, 16, 22, 25} + 16
        = 32 (minimum value, 16 came from j = 2. Optimal root in this subset is 2)
```

### Constructing the BST

Optimal root in subset 0 to 2 is 2.

So the left subtree will have keys 0 to 1 and the right subtree will have keys 3 to 4.

Optimal root in subset 0 to 1 is 1 and optimal root in subset 3 to 4 is 4.

Similarly, construct the rest of the tree.

```
  20
 /  \
10  30
      \
      40
```
