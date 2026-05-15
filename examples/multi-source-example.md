# Multi-Source Example

Suppose two emergency depots can reach a road network.

```mermaid
graph LR
    S1((Depot 1)) -- "3" --> A((A))
    S2((Depot 2)) -- "2" --> B((B))
    A -- "4" --> C((C))
    B -- "1" --> C
    C -- "2" --> D((D))
```

The distance to `C` is:

```text
min(distance from Depot 1 through A, distance from Depot 2 through B)
= min(3 + 4, 2 + 1)
= 3
```

So `Depot 2 -> B -> C` wins.

## BMSSP Connection

BMSSP receives a set `S` of complete vertices. These are like multiple trusted entry points into the next region.

```text
S = {Depot 1, Depot 2}
```

The algorithm then explores below a boundary:

```text
B = 6
```

Only vertices with distance less than `6` are relevant to that call.
