[Home](../../README.md)

# Graph search

There are two ways to search for a node in a graph.

- Depth first search
- Breadth first search

## Depth first search (DFS)

In this method we emphasize on the edges of the graph. We start from the root and recursively visit all the nodes of a particular edge before moving to the next one. We use a stack and push the current node into it and mark it as visited, if it has any unvisited adjacent vertices, they are pushed. If there are none the node is popped.

## Breadth first search (BFS)

In this method we emphasize on the vertices of the graph. We start from the root and visit all the nodes in the same level before moving to the next one. We use a queue to store the adjacent nodes of a vertex before marking it visited and visit the next unvisited node in the queue.
