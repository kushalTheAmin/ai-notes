# 079: read the failures, then sort them into piles

builds on: [078](./078-what-turns-the-build-red.md), [069](./069-did-the-answer-come-from-the-docs.md), [067](./067-did-the-right-chunk-come-back.md)
arc: evals, how you know any of it works (9 of 11), ~2 min

078 goes red and hands me a list of ids and nothing else. so i opened all six and read them one at a time, and thats the whole technique. error analysis is that, plus somewhere to put each one when youre done.

```
grounded 44/50, so six rows failed. i opened all six.

RETRIEVAL: the right chunk never came back (067)
  #14   asked about sso, the top 5 were all billing docs
  #29   i say "cancel", the doc says "terminate" (062)
  #41   right chunk came back at rank 8, i only send 5

ANSWER: the chunk was sitting right there in the context (069)
  #22   cited a doc i never sent
  #33   read the rule, skipped the exception under it

GOLDEN ROW: nothing broke, the row is wrong (072)
  #7    answer says "a month", must_say wants "30 days"

        3 retrieval     2 answer     1 golden row
```

reading one row means looking at three things. what retrieval sent, what the model wrote, and what the row said it wanted. usually one of those three is where it went wrong, and once you see which, the pile picks itself. three piles isnt a rule, its just what six rows needed.

then the counts, thats the payoff. three of my six never had the right chunk in the context, so no edit to the answer prompt fixes them. my instinct after seeing 44/50 was to go rewrite the prompt again, which would have helped two rows out of six. the piles point at a lever, the score never does.

#7 is the one i enjoyed. it flipped by itself back in 076 and i blamed sampling. open it and must_say wants "30 days" while the model keeps writing "a month" (073), so nothing is broken there except my row.

six rows here because i wrote the questions. once its live, the failures pick themselves.
