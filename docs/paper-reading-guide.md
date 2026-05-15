# Paper Reading Guide

BMSSP can feel dense because it combines several ideas at once. Use this guide while reading the original paper.

## Before Reading BMSSP

Make sure you are comfortable with:

- Dijkstra's algorithm,
- priority queues,
- edge relaxation,
- graph adjacency lists,
- recursion,
- asymptotic notation,
- and invariants.

## What To Track

When reading the BMSSP pseudocode, track these questions:

| Question | Why it matters |
|---|---|
| Which vertices are complete? | Correctness depends on completed vertices having trusted distances |
| What is the active boundary? | The algorithm is bounded by `B` and returned `B'` |
| Why is this source set small? | The recursion requires source-set size control |
| Where do relaxed vertices go? | Queue placement determines future work |
| Why is a batch operation valid? | The complexity analysis relies on batched queue behavior |

## Suggested Reading Order

1. Read the theorem statement for the full SSSP result.
2. Skim the data structure lemma used by `D`.
3. Read `FindPivots`.
4. Read `BaseCase`.
5. Read BMSSP once for structure only.
6. Read BMSSP again and annotate every boundary interval.
7. Only then read the full complexity proof.

## Common Confusion Points

### BMSSP Is Not Plain Multi-Source Dijkstra

Multi-source Dijkstra starts a priority queue with many sources. BMSSP uses multiple sources, but also imposes boundaries, pivots, recursion levels, and batched queue updates.

### `B` And `B'` Are Not Decorative

The boundary controls which vertices are relevant. The returned boundary tells the caller how far the child call safely progressed.

### Pivots Are A Structural Tool

Pivots are not arbitrary samples. They are selected to preserve the recursive invariant and keep subproblem sizes controlled.
