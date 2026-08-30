# 064: two searches, one ranking

builds on: [063](./063-the-search-that-understands-nothing.md), [062](./062-when-you-and-the-doc-use-different-words.md), [013](./013-cosine-similarity.md)
arc: giving the model your data (9 of 15), ~2 min

063 left two ranked lists and neither one is the list you want. merging them sounds like a one liner. it isnt, and the reason is the numbers.

```
you type:  "whats the deadline to claim a Nova expense?"

  by meaning (013)                  by literal words (063)
  1  policies/deadlines.md  0.74     1  onboarding/tools.md    8.2
  2  handbook/expenses.md   0.71     2  handbook/expenses.md   6.4
  3  handbook/refunds.md    0.69     3  handbook/refunds.md    2.1

  0.71 and 6.4 measure different things. adding them means nothing.
```

so throw the scores away and keep the positions. every list can tell you 1st, 2nd, 3rd, and that part compares. the name for it is reciprocal rank fusion, which is one over the rank, added up.

| chunk | meaning | words | 1/(3+rank), each | total |
| --- | --- | --- | --- | --- |
| handbook/expenses.md | 2 | 2 | 1/5 + 1/5 | 0.40 |
| handbook/refunds.md | 3 | 3 | 1/6 + 1/6 | 0.33 |
| policies/deadlines.md | 1 | not in top 3 | 1/4 + 0 | 0.25 |
| onboarding/tools.md | not in top 3 | 1 | 0 + 1/4 | 0.25 |

expenses.md is the doc that answers you. it won neither list. it came second in both, and that was enough.

the 3 in the denominators is a fudge constant and its doing real work. without it, first place scores a flat 1.0 and a chunk thats second in both only ties it. real code usually uses 60, same idea, flatter.

i expected to need a weighted average, some number i tune per query. no. sum one over rank and youre done, its about ten lines.

one honest thing you give up. rank 1 might have been miles clear or a hair ahead, and after this you cant tell. the merged list is roughly right, the order inside it is mush. 065 is the fix.
