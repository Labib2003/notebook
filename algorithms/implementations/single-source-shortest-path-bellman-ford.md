[Home](../../README.md) | [Dynamic Programming](../theories/dynamic-programming.md)

# Single Source Shortest Path Using Bellman-Ford Algorithm

Given a graph and a source vertex, find the shortest path from the source vertex to all other vertices.

- This is similar to [Dijkstra's Algorithm](./single-source-shortest-path-dijkstra.md) but it also works for graphs with negative edge weights.

- This does NOT work if there is a negative total weight cycle in the graph.

## Procedure

- If there are `n` edges, perform [Relaxation](./single-source-shortest-path-dijkstra.md/#relaxation) on the vertices `n - 1` times.
