# 034: greedy takes the top row, sampling rolls for it

builds on: [033](./033-temperature-is-one-divide.md), [032](./032-raw-scores-arent-percentages.md)
arc: how it writes, and the knobs you own (3 of 10), ~2 min

033 dug a hole and left it. the same divisor on every score cant reorder anything, so ghee sits on top at 0.4 and at 2.0 both. if the picker always grabs the top row, temperature does nothing. that picker is real, its called greedy, and its one of two options.

```
the percentages from 033, temperature 1.0, written as decimals

  " ghee" 0.680    " time" 0.226    " water" 0.075    " flour" 0.019
   68.0%            22.6%            7.5%             1.9%


GREEDY                      SAMPLING

return biggest row          roll = random()        // 0.0 to 1.0
                            running = 0
= " ghee"                   for each row:
every time, forever           running += row.percentage
                              if (roll < running) return row


one roll, it comes up 0.83

  " ghee"    running = 0.680    0.83 < 0.680 ?   no
  " time"    running = 0.906    0.83 < 0.906 ?   yes   ->   " time"
  " water"   running = 0.981    never reached
  " flour"   running = 1.000    never reached
```

greedy is the boring one. biggest percentage, return it, done. same scores in, same token out. no api defaults to this, you have to ask for it.

sampling rolls once and walks down the rows adding percentages until the running total passes the roll. every row ends up owning a slice of the 0 to 1 line exactly as wide as its percentage. ghee owns 0 up to 0.680, time owns the next 0.226.

the roll came up 0.83, that lands in the second slice, so time gets written even though ghee was three times more likely. if you have ever coded a weighted random pick for loot drops or an a/b bucket, you already wrote this loop.

i had it backwards for a while. i thought sampling was the model being creative. its a random number and a running sum.

and temperature 0, the thing everyone reaches for when they want the same answer twice, is just this. you cant divide by zero, so providers skip the roll and hand you greedy.
