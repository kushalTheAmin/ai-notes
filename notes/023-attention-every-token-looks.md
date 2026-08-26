# 023: attention, every token looks at every other token

builds on: [022](./022-guess-the-next-token.md), [016](./016-one-word-many-meanings.md), [012](./012-dot-product-by-hand.md)
arc: whats inside the box (2 of 8), ~2 min

022 left one thing shut on purpose. one call, and back comes a score for every token in the vocabulary. but how does the box know "the roti needs more" wants ghee, when " more" on its own means nothing? i went looking and the answer is a dot product loop.

```
[the] [roti] [needs] [more]      3 floats each, made up

  the    [0.1, 0.9, 0.0]
  roti   [0.9, 0.1, 0.2]
  needs  [0.2, 0.3, 0.8]
  more   [0.3, 0.2, 0.7]   <- this ones doing the looking

1. score "more" against each one, dot product, 012 style
     more . the    = 0.03 + 0.18 + 0.00 = 0.21
     more . roti   = 0.27 + 0.02 + 0.14 = 0.43
     more . needs  = 0.06 + 0.06 + 0.56 = 0.68
     more . more   = 0.09 + 0.04 + 0.49 = 0.62
                                  total = 1.94

2. scores into percentages, each one divided by the total
     the 11%    roti 22%    needs 35%    more 32%

3. new "more" = every vector times its percentage, added up
     0.11 x [0.1, 0.9, 0.0] = [0.011, 0.099, 0.000]
     0.22 x [0.9, 0.1, 0.2] = [0.198, 0.022, 0.044]
     0.35 x [0.2, 0.3, 0.8] = [0.070, 0.105, 0.280]
     0.32 x [0.3, 0.2, 0.7] = [0.096, 0.064, 0.224]
                              ----------------------
                              [0.375, 0.290, 0.548]

   was [0.3, 0.2, 0.7]. now it leans roti and needs.

(numbers made up. real models use a formula that exaggerates
 the gaps, i divided by the total so you can check it by hand.
 also, while generating, a token only looks back, never at
 words that dont exist yet)
```

step 1 is the trick. " more" scores itself against every token in the sentence, itself included, with the same multiply-and-add from 012. high score means those two lean the same way.

step 2 is where the name comes from. " more" is spending 35% of its attention on " needs", 22% on " roti". thats all attention is, a weight.

step 3 took me a minute. the new " more" is every vector multiplied by its own percentage, added up. a weighted average. it walks out carrying a bit of roti, a bit of needs, and it isnt a generic "more" anymore.

which is 016, finally explained. same word, different floats, depending on the neighbours. nothing got looked up, the neighbours just got mixed in by weight.

one thing im flattening: real attention pushes each vector through three small transforms first, so a token can ask for one thing and offer another. the shape holds, score everything, blend by score.

and this runs for every token, not just the last. four tokens, sixteen scores. you can probably already feel what four thousand does. thats 024.
