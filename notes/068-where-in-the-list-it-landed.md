# 068: recall throws away where it landed

builds on: [067](./067-did-the-right-chunk-come-back.md), [064](./064-two-searches-one-ranking.md)
arc: giving the model your data (13 of 15), ~2 min

067 ended on a complaint i had no fix for. rank 1 and rank 9 both count as a plain yes. mrr is the fix, and its one line of arithmetic.

```
question           came back at   recall@10    mrr
key rotation             1           yes       1/1 = 1.0
refund window            4           yes       1/4 = 0.25
single sign-on           9           yes       1/9 = 0.11
delete account         miss           no             0

recall@10 = 3 of 4 hit                        = 0.75
mrr       = (1.0 + 0.25 + 0.11 + 0) / 4       = 0.34
```

same four questions from 067, same ranks, nothing rerun. instead of yes or no you score one over the rank the right chunk came back at. rank 9 barely registers, a miss scores 0. average the four and thats mean reciprocal rank.

you have met one over a rank already, 064 used it to merge two ranked lists. same arithmetic, different job.

what got me is how far apart the two numbers land on identical data. recall says 0.75, mrr says 0.34, and neither is wrong. recall asks did it come back at all. mrr asks did it come back near the top. i had been reading mrr as a stricter recall. its a different question.

one honest limit. mrr only looks at the first right chunk, so a question needing three still scores a perfect 1.0 if one lands at rank 1.

both numbers stop at the chunk though. neither has opened the answer yet.
