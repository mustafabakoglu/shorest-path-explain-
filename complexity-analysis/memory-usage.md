# Memory Usage

BMSSP-style algorithms need memory for both graph data and recursive state.

## Core Storage

| Structure | Purpose |
|---|---|
| Adjacency lists | Store outgoing edges |
| Distance array `d` | Store tentative shortest path values |
| Complete/incomplete markers | Track algorithm state |
| Bounded data structure `D` | Store active frontier candidates |
| Pivot set `P` | Store selected representatives |
| Witness set `W` | Store vertices found by pivot discovery |
| Completed set `U` | Store vertices completed by a call |
| Temporary set `K` | Store local candidates for batch prepend |

## Practical Educational Implementation

For a simple implementation, memory would usually look like:

```text
O(n + m + frontier storage + recursion state)
```

The graph itself often dominates:

```text
adjacency list size = O(n + m)
```

## Recursion State

Each recursive level may store:

- its boundary,
- its source set,
- local completed vertices,
- local queue state,
- and temporary candidates.

This is one reason practical implementations need careful engineering.
