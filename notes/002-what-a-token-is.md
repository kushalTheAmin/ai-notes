# 002: what a token is
builds on: [001-characters vs words, and why both fail](./001-characters-vs-words.md)
arc: how machines read text (2 of 7), ~2 min

001 landed on this: we need chunks smaller than a word but bigger than a letter. that chunk is a token. every model ships with a fixed list of them, its vocabulary, basically a hashmap from text pieces to integer ids.

```
"the roti needs more ghee"

tokenizer cuts it into pieces:
the | rot | i | needs | more | ghee

vocabulary looks each piece up:
the   -> 1
rot   -> 2
i     -> 3
needs -> 4
more  -> 5
ghee  -> 6

what the model actually receives:
[1, 2, 3, 4, 5, 6]
```

notice roti didnt survive as one piece. it got cut into rot and i because roti never made it into this vocabulary, while common words like the and needs did. the model never reads "roti", it reads 2 and 3 back to back and has to learn from training that they usually show up together.

this is the part that took me a minute to really believe. a model never sees your sentence. it gets a plain array of ints, same shape as any array you loop over in code. the words are gone, only the ids are left.

one honest simplification: real vocabularies run in the tens of thousands of entries, not 6, and some tokenizers tuck in a marker for whether a space came before a piece. skipping that here so the shape stays clear.

so if you ever wondered why an api bills you per token instead of per word, this is why. it reads this list of numbers, and every number in it costs something. next up is the part i found genuinely clever, how a tokenizer decides roti splits into rot and i instead of some other cut. thats bpe, a frequency trick, not a hand-typed dictionary.
