# 012: dot product, by hand
builds on: [011](./011-a-vector-is-a-list-of-numbers.md)
arc: meaning as numbers (2 of 11), ~2 min

011 ended on two equal-width arrays and said they can be walked together in one loop. this is that loop.

```
a = [ 2, -1,  3 ]

          b = [  3, -2,  4 ]    c = [ -3,  2, -4 ]    d = [  1,  3,  0 ]
slot 0        2 *   3 =    6        2 *  -3 =   -6        2 *   1 =    2
slot 1       -1 *  -2 =    2       -1 *   2 =   -2       -1 *   3 =   -3
slot 2        3 *   4 =   12        3 *  -4 =  -12        3 *   0 =    0
                      ------                ------                ------
                          20                   -20                    -1
```

pick a column and go down it. multiply slot 0 by slot 0, slot 1 by slot 1, add each product to a running total. one number falls out at the end. thats the entire operation, and it works the same whether the arrays are 3 long or 4096.

i expected something heavier. its a `reduce` in typescript, a for loop with a running total in C#. equal width is the only requirement, slot 0 pairs with slot 0 and nothing is left over.

now look at what the number does, thats the part i actually cared about. b leans the same way as a in every slot, so every product comes out positive, 20. c is b with every sign flipped, they disagree everywhere, -20. d agrees with a in slot 0, disagrees in slot 1, and slot 2 contributes nothing at all, so you get -1. agreement pushes the total up, disagreement pulls it down. unrelated lands near zero, and near is doing real work in that sentence, nothing forces the products to cancel perfectly.

one catch to hold onto before you trust one of these numbers. scale b up to [30, -20, 40], exact same direction as before, and the total becomes 200. big numbers move it on their own, so a big total is not proof of a strong match.
