# Complexity Overview

BMSSP appears in a theoretical shortest path framework whose reported full-algorithm running time is:

```text
O(m log^(2/3) n)
```

for directed graphs with non-negative real edge weights under the assumptions and model of the paper.

## Symbols

| Symbol | Meaning |
|---|---|
| `n` | Number of vertices |
| `m` | Number of edges |
| `l` | BMSSP recursion level |
| `B` | Current distance boundary |
| `S` | Source set |
| `P` | Pivot set |
| `U` | Completed set |

## Why Dijkstra Has A Sorting Flavor

Dijkstra repeatedly extracts the smallest tentative distance from a priority queue.

With common theoretical heaps, the classical bound is often written:

```text
O(m + n log n)
```

The `n log n` term reflects the cost of maintaining global order over vertices.

## Why BMSSP Is Different

BMSSP avoids organizing the entire unsettled frontier as one flat sorted set. It instead uses:

- distance boundaries,
- recursive slices,
- pivot-controlled source sets,
- and batched queue operations.

The goal is to pay for enough ordering to make progress, without paying for unnecessary global ordering at every step.

## Complexity Responsibilities By Component

| Component | Complexity role |
|---|---|
| `FindPivots` | Keeps recursive source sets controlled |
| `D.Initialize` | Creates bounded queue capacity for the level |
| `D.Pull` | Extracts a structured slice instead of one vertex |
| Recursive call | Solves a smaller bounded problem |
| Relaxation loop | Charges work to outgoing edges of newly completed vertices |
| `BatchPrepend` | Groups local queue updates |

## Why The Analysis Is Hard

The complexity proof must show that:

- recursive calls do not multiply work too much,
- pivot selection does not miss required vertices,
- every important relaxation is eventually processed,
- boundaries preserve correctness,
- and data structure operations remain within the promised total cost.

That is why BMSSP is considered advanced: the algorithm and proof are tightly coupled.
