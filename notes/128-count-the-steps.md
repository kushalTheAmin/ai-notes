# 128: count the steps

builds on: [127](./127-grade-the-end-state.md), [126](./126-a-trace-not-a-log-line.md), [115](./115-one-round-itemized.md)
arc: agents you can trust (7 of 13), ~2 min

127 gives a finished run one bit, passed or not. a run can pass and still have been awful.

126 already writes the rounds and the tokens down, so you have both numbers. this is just adding them up per run.

```text
same task, 5 saved runs, every one of them passed

run 1     4 rounds     9,200 tokens
run 2     4 rounds     9,600 tokens
run 3     5 rounds    12,400 tokens
run 4     4 rounds     9,400 tokens
run 5    11 rounds    38,400 tokens

pass rate   5/5
median      4 rounds,   9,600 tokens
worst      11 rounds,  38,400 tokens   <- same score, 4x the tokens
```

run 5 passed. i wouldnt ship run 5. it wandered, re-read things, got there eventually. the pass rate cant see any of that, every row is a 1 to it.

now look at the two columns together. rounds go 4 to 11, under 3x. tokens go 4x. 115 said why, every round replays the whole history, so the bill climbs faster than the step count. if you want dollars, price that column out with [004](./004-tokens-are-money.md).

if you watch p95 on a dashboard at work, same read. the median is what this task normally costs, the worst run is a bad day, and the gap is where i go looking.

one catch, and it took me a minute to see it. push the token number down on its own and you get a run that quits early, cheap and wrong. it only means anything sitting next to the pass rate.
