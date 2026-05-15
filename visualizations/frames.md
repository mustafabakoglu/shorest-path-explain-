# Animation Frames

## Frame Checklist

| Frame | Visual |
|---:|---|
| 1 | Graph appears with weighted directed edges |
| 2 | Complete source set `S` highlighted |
| 3 | Boundary `B` appears |
| 4 | Reachable region below `B` is shaded |
| 5 | Pivots `P` are selected |
| 6 | Pivots move into bounded queue `D` |
| 7 | `D.Pull()` emits `B_i, S_i` |
| 8 | Recursive call box opens |
| 9 | Completed set `U_i` returns |
| 10 | Edges from `U_i` relax neighbors |
| 11 | Candidates split into future insertions and local prepends |
| 12 | Parent call returns `B'` and `U` |
