# BaseCase

`BaseCase(B, S)` handles BMSSP when the recursion level reaches zero.

## Role

At the bottom of the recursion, the algorithm stops splitting the problem and solves the local bounded search directly.

```text
if l = 0:
    return BaseCase(B, S)
```

## Educational Sketch

```text
function BaseCase(boundary, sources):
    queue = priority queue initialized with sources
    completed = empty set

    while queue is not empty:
        u = queue.extract_min()

        if distance[u] >= boundary:
            return distance[u], completed

        mark u complete
        completed.add(u)

        if completed is large enough:
            return distance[u], completed

        for each edge (u, v):
            if distance[u] + weight(u, v) improves distance[v]:
                update distance[v]
                queue.insert_or_decrease_key(v)

    return boundary, completed
```

## Why It Exists

The base case gives recursion a concrete stopping point. It also keeps the most local work simple and direct.

The exact base case in the paper should be used for formal analysis. This file is an explanatory sketch.
