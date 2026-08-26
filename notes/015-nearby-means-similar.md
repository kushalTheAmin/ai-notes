# 015: nearby means similar
builds on: [014](./014-what-an-embedding-is.md), [013](./013-cosine-similarity.md)
arc: meaning as numbers (5 of 9), ~2 min

014 claimed the floats end up pointing the same way when the text means the same thing, then showed you none of it. heres the check. three sentences into that same model, 013's cosine on each pair.

```
A  kadhi takes an hour
B  this dish needs sixty minutes on the stove
C  my typescript build takes an hour
```

| pair | words in common | cosine, approx |
| --- | --- | --- |
| A vs B | 0 | 0.55 |
| A vs C | 3 | 0.41 |
| B vs C | 0 | 0.18 |

row two got me. A and C share three real words, takes an hour, and they still land under A and B, which share zero. B never says kadhi. it wins anyway, because a dish and sixty minutes on a stove is what A is about.

row three is the floor, a stove and a typescript build, 0.18, which 013 taught us to read as unrelated.

nothing here is counting overlapping words. i expected overlap to carry more weight than it does.

thats all nearby means. high cosine, arrows pointing the same way, so we say those two texts sit near each other. near is direction, not distance on a map.

treat the digits as ballpark, the order is the real output. dont go build a threshold at 0.5 either, that number drifts by model, some bunch everything up into the high 0.7s. rank scores against each other.
