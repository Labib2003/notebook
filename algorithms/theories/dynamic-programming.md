[Home](../../README.md)

# Dynamic Programming

Dynamic programming is an algorithm design method that can be used when the solution can be viewed as a sequence of decisions. It breaks the problem down to a series of **overlapping** sub-problems and builds up solutions to longer and longer sub-problems. At the end, it chooses the most optimal solution sequence as the final result.

## Optimization

DP often drastically reduces the amount of enumeration by avoiding sequences that cannot possibly be optimal using the principle of optimality.

It states that an optimal solution to a problem can be constructed from optimal solutions to its subproblems. i.e. for a problem to have an optimal overall solution, each of its subproblems must also have optimal solutions.

## Techniques

### Memoization

It is a top down approach used to optimize recursive calls. It breaks the problem down to smaller subproblems and stores the results of them in a cache. If the same subproblem is encountered again (overlapping subproblems), it retrieves the results from the cache instead of recalculating it again.

### Tabulation

It is a bottom up approach used to optimize iterative calls. It breaks the problem into subproblems, stores their results in a table and iteratively builds the solution up to the larger problems.

## Problems and Algorithms

- [0/1 Knapsack](../implementations/01-knapsack.md)
- [Shortest Path in Multistage Graph](../implementations/multistage-graph.md)
- [Travelling Salesperson](../implementations/travelling-salesperson.md)
- [All Pair Shortest Path (Floyd Warshall Algorithm)](../implementations/all-pair-shortest-path-floyd-warshall.md)
