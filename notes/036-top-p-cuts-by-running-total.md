# 036: top-p cuts by running total, not by count

builds on: [035](./035-top-k-cuts-the-tail.md), [034](./034-greedy-vs-sampling.md)
arc: how it writes, and the knobs you own (5 of 13), ~2 min

035 ended on the bit that bugged me. k is a fixed count, the same count whether the model is dead certain or completely torn. top-p cuts somewhere else. dont count rows, add percentages down the list until the running total passes p, keep everything you touched, delete the rest.

```
p = 0.9   add percentages down the list, stop the moment the total passes p

PEAKED   the ghee list from 033, at temperature 1.0

  " ghee"     68.0%   total 0.680   past 0.9?  no
  " time"     22.6%   total 0.906   past 0.9?  yes, stop here
  " water"     7.5%   cut
  " flour"     1.9%   cut

  2 survivors, adding to 0.906
    0.680 / 0.906 = 75.1%      0.226 / 0.906 = 24.9%

FLAT   different sentence, the model has no favourite

  " dal"      28.0%   total 0.280   past 0.9?  no
  " khichdi"  26.0%   total 0.540   past 0.9?  no
  " rice"     24.0%   total 0.780   past 0.9?  no
  " roti"     16.0%   total 0.940   past 0.9?  yes, stop here
  " pasta"     6.0%   cut

  4 survivors, adding to 0.940
    0.280 / 0.940 = 29.8%      0.240 / 0.940 = 25.5%
    0.260 / 0.940 = 27.7%      0.160 / 0.940 = 17.0%

same p on both. 2 rows survive, then 4.
(flat list made up, the arithmetic is real)
```

the walk is 034s loop and the divide at the end is 035s rescale, so nothing in the mechanics is new. the new part is where it stops.

look at the survivor counts. same p, 2 rows on the peaked list and 4 on the flat one. that count moves with the shape of the list, and thats the whole idea.

now run k = 2 on the flat list instead. dal and khichdi live and everything under them gets deleted, which is 46% of the list by percentage, while the model was genuinely torn between four words. p keeps rice and roti because it counts percentage, not rows.

i kept picturing p as a stricter k. its not a count at all.

set p to 1.0 and you keep every row, which is 034 again with no cut in front of it. most apis let you set p and k together, and both filters apply, so whichever one cuts harder is the one deciding.
