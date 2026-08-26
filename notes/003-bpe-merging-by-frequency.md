# 003: BPE, merging by frequency
builds on: [002-what a token is](./002-what-a-token-is.md)
arc: how machines read text (3 of 7), ~2 min

002 ended with a promise: explain why roti splits into rot and i instead of some other cut. the answer is byte pair encoding, bpe for short, and its dumb-simple: start from single characters and keep gluing together whichever pair shows up most.

```
corpus (counts):  roti x5   rot x3   rope x2
start as characters, _ marks end of word:

r o t i _   x5
r o t _     x3
r o p e _   x2

round 1, count every neighbor pair:
(r,o): 5+3+2 = 10   <- most common, merge it
(o,t): 5+3   = 8
(t,i): 5
others: fewer

after merging r+o -> ro:
ro t i _    x5
ro t _      x3
ro p e _    x2

round 2, count again:
(ro,t): 5+3 = 8   <- most common, merge it
others: fewer

after merging ro+t -> rot:
rot i _     x5
rot _       x3
ro p e _    x2
```

start every word as separate characters. count every neighboring pair across the whole training corpus. whichever pair appears most, fuse it into one new piece. repeat. thats the entire algorithm, which genuinely surprised me the first time i read it, no linguist decides which chunks deserve to exist.

here, r followed by o wins round one with 10 appearances, more than any other pair, so they fuse. round two, ro followed by t is the most common pair at 8, so they fuse into rot. rot showed up together often enough across the corpus to earn its place as one piece. the i in roti never got that treatment, it didnt pair with anything common enough to merge yet.

thats the whole trick, frequency in the training data decides the vocabulary, nobody sits down and writes it by hand. next time an api response splits some word into a weird chunk, thats why, that pairing didnt come up often enough in training. real tokenizers run this for tens of thousands of rounds over billions of words, not two rounds over ten, but the mechanism stays exactly this loop.

next up: tokens are money, literally, how the pricing actually works once you know what a token is.
