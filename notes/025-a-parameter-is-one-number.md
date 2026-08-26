# 025: a parameter is one number the model learned

builds on: [024](./024-twice-the-input-four-times-the-work.md), [011](./011-a-vector-is-a-list-of-numbers.md)
arc: whats inside the box (4 of 10), ~2 min

024 measured cost by how much text you send in. the other axis is the box itself, how big it is. so i downloaded an open model and just looked at the folder.

```
llama-3.1-8b/                   (the files that matter)

  config.json      2 KB   <- shapes and settings, plain json
  tokenizer.json   9 MB   <- 003s merge list, text to ids
  *.safetensors   16 GB   <- the model itself

         8,030,000,000  numbers
       x             2  bytes each
       --------------------------
        16,060,000,000  bytes
```

thats the whole thing. "8B" is just a count. eight billion numbers, each one stored in 2 bytes. a parameter is one of them, one float at one position, and 011 already gave you that shape. this is that, eight billion long.

what i went looking for and did not find: rules. a grammar module, a facts table, some lookup that knows roti is food. none of it is in there. config.json is a couple of kilobytes saying how the numbers are wired up, and the rest is the numbers. the arithmetic that runs over them, 023s attention included, is identical for every prompt. two models wired the same way differ in nothing but those values.

nobody typed those values either. they got set automatically, and how thats done is its own note.

feels obvious now. this morning i was still half-picturing a rulebook in there.

026 is the bill for all this: every one of the eight billion gets read to produce one token. every token.
