# 013: cosine similarity, a score that ignores size
builds on: [012](./012-dot-product-by-hand.md)
arc: meaning as numbers (3 of 9), ~2 min

012 ended on a hole i left open. scale b ten times bigger, same direction, and the total jumps from 20 to 200. heres the fix, one division.

```
a = [2, -1, 3]
len(a) = sqrt(2*2 + -1*-1 + 3*3) = sqrt(14) = 3.74

                                 b        b x10            d
                          [3,-2,4]  [30,-20,40]      [1,3,0]
  dot with a                    20          200           -1
  its own length              5.39        53.85         3.16
  ----------------------------------------------------------
  dot / (3.74 * len)          0.99         0.99        -0.08
```

the length of an array stopped me for a second, i assumed it was a new operation. its the 012 loop with the same array passed in twice, then a square root.

then divide the dot product by both lengths, one per array. read the b x10 column down and watch the problem die. the dot went up ten times, but bs own length went 5.39 to 53.85, the same ten. it cancels, both columns land on 0.99, which is right since the direction never changed.

after that division the score cant leave -1 to 1. 1 is pointing the same way, -1 is dead opposite (c from 012 is b with every sign flipped, it scores -0.99), near 0 is unrelated, thats d at -0.08. every pair on one ruler now.

the name is the only weird part. it comes from trig, and if you picture each array as an arrow, the score really is the cosine of the angle between them. you never need to picture that to use it.

so the tool is done. these arrays are still numbers i made up though, nothing yet says why a real row of floats would mean anything. 014 starts there.
