# 083: when the loop wont stop

builds on: [082](./082-a-while-loop-with-a-model-inside.md), [047](./047-your-code-fakes-the-memory.md), [004](./004-tokens-are-money.md)
arc: running it, speed, cost, and when things break (2 of 11), ~2 min

082 left the loop with one exit, and the model owns it. so what does it cost when it never takes it.

```
doc-QA agent, one question, each round appends about 1,000 tokens

round      sent this round      billed so far
   1              1,000              1,000
   2              2,000              3,000
   3              3,000              6,000   <- answers here on a good day
   6              6,000             21,000   <- my cap kills it here
  20             20,000            210,000   <- no cap, still asking
```

every round re-sends the whole array (047), and it got longer last round. so ten rounds isnt ten times one round, its fifty five times. i knew the array grew, i just never did the addition.

a stuck loop doesnt look like a hang, thats the part that got me. the model keeps asking search_docs with reworded queries, my code keeps running them, nothing throws. it reads as progress the whole time the meter runs.

so my code brings its own exits. a round counter that hard stops at 6. a token total checked before each call. a wall clock too, since one tool call can hang while the round count sits at 2.

what do you send back when you hit the cap? theres no clean answer. i return the last text with a flag, and log the array, because 6 rounds usually means my tool descriptions were bad, not a hard question.
