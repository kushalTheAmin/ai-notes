# 016: one word, many meanings
builds on: [014](./014-what-an-embedding-is.md), [011](./011-a-vector-is-a-list-of-numbers.md)
arc: meaning as numbers (6 of 9), ~2 min

011 handed me a table with one row per token and i have been treating that row as where the meaning lives. 015 scored whole sentences and never pulled a single word out on its own. heres why it couldnt.

```
// 011's table. one row per token id, fixed, forever
TABLE[8085]   // "bank" -> [0.02, -0.11, 0.07, ...]
TABLE[8085]   // ask again -> the exact same floats

// but "bank" is doing two different jobs here
a = "we sat on the bank of the river"
b = "i moved cash to the bank"

// so 014's call cant be a lookup
embed(a)  -> 1536 floats
embed(b)  -> 1536 floats
//  same word in both. the two arrays land far apart.
```

row 8085 is a constant. it cant be right in both of those, one is a place with water, the other is where my salary lands. a table only gets one answer per key.

so the fixed row isnt the answer, its the starting point. you hand embed() the whole string, the model reads what sits around each word and mixes it in, so what comes out the far end has the neighbours baked in. river, three words away, is part of what decides where bank ends up.

which means theres no vector for bank. not anywhere you can go and read it. theres only a vector for a piece of text that happened to contain it. took me a minute to stop hunting for the table.

the table version was real though. older systems like word2vec kept one row per word and genuinely could not separate the two banks. thats the thing that got fixed.

try it, embed "kadhi takes an hour" then "kadhi" on its own. the arrays come back different. theres no shared row to go find.

and the model doing that mixing isnt the one i chat with. i assumed it was. 017.
