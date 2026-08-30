# 041: the same prompt, twice, two different answers

builds on: [034](./034-greedy-vs-sampling.md), [022](./022-guess-the-next-token.md)
arc: how it writes, and the knobs you own (10 of 13), ~2 min

034 ended on temperature 0 skipping the roll and handing you greedy. no random number left anywhere. so pin it to 0 and you get the same answer forever.

i believed that for a while.

```
"the best thing to eat with masala chai is"
temperature 0 both times, same model, calls sent a minute apart

  CALL A                          CALL B
  scores for the next token       scores for the next token

  " fafda"    8.1342   <- top     " fafda"    8.1340
  " dhokla"   8.1339              " dhokla"   8.1341   <- top
  " thepla"   6.9021              " thepla"   6.9022

  writes " fafda"                 writes " dhokla"

  " fafda, obviously, crispy      " dhokla, steamed, still
    and salty and..."               warm and..."
```

your call doesnt get a gpu to itself, it rides along with whoever else hit the api that second. how many of you are in there decides how the machine splits up the adding, and the same floats added in a different order give a slightly different total. same reason 0.1 + 0.2 isnt 0.3 in javascript. so the scores wobble past the 3rd decimal.

almost always that changes nothing. greedy did its job both times, took the top row. the top row moved.

then it compounds, because the loop from 022 writes each token from what it already wrote. one flipped word and the rest comes off a different sentence.

so your cache holds two right answers under one key, and a test asserting an exact string goes flaky for no reason thats in your diff. seed doesnt save you either, it pins the roll, not the adding.

temperature 0 doesnt mean deterministic. it means no dice roll. i had those as the same thing. arc 7 is where i find out how you test something that wont sit still.
