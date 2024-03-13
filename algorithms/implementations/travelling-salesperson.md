[Home](../../README.md) | [Dynamic Programming](../theories/dynamic-programming.md)

# Travelling Salesperson (TSP)

Given a graph of cities (vertices) and the distances between them (weighted edges), the problem is to find the shortest possible route that visits each city **exactly once** and returns to the starting city.

## Given

A graph in matrix or adjacency list form.

## Procedure

- Consider each city except the first one as the last city before returning home and calculate their distance.
- Keep calculating upwards using the formula until first city (root is reached).
- Generate the shortest path by taking the minimum value cities from the calculations.

Formula:

```
g(i, S) = min{c(i, k) + g(k, S - {k})}
          k∈S
```

## Simulation

Given:

|          | 1   | 2   | 3   | 4   |
| -------- | --- | --- | --- | --- |
| <b>1</b> | 0   | 2   | 3   | 4   |
| <b>2</b> | 1   | 0   | 5   | 4   |
| <b>3</b> | 15  | 7   | 0   | 8   |
| <b>4</b> | 6   | 3   | 12  | 0   |

```
(we have to calculate the distance at each stage and take the minmum)
        1
      / | \
     /  |  \
    /   |   \
   /    |    \
  2     3     4
 / \   / \   / \
3   4 2   4 2   3
|   | |   | |   |
1   1 1   1 1   1

```

For |S| = 0, i.e no remaining cities (4rd level of the tree)

```
g(2, Φ) = min{c(2, 1)} = 1
g(3, Φ) = min{c(3, 1)} = 15
g(4, Φ) = min{c(4, 1)} = 6
```

For |S| = 1, i.e one remaining city (3rd level of the tree)

```
g(2, {3}) = min{c(2, 3) + g(3, Φ)} = 5 + 15 = 20
g(2, {4}) = min{c(2, 4) + g(4, Φ)} = 4 + 6 = 10

g(3, {2}) = min{c(3, 2) + g(2, Φ)} = 7 + 1 = 8
g(3, {4}) = min{c(3, 4) + g(4, Φ)} = 8 + 6 = 14

g(4, {2}) = min{c(4, 2) + g(2, Φ)} = 3 + 1 = 4
g(4, {3}) = min{c(4, 3) + g(3, Φ)} = 12 + 15 = 27
```

For |S| = 2, i.e two remaining cities (2nd level of the tree)

```
g(2, {3, 4}) = min{
                    c(2, 3) + g(3, {4}),
                    c(2, 4) + g(4, {3}),
                } = min{5 + 14, 4 + 27} = 19

g(3, {2, 4}) = min{
                    c(3, 2) + g(2, {4}),
                    c(3, 4) + g(4, {2}),
                } = min{7 + 10, 8 + 4} = 12

g(4, {2, 3}) = min{
                    c(4, 2) + g(2, {3}),
                    c(4, 3) + g(3, {2}),
                } = min{3 + 20, 12 + 8} = 20
```

For |S| = 3, i.e one remaining city (root of the tree)

```
g(1, {2, 3, 4}) = min{
                        c(1, 2) + g(2, {3, 4}),
                        c(1, 3) + g(3, {2, 4}),
                        c(1, 4) + g(4, {2, 3}),
                    } = min{1 + 19, 9 + 12, 10 + 20} = 21
```

Therefore, the shortest distance is `21`.

And by taking the minimum distance at each stage, we get the shortest path.

```
1 → 2 → 3 → 4 → 1
or
1 → 3 → 4 → 2 → 1
```

## Code

Brute force solution:

```c++
#include <bits/stdc++.h>
using namespace std;

const int INFINITE = numeric_limits<int>::max();
const int MAX_SIZE = 10001;
int GRAPH[MAX_SIZE][MAX_SIZE];

// calculates the cost of the solution [a, b, c]
// like this, cost[a][b] + cost[b][c] + cost[c][a]
int tsp(int n, int solutions[]) {
  int cost = 0;

  for (int i = 0; i < n - 1; i++) {
    int u = solutions[i];
    int v = solutions[i + 1];
    cost += GRAPH[u][v];
  }

  cost += GRAPH[solutions[n - 1]][solutions[0]];

  return cost;
}

int main() {
  int minCost = INFINITE, vertexCount;

  // input
  do {
    printf("Enter the number of vertices (max = %d): ", MAX_SIZE - 1);
    cin >> vertexCount;
  } while (vertexCount >= MAX_SIZE);

  int solution[vertexCount + 1], optimalSolution[vertexCount + 1];

  printf("Enter the %d*%d adjacency matrix:\n", vertexCount, vertexCount);
  for (int i = 0; i < vertexCount; i++)
    for (int j = 0; j < vertexCount; j++)
      cin >> GRAPH[i][j];

  // initial solution i.e 0, 1, 2, 3...
  for (int i = 0; i < vertexCount; i++)
    solution[i] = i;

  // brute force:
  // iterate over all permutations of solution:
  //  if a new minimum cost is found:
  //    update minimum cost
  //    copy that permutation as the new optimal solution
  do {
    int cost = tsp(vertexCount, solution);
    if (cost < minCost) {
      minCost = cost;
      for (int i = 0; i < vertexCount; i++)
        optimalSolution[i] = solution[i];
    }
  } while (next_permutation(solution, solution + vertexCount));

  // output
  printf("Minimum cost: %d\n", minCost);

  printf("Optimal tour: ");
  printf("%d", optimalSolution[0] + 1);
  for (int i = 1; i < vertexCount; i++)
    printf("-->%d", optimalSolution[i] + 1);
  printf("-->%d\n", optimalSolution[0] + 1);

  return 0;
}
```
