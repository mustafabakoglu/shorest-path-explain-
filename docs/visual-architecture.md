# Visual Architecture

BMSSP is easiest to understand as a machine made of five interacting parts.

```mermaid
flowchart TD
    A["Complete source set S"] --> B["FindPivots"]
    B --> C["Bounded data structure D"]
    C --> D["Pull distance slice"]
    D --> E["Recursive BMSSP call"]
    E --> F["Edge relaxation"]
    F --> G["Candidate classification"]
    G --> H["BatchPrepend / Insert"]
    H --> C
```

## Component 1: Source Set

The source set `S` contains vertices whose distances are already trusted.

```mermaid
graph LR
    S1((s1)) --> A((A))
    S2((s2)) --> B((B))
    S3((s3)) --> C((C))
```

## Component 2: Boundary

The boundary `B` limits the current problem.

```text
Active region = vertices x where d[x] < B
```

## Component 3: Pivots

Pivots summarize useful frontier points.

```mermaid
graph TD
    S["Sources"] --> F["Frontier"]
    F --> P1["Pivot p1"]
    F --> P2["Pivot p2"]
    F --> P3["Pivot p3"]
```

## Component 4: Queue Slices

The bounded queue groups candidate vertices by distance ranges.

```mermaid
flowchart LR
    A["[0, 5)"] --> B["[5, 9)"]
    B --> C["[9, 13)"]
    C --> D["Boundary B"]
```

## Component 5: Recursive Calls

Each recursive call solves a smaller bounded problem.

```mermaid
flowchart TD
    A["BMSSP(l, B, S)"] --> B["BMSSP(l-1, B1, S1)"]
    A --> C["BMSSP(l-1, B2, S2)"]
    B --> D["BMSSP(l-2, B3, S3)"]
    C --> E["BMSSP(l-2, B4, S4)"]
```
