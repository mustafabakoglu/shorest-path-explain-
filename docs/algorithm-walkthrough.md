# BMSSP Algorithm Walkthrough

This file explains the academic BMSSP pseudocode block by block.

## Interface

```text
BMSSP(l, B, S)
```

Inputs:

| Symbol | Meaning |
|---|---|
| `l` | Recursion level |
| `B` | Distance boundary |
| `S` | Complete source vertices |

Outputs:

| Symbol | Meaning |
|---|---|
| `B'` | Returned boundary, with `B' <= B` |
| `U` | Vertices completed by this call |

## Mental Model

Think of BMSSP as a bounded frontier machine:

```mermaid
flowchart LR
    Sources["Complete sources S"] --> Region["Region below B"]
    Region --> Pivots["Find pivots"]
    Pivots --> Queue["Bounded queue D"]
    Queue --> Recursive["Recursive slices"]
    Recursive --> Completed["Completed vertices U"]
```

It does not try to finalize every vertex in one global sweep. It repeatedly opens smaller windows.

## Step 1: Check The Level

```text
if l = 0 then
    return BaseCase(B, S)
```

At level zero, the algorithm stops decomposing and solves the small bounded problem directly.

Why:

- There is no lower recursion level.
- The overhead of pivoting and batching would no longer be useful.

## Step 2: Find Pivots

```text
P, W <- FindPivots(B, S)
```

`P` is a set of pivot vertices. `W` is a witness-like set used later when returning completed vertices.

Why:

- BMSSP needs a smaller set of representatives.
- Pivots help control how many sources enter the next layer of recursion.

## Step 3: Initialize The Data Structure

```text
D.Initialize(M, B)
M = 2^((l - 1)t)
D.Insert((x, d[x])) for x in P
```

The data structure `D` stores candidates by tentative distance, but only below the boundary `B`.

Why:

- BMSSP needs priority behavior.
- It also needs bounded and batched operations.

## Step 4: Pull A Slice

```text
B_i, S_i <- D.Pull()
```

`Pull` returns:

- a boundary `B_i`,
- and a source set `S_i` for a recursive subproblem.

Why:

- The next recursive call should work on a controlled distance interval.
- Pulling a slice gives the algorithm a smaller problem with a new boundary.

## Step 5: Recurse

```text
B'_i, U_i <- BMSSP(l - 1, B_i, S_i)
U <- U union U_i
```

The child call completes some vertices `U_i` below its returned boundary.

Why:

- The algorithm builds shortest path knowledge bottom-up.
- Parent calls use child-completed vertices for edge relaxation.

## Step 6: Relax Edges

```text
for edge (u, v) where u in U_i:
    if d[u] + w_uv <= d[v]:
        d[v] <- d[u] + w_uv
```

This is the same core idea as Dijkstra: every completed vertex may improve its neighbors.

Why:

- Shortest path algorithms discover better paths through relaxation.
- BMSSP changes scheduling, not the mathematical meaning of relaxation.

## Step 7: Classify Updated Vertices

```text
if d[u] + w_uv in [B_i, B):
    D.Insert((v, d[u] + w_uv))
else if d[u] + w_uv in [B'_i, B_i):
    K <- K union {(v, d[u] + w_uv)}
```

Updated vertices are separated by distance range:

| Range | Action |
|---|---|
| `[B_i, B)` | Future work for `D` |
| `[B'_i, B_i)` | Current/local slice candidate |
| Outside active ranges | No immediate queue action |

Why:

- Vertices in different distance windows belong to different parts of the recursive schedule.

## Step 8: Batch Prepend

```text
D.BatchPrepend(K union {(x, d[x]) : x in S_i and d[x] in [B'_i, B_i)})
```

This pushes newly relevant local candidates back into the front of the bounded structure.

Why:

- A child call may refine the lower boundary.
- Candidates that now belong to the refined interval should be processed soon.

## Step 9: Return

```text
return B' <- min{B'_i, B}
       U <- U union {x in W : d[x] < B'}
```

The call returns a refined boundary and a completed set.

Why:

- Parent calls need a clean summary.
- The returned set must preserve the correctness invariant expected by higher recursion levels.
