# BMSSP Academic Pseudocode

This is a clean educational transcription of the BMSSP structure shown in the paper-style pseudocode. It is not executable code.

```text
function BMSSP(l, B, S)
    requirement 1:
        |S| <= 2^(l t)

    requirement 2:
        for every incomplete vertex x with d[x] < B,
        the shortest path to x visits some complete vertex y in S

    returns:
        boundary B' <= B
        set U

    if l = 0 then
        return B', U <- BaseCase(B, S)

    P, W <- FindPivots(B, S)

    D.Initialize(M, B) with M = 2^((l - 1)t)
    D.Insert((x, d[x])) for x in P

    i <- 0
    B'_0 <- min_{x in P} d[x]
    U <- empty set

    while |U| < k 2^(l t) and D is non-empty do
        i <- i + 1

        B_i, S_i <- D.Pull()

        B'_i, U_i <- BMSSP(l - 1, B_i, S_i)

        U <- U union U_i

        K <- empty set

        for edge e = (u, v) where u in U_i do
            if d[u] + w_uv <= d[v] then
                d[v] <- d[u] + w_uv

                if d[u] + w_uv in [B_i, B) then
                    D.Insert((v, d[u] + w_uv))

                else if d[u] + w_uv in [B'_i, B_i) then
                    K <- K union {(v, d[u] + w_uv)}

        D.BatchPrepend(
            K union {(x, d[x]) : x in S_i and d[x] in [B'_i, B_i)}
        )

    return B' <- min{B'_i, B}
           U <- U union {x in W : d[x] < B'}
```

## Notes

- If the pivot set `P` is empty, the boundary initialization is handled specially in the paper.
- `D` refers to the bounded data structure used by the algorithm.
- `t` and `k` are parameters chosen in the full algorithmic analysis.
- The comparison `<=` in relaxation follows the displayed pseudocode; implementations may handle ties according to their own predecessor-tracking policy.
