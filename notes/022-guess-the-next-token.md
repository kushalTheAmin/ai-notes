# 022: all it does is guess the next token

builds on: [021](./021-search-by-meaning-end-to-end.md), [002](./002-what-a-token-is.md), [011](./011-a-vector-is-a-list-of-numbers.md)
arc: whats inside the box (1 of 10), ~2 min

arc 2 left the model as a thing that eats my text and hands back floats. 021 ended asking what it does going the other way, handing words back. heres the answer, and its smaller than i expected.

```
prompt: "the roti needs more"

step 1   in    [the][ roti][ needs][ more]
         out   a score for every token in the vocabulary, all ~100,000
                 " ghee"    31%
                 " time"    19%
                 " water"   12%
                 " flour"    8%
                 ...the other 99,996 share whats left
         pick  " ghee", stick it on the end

step 2   in    [the][ roti][ needs][ more][ ghee]
         out    "."        27%
                " than"    14%
                " and"      9%
                 ...
         pick  ".", stick it on the end

step 3   in    [the][ roti][ needs][ more][ ghee][.]
         out    <done>     41%
                " it"       6%
                 ...
         pick  <done>, loop breaks

result: "the roti needs more ghee."

(the model actually returns raw scores, these are percentages
 because they read easier. numbers made up, the shape is real)
```

look at the out lines. no sentence comes out, ever. one call gives back one number per token in the vocabulary, 011's table with a score on every row. 100,000 rows, 100,000 numbers back, and one of them gets used.

then the loop. take a token off that list, glue it to the end of the input, run the whole thing again. every step gets the full list from the start, not just the new bit. that growing list of ids is the whole state, nothing else carries.

one thing i had backwards: the model doesnt pick. it produces the list, the picking happens after, and how it picks is a knob you own in arc 4.

stopping is dumber than i thought. the vocabulary holds a token that means done, and when that one wins, the loop breaks.

if youve watched a chat ui type a reply out word by word, thats not an animation. thats this, running.
