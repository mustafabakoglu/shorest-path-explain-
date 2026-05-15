# Glossary

| Term | Meaning |
|---|---|
| `B` | Upper distance boundary for a BMSSP call |
| `B'` | Returned refined boundary |
| `D` | Specialized bounded queue-like data structure |
| `d[x]` | Current tentative distance estimate for vertex `x` |
| Edge relaxation | Updating `d[v]` using `d[u] + w(u,v)` |
| Complete vertex | Vertex whose distance is treated as finalized within the algorithm invariant |
| Incomplete vertex | Vertex that may still receive a shorter distance |
| Pivot | A selected representative vertex used to control recursion |
| Source set `S` | Complete vertices used as the entry points to a BMSSP call |
| Witness set `W` | Auxiliary set returned by pivot discovery and used in final completion |
| `U` | Set of vertices completed by a BMSSP call |
| `K` | Temporary set of candidates for batch prepending |
| `l` | Recursion level |
| `t`, `k` | Paper parameters used to control sizes and bounds |
| SSSP | Single-source shortest paths |
| MSSP | Multi-source shortest paths |
