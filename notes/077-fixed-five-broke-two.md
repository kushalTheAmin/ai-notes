# 077: the change that fixed five things and broke two

builds on: [076](./076-the-score-moved-is-it-real.md), [072](./072-the-same-questions-every-run.md)
arc: evals, how you know any of it works (7 of 11), ~2 min

076 left prompt B at 44/50 against A at 41, and i wanted to ship it. heres what that +3 is actually made of.

```
$ evals diff  runs/prompt-A.json  runs/prompt-B.json    # same 50 rows (072)

  grounded    A 41/50  ->  B 44/50     +3

  fixed   #15  fail -> pass
          #23  fail -> pass
          #31  fail -> pass
          #38  fail -> pass
          #45  fail -> pass

  broke   #7   pass -> fail    <- this one flipped by itself in 076 too
          #22  pass -> fail    <- new. answer cites a doc i never sent

  5 fixed, 2 broke.  the headline showed me neither, only 5 - 2.

(numbers made up, the shape is the point)
```

the score is a sum, and a sum has no memory of which rows built it. five rows got better, two got worse, and the only thing that reached me was the difference between those counts.

#22 is the one that would have shipped. it passed on the old prompt, my new instruction broke it, nothing threw. and a row thats failing now but wasnt failing last run never gets read, because you only read the list.

i kept waiting for the aggregate to warn me. it cant. +3 and "five fixed, two broke" are the same number.

so i read eval runs the way i read a pull request now, the diff and not the summary line. same 50 rows from 072, and you look at which ids moved and which direction.

one catch. #7 is the row that flipped on its own back in 076 with nothing changed, so finding it in the broke list proves nothing. re-run that row on both prompts a few times before you call it a regression. #22 broke every time, thats why i believe that one.
