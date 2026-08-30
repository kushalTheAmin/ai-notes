# 032: raw scores arent percentages yet

builds on: [031](./031-the-box-closed.md), [022](./022-guess-the-next-token.md)
arc: how it writes, and the knobs you own (1 of 13), ~2 min

022 and 031 both ended on the same line, the model doesnt pick a token, it hands back a score for every token in the vocabulary and the picking happens after. arc 4 is that after. first thing in the way: those scores arent percentages. some of them are negative.

```
what the model actually handed back
(the raw scores are called logits)

  " ghee"     3.2
  " time"     2.1
  " water"    1.0
  " flour"   -0.4
  ...99,996 more rows, same treatment below

step 1   Math.exp(score) on each row
         all positive now, and the gaps stretch

  " ghee"     3.2  ->  24.53
  " time"     2.1  ->   8.17
  " water"    1.0  ->   2.72
  " flour"   -0.4  ->   0.67
                       -----
              total     36.09

step 2   each one, divided by the total

  " ghee"    24.53 / 36.09  =  68.0%
  " time"     8.17 / 36.09  =  22.6%
  " water"    2.72 / 36.09  =   7.5%
  " flour"    0.67 / 36.09  =   1.9%
                               ------
                               100.0%

(raw scores made up, the arithmetic is real)
```

i kept expecting the raw scores to be something clever. theyre just numbers with no ceiling and no floor, and the only thing they carry is which one is bigger.

step 1 is why you cant skip straight to dividing. " flour" is at -0.4, and negative divided by a total gives you negative percent, which isnt a thing. Math.exp fixes the sign for every row without reordering anything.

now look at what else it did. ghee beat time by 1.1 points of raw score, which sounds like nothing. after the recipe ghee is 68% and time is 22.6%, so three times as likely. the stretching is the interesting part.

this two-step thing is called softmax, and you will see the word constantly. it means what you just watched, raw scores in, percentages that add to 1 out.

still nobody has picked anything. we just went from 100,000 weird numbers to 100,000 percentages. but theres a knob that squeezes or stretches those gaps before step 1 even runs, and thats 033.
