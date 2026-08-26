# 020: finding the groups nobody labeled

builds on: [019](./019-near-duplicates-and-a-threshold.md), [018](./018-classify-with-no-training.md), [013](./013-cosine-similarity.md)
arc: meaning as numbers (10 of 11), ~2 min

018 and 019 both took something hand-written from me. one example sentence per label, then thirty pairs i scored myself. either way i already knew what the buckets were. this is the other case. 500 support tickets, nobody sorted them, and the question is what people are even complaining about.

```
500 ticket arrays, no labels. i want 3 groups

centers = the arrays of 3 tickets picked at random

loop:

  # assign
  for each ticket:
    group = the center it scores highest against   # 013's cosine

  # move
  for each group:
    center = average of its arrays, slot by slot
      [0.2, 0.9]
      [0.4, 0.7]
      -> [0.3, 0.8]

  stop when nobody switched groups
```

two steps, and only one is new. assign is 013's cosine against each center, keep the best, thats 018's max() again. move is plain averaging, slot 1 with slot 1, slot 2 with slot 2, and the center lands in the middle of whatever ended up in that group.

then it just loops. tickets pick their closest center, centers slide toward whoever picked them, that pulls a few more over and shakes a few loose. after a handful of rounds nothing switches and youre done. read five tickets out of a group and you can name it yourself. i kept waiting for the clever part, it never showed up. the word for this is clustering, the loop is k-means, and the k is the number of groups you ask for. every library has it.

heres what got me though. the 3 is mine. i picked it before seeing a single group. 019 made me hand-pick a threshold and this one doesnt need one, it wants a count instead. same hand, different number. and it hands you exactly 3 groups whether or not your tickets have 3 topics in them.
