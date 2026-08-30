# 011: a vector is just a list of numbers
builds on: [010](./010-what-i-send-and-what-it-costs.md)
arc: meaning as numbers (1 of 11), ~2 min

010 left 5868 sitting on the wire and i called it a lookup key. heres what its a key to.

```
id 5868 (" rot")  ->  row 5868 of the model's table

    [ 0.018, -0.041,  0.003,  0.046, ... , -0.009 ]
      slot0   slot1   slot2   slot3         slot767
      <-------------- 768 floats -------------->

id   19 ("4")  ->  [-0.006,  0.022, -0.018,  0.031, ... ,  0.004 ]
id   72 ("i")  ->  [ 0.009, -0.001,  0.041, -0.026, ... , -0.012 ]
id  285 ("is") ->  [ 0.011,  0.033, -0.007,  0.002, ... ,  0.027 ]

one row per token in the vocabulary. every row the exact same width.
(floats here are made up, the shape is real)
```

the id was never data, its an index. the model carries one big table, a row per token in its vocabulary, and 5868 means row 5868. that row is a plain array of floats, and thats all a vector is. `number[]` in typescript, `float[]` in C#. if youve ever written `new float[768]`, you already have the data structure.

the width is the part to hold onto. the small gpt-2 used 768 floats a row, llama 3 8b uses 4096, the big closed models dont publish theirs. inside one model though, every row is that same width. a vocabulary of 100,000 tokens at 768 floats a row is 76.8 million numbers, loaded before you send anything.

i went hunting for slot 4 to mean something, a flag for "is this a noun" maybe. it doesnt. no single slot is readable on its own, and i had to give that up before the rest of it landed.

same id, same row, every time. that row does change once its moving through the model, but thats a later note.

equal width is the whole reason two of these can be walked together in one loop. 012 is that loop.
