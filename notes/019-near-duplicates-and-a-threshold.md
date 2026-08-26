# 019: near-duplicates, and the one number you have to pick
builds on: [018](./018-classify-with-no-training.md), [015](./015-nearby-means-similar.md), [017](./017-embedding-model-is-separate.md)
arc: meaning as numbers (9 of 11), ~2 min

018 dodged the hard part. max() only compared three scores to each other, so i never had to say what a good score is. near-duplicate checking takes that away. two tickets, one cosine, is this the same complaint we already have open? nothing to rank it against, so the number has to stand on its own.

```
the three tickets from 018, each next to a lookalike, sorted by cosine

  0.94  "cant log in, the reset link loops"
        "login broken, password reset just loops"    same
  0.87  "cant log in on mobile"
        "cant log out on mobile"                     different  <- merged
  ----------------------------------------------- cut at 0.85
  0.81  "please add dark mode"
        "can you add a night theme"                  same       <- missed
  0.34  "charged twice this month"
        "please add dark mode"                       different
```

you sort your pairs and draw a line. thats the method, and it annoyed me a bit that its not cleverer. the line is yours to find by hand: label thirty pairs dupe or not, score them, sort, see where the groups sit. mine wanted 0.85.

now read either side of that line. log in and log out share nearly every word, land at 0.87, and my cut merges two unrelated tickets. dark mode and night theme share none, land at 0.81, and my cut misses a real dupe. drop to 0.80 and i catch dark mode, plus whatever else sits in that band. you trade one mistake for the other, you dont get to delete both.

and 0.85 is only mine. swap the embedding model and every score moves (017), so the number goes in the bin and you do this again.

020 keeps the scores and drops the labels.
