# 035: top-k cuts the list before the roll

builds on: [034](./034-greedy-vs-sampling.md), [032](./032-raw-scores-arent-percentages.md)
arc: how it writes, and the knobs you own (4 of 11), ~2 min

034 left the roll walking every row, top to bottom. " flour" at 1.9% still owns a real slice of the 0 to 1 line, and the real list isnt 4 rows, its 100,000. top-k is the knife. sort, keep k rows, delete the rest, roll on whats left.

| row | percentage | after top-k, k = 2 |
| --- | --- | --- |
| `" ghee"` | 68.0% | 75.1% |
| `" time"` | 22.6% | 24.9% |
| `" water"` | 7.5% | cut |
| `" flour"` | 1.9% | cut |
| **total** | 100.0% | 100.0% |

```
survivors add to  0.680 + 0.226 = 0.906

  0.680 / 0.906 = 0.751        0.226 / 0.906 = 0.249
```

set k to 2 and water and flour stop existing for this one token. next token, fresh scores, fresh cut.

the part i kept skipping is the rescale. cut two rows and whats left adds to 0.906, not 1. roll a 0.95 and you walk past both survivors, run out of list, return nothing. so you divide each one by 0.906 and they add back to 1.

now look at ghee. 68.0 went to 75.1. deleting the tail hands its probability to the rows you kept, so the favourite gets more favourite. small k, safer and duller. big k, the tail comes back.

k is a fixed count though. the same count whether the model is dead certain or completely torn between two words. that bugged me for a while, and its why some apis dont expose it at all. 036 is the fix.
