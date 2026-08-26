# 018: classify with no training
builds on: [017](./017-embedding-model-is-separate.md), [015](./015-nearby-means-similar.md), [013](./013-cosine-similarity.md)
arc: meaning as numbers (8 of 11), ~2 min

017 left me with a cheap call that hands back a plain array, and i had quietly filed this whole arc under search. then the first thing i actually built with those arrays had nothing to do with search. it was sorting support tickets.

```
embed these three once, keep the arrays around

  bug       "cant log in, the reset link loops"
  feature   "please add dark mode"
  billing   "charged twice this month"

a ticket comes in

  "i got billed for two seats and i only have one"

  embed it, then cosine against each (numbers approx)

    vs bug        0.34
    vs feature    0.26
    vs billing    0.72   <-- max

  label = billing
```

three embed calls at startup, one per ticket after that. cosine three times, take the biggest. thats the classifier, all of it.

i kept scrolling for the training step. there isnt one. no labeled dataset of ten thousand tickets, no training run of my own. i wrote one example sentence per label and the scoring is 013's loop with a max() on top.

and notice what im not doing. no threshold, nothing hardcoded at 0.7. 015 warned me those digits drift model to model, and max sidesteps that completely, it only ever compares the three scores to each other, which is exactly what 015 told me to do.

want a fourth label? write a sentence, embed it, push it on the list. compare that to the if-chain of keyword matches this usually turns into.

two honest limits. one example per label is the toy version, in practice you write five or six and take the best match across all of them. and max always returns something, theres no none of these, so when the top two land 0.02 apart the answer is noise. look at the gap, not just the winner.
