# BMSSP Animation Storyboard

## Scene 1: Start With Sources

Show several complete vertices highlighted in green.

Text overlay:

```text
BMSSP begins from a set of complete sources S.
```

## Scene 2: Draw Boundary

Draw a distance ring labeled `B`.

Text overlay:

```text
Only vertices below boundary B are active.
```

## Scene 3: Select Pivots

Highlight a subset of frontier vertices as pivots.

Text overlay:

```text
Pivots summarize useful frontier regions.
```

## Scene 4: Pull Queue Slice

Show candidates grouped into distance buckets. Pull the nearest active slice.

Text overlay:

```text
The bounded structure D returns the next recursive slice.
```

## Scene 5: Recurse

Zoom into the selected slice.

Text overlay:

```text
BMSSP solves a smaller bounded problem.
```

## Scene 6: Relax And Merge

Show outgoing edges updating neighbors, then candidates re-entering the queue.

Text overlay:

```text
Relax improved edges, then merge candidates back into D.
```
