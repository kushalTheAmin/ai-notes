# 076: the score moved, is it real

builds on: [075](./075-where-the-judge-tilts.md), [072](./072-the-same-questions-every-run.md), [041](./041-same-prompt-two-answers.md)
arc: evals, how you know any of it works (6 of 11), ~2 min

075 ended on a score that stopped moving because nearly everything passed. this is the other way the number lies. it moves when nothing changed.

before you trust any gap, run the old prompt a second time. same 50 rows from 072, same prompt, same everything.

```
prompt A, run twice, nothing touched between them

  run 1    grounded 41/50    82%
  run 2    grounded 43/50    86%

  rows that moved:   #7   pass -> fail
                     #12  fail -> pass
                     #29  fail -> pass
                     #44  fail -> pass

  4 rows moved. net +2 answers. i changed nothing.

then the comparison i actually cared about

  prompt A  41/50   82%    (or 86%, run 2 was just as real)
  prompt B  44/50   88%

(numbers made up. the shape is the point)
```

four rows flipped on their own, and thats just 041 arriving in arc 7. same prompt, different text, and groundedness (069) reads that text.

out of 50, one answer is worth 2 points. thats the smallest thing this score can ever say.

then B comes in at 88 and i wanted to ship it. +6 sounds like a real move. its 3 answers. against run 2 of the same prompt A its 1, and 4 rows moved with nothing changed at all.

that doesnt mean B is no better. it means these 50 rows cant tell me. run each side a few times and look at the spread, or grow the file until one answer stops being worth 2 points.

the other thing in that list is #7, a row that went from pass to fail. real changes do that too, and a net win with a quiet loss buried in it is 077.
