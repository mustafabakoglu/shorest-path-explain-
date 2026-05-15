# Shortest Path Algorithm Family Table

| Algorithm | Graph type | Weights | Source model | Typical use |
|---|---|---|---|---|
| BFS | Unweighted | Unit weights | Single source | Intro graph traversal |
| Dijkstra | Directed or undirected | Non-negative | Single source | Practical weighted SSSP |
| Multi-source Dijkstra | Directed or undirected | Non-negative | Multiple sources | Nearest facility / frontier search |
| Bellman-Ford | Directed | Can handle negative edges if no negative cycle | Single source | Negative edge teaching baseline |
| DAG shortest paths | Directed acyclic | Can handle negative edges | Single source | Scheduling and acyclic dependency graphs |
| A* | Directed or undirected | Non-negative plus heuristic | Single pair | Pathfinding with admissible heuristic |
| BMSSP | Directed setting in the paper | Non-negative real weights | Multiple complete sources | Research-level SSSP subroutine |

This table is educational, not a full taxonomy of every shortest path algorithm.
