# 037: theres no row for "i dont know"

builds on: [032](./032-raw-scores-arent-percentages.md), [034](./034-greedy-vs-sampling.md), [022](./022-guess-the-next-token.md)
arc: how it writes, and the knobs you own (6 of 13), ~2 min

032 through 036 all leaned on something none of them said out loud. the model hands back a full list of percentages and one row wins. every step, no exceptions.

```
two prompts, same model, one step each


A   "the roti needs more"                   seen a million lines like this

      " ghee"                  68.0%
      " time"                  22.6%
      " water"                  7.5%
      " flour"                  1.9%
      the other 99,996 rows     0.0%   all of them round to zero
                              ------
      total                   100.0%   picked: " ghee"


B   "to retry the call, use retryPolicy."   i made retryPolicy up,
                                            it does not exist

      " withBackoff"           14.0%
      " create"                11.5%
      " exponential"            9.0%
      " retry"                  7.0%
      the other 99,996 rows    58.5%   spread thin across all of them
                              ------
      total                   100.0%   picked: " withBackoff"


same softmax, same roll, same 100.0%.
neither list has a row that means "i dont know"
```

look at B. i made retryPolicy up while writing this note, and the list still adds to 100.0%, still has a favourite. thats softmax from 032. run Math.exp on every score, divide by the total, and what comes out adds to 1 no matter what went in. a list built on nothing comes out just as tidy as a list built on a million recipe lines.

then 034 picks a row off it. no floor under that step, no "if the top row is under 20%, stop". so the loop from 022 runs, a token comes out, gets glued to the end of the input, and the next step reads it back as fact.

ever had a model hand you an api method that doesnt exist? this is where it comes from.

the bit that took me a minute: the model can type "i dont know", it does it plenty. but those are tokens winning, training and tuning made them likely there. thats not the machinery declining. 022 has a real <done> token in the vocabulary that breaks the loop. theres nothing like it for not knowing.

i kept looking for the guard clause. theres no guard clause.
