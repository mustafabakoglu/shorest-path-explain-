# BMSSP Beginner Pseudocode

This version is intentionally simplified. It is for learning the shape of the algorithm, not proving the theorem.

```text
function BeginnerBMSSP(level, boundary, sources):
    if level == 0:
        return solve_small_bounded_problem(boundary, sources)

    pivots, witnesses = find_useful_frontier_vertices(boundary, sources)

    queue = new bounded_queue(boundary)
    queue.insert_all(pivots)

    completed = empty set
    best_boundary = boundary

    while queue is not empty and completed is not too large:
        slice_boundary, slice_sources = queue.pull_next_slice()

        child_boundary, child_completed =
            BeginnerBMSSP(level - 1, slice_boundary, slice_sources)

        completed.add_all(child_completed)
        best_boundary = min(best_boundary, child_boundary)

        local_candidates = empty set

        for each completed vertex u in child_completed:
            for each outgoing edge (u, v):
                new_distance = distance[u] + weight(u, v)

                if new_distance improves distance[v]:
                    distance[v] = new_distance

                    if new_distance belongs to a future slice:
                        queue.insert(v)
                    else if new_distance belongs to the current slice:
                        local_candidates.add(v)

        queue.batch_prepend(local_candidates)

    completed.add_all(witnesses that are safely below best_boundary)
    return best_boundary, completed
```

## Five-Word Summary

```text
Split -> Queue -> Recurse -> Relax -> Merge
```

## What Was Removed?

This beginner version hides:

- exact `k` and `t` parameter bounds,
- formal source-set invariants,
- exact pivot selection criteria,
- exact data structure guarantees,
- and proof-level boundary cases.
