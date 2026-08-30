# 090: jitter, or why everyone wakes up on the same tick

builds on: [089](./089-wait-then-double.md), [088](./088-two-meters.md)

arc: running it, speed, cost, and when things break (9 of 17), ~2 min

089s loop is fine when youre the only one running it. it breaks the moment four workers on the same api key get 429d on the same tick.

```
089s sleep line:  sleep(wait)
with jitter:      sleep(wait + random(0, wait))

4 workers, one api key, all 429 at t=0, all with wait = 1s

no jitter, everyone sleeps exactly 1.00s
  t=1.00   A B C D     four calls in one instant, the meter refuses most of them
  t=3.00   B C D       the refused ones doubled to 2s, still in lockstep

with jitter, everyone sleeps 1s plus a random slice of 1s
  t=1.12   A
  t=1.34   C
  t=1.79   B
  t=1.91   D
           same four calls, spread over 0.79s, arriving one at a time
```

they all picked the same wait because the loop is deterministic. one second, to the millisecond. so they wake together, land together, and the meter from 088 has not refilled enough for four at once. most get refused, double together, pile up again at t=3.00. the retry code is what keeps them in step. i did not see that coming, i read 089 with one client in my head the whole time.

the fix has a name, jitter. sleep the wait plus a random slice of it, so nobody agrees on when to wake. it costs you half a second more per attempt on average here, and the calls arrive spread out instead of stacked.

it still sleeps at least the full wait, so youre not retrying instantly, which 089 already ruled out. the random part only pushes clients apart, never pulls them earlier.

how many clients does your thing actually run? one script, skip it. background workers, or a react app where every open tab retries on its own, put the random in.
