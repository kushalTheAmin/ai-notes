# 033: temperature is one divide

builds on: [032](./032-raw-scores-arent-percentages.md)
arc: how it writes, and the knobs you own (2 of 9), ~2 min

032 ended on the gap. ghee beat time by 1.1 points of raw score and came out three times as likely. temperature is the knob that decides how much of that stretching happens, and it does it by dividing every score before the exp step runs.

```
temperature is one divide, on every score, before the exp step

T = 0.4   every score / 0.4, then the same softmax

  " ghee"    3.2 / 0.4 =  8.00   ->  93.6%
  " time"    2.1 / 0.4 =  5.25   ->   6.0%
  " water"   1.0 / 0.4 =  2.50   ->   0.4%
  " flour"  -0.4 / 0.4 = -1.00   ->   0.0%
                                     ------
                                     100.0%

T = 1.0   divide by 1, nothing moves, this is 032 exactly

  " ghee"    3.2 / 1.0 =  3.20   ->  68.0%
  " time"    2.1 / 1.0 =  2.10   ->  22.6%
  " water"   1.0 / 1.0 =  1.00   ->   7.5%
  " flour"  -0.4 / 1.0 = -0.40   ->   1.9%
                                     ------
                                     100.0%

T = 2.0   every score / 2, the scores squash together

  " ghee"    3.2 / 2.0 =  1.60   ->  48.2%
  " time"    2.1 / 2.0 =  1.05   ->  27.8%
  " water"   1.0 / 2.0 =  0.50   ->  16.0%
  " flour"  -0.4 / 2.0 = -0.20   ->   8.0%
                                     ------
                                     100.0%

(the -> is exp then divide by the total, exactly note 032, unchanged)
```

thats it. thats the whole knob. i expected more moving parts, a clever randomness dial maybe. its a divide. [017](./017-embedding-model-is-separate.md) had temperature sitting in a request json with me saying id get to it. this is it.

divide by a small number and the scores spread apart, so the leader runs away with it. at 0.4 ghee takes basically everything. a bigger divisor squashes them toward each other instead, and at 2.0 water has a real 16% shot.

took me a minute to catch this: the order never changes. the same positive divisor on every score cant reorder them, so ghee sits on top at every temperature. if whatever comes next always grabs the top row, temperature does nothing to your output.

check your providers range before copying a number off a blog post, some cap at 1, some go to 2.

nothing has been picked yet. 034 is the part that actually chooses.
