[Home](../../README.md) | [Dynamic Programming](../theories/dynamic-programming.md)

# All Pair Shortest Path (Floyd Warshall Algorithm)

Given a weighted graph, find the shortest paths between all pairs of nodes in it.

## Given

Adjacency matrix representation of the graph.

## Procedure

- Consider each vertex as an intermediate vertex and recalculate the adjacency matrix using this formula.

  $A^k[i, j] = min(A^k-1[i, j], A^k-1[i, k] + A^k-1[k, j])$

  - In each step, the $kth$ row and columns and the diagonal can be copied from the previous matrix.

- Repeat this process until all intermediate vertices are covered.

## Simulation

### Given

|       | 1   | 2       | 3       | 4       |
| ----- | --- | ------- | ------- | ------- |
| **1** | 0   | 3       | &infin; | 7       |
| **2** | 8   | 0       | 2       | &infin; |
| **3** | 5   | &infin; | 0       | 1       |
| **4** | 2   | &infin; | &infin; | 0       |

#### Via 1

|       | 1   | 2   | 3       | 4   |
| ----- | --- | --- | ------- | --- |
| **1** | 0   | 3   | &infin; | 7   |
| **2** | 8   | 0   | 2       | 15  |
| **3** | 5   | 8   | 0       | 1   |
| **4** | 2   | 5   | &infin; | 0   |

#### Via 2

|       | 1   | 2   | 3   | 4   |
| ----- | --- | --- | --- | --- |
| **1** | 0   | 3   | 5   | 7   |
| **2** | 8   | 0   | 2   | 15  |
| **3** | 5   | 8   | 0   | 1   |
| **4** | 2   | 5   | 7   | 0   |

#### Via 3

|       | 1   | 2   | 3   | 4   |
| ----- | --- | --- | --- | --- |
| **1** | 0   | 3   | 5   | 6   |
| **2** | 7   | 0   | 2   | 3   |
| **3** | 5   | 8   | 0   | 1   |
| **4** | 2   | 5   | 7   | 0   |

#### Via 4

|       | 1   | 2   | 3   | 4   |
| ----- | --- | --- | --- | --- |
| **1** | 0   | 3   | 5   | 6   |
| **2** | 5   | 0   | 2   | 3   |
| **3** | 3   | 6   | 0   | 1   |
| **4** | 2   | 5   | 7   | 0   |
