# 014: what an embedding is
builds on: [013](./013-cosine-similarity.md), [011](./011-a-vector-is-a-list-of-numbers.md)
arc: meaning as numbers (4 of 9), ~2 min

013 finished the tool and i still had nothing real to run it on. every array in this arc so far, i typed by hand. heres where the floats come from.

```
POST /v1/embeddings
{ "model": "text-embedding-3-small",
  "input": "kadhi takes an hour" }

  -> {"data": [{"embedding": [0.021, -0.033, 0.008, ... , 0.014]}]}
                              ^                           ^
                            slot 0                    slot 1535
                              <----- 1536 floats, always ----->

same model, three other inputs:
  "hi"                        2 chars  ->  1536 floats
  "kadhi takes an hour"      19 chars  ->  1536 floats
  an 800-word blog post   ~4700 chars  ->  1536 floats
```

you send text, you get back one array of floats. thats an embedding.

two things in that response stopped me. its one array for the whole input, not one per token like 011's table. the words get read, then squashed into one row. and look at the right column, the width never moves. 1536 is a fact about the model, not about what you sent.

that second one is the whole trick and it took me a minute. 012 only works on equal-width arrays, and real text is never equal anything, my sentence isnt your paragraph. embeddings hand you equal width for free. so any two strings, any lengths, are comparable with 013.

you cant send unlimited text, this model caps around a few thousand words, but under the cap the width doesnt move.

and the floats arent arbitrary. theyre the output of a model trained for exactly this, so text that means similar things comes out pointing similar ways. i keep wanting to open one up and read it, same instinct 011 killed. still cant. 015 shows the property instead of claiming it.

one naming thing. 011's table row, one per token, also gets called an embedding. same word, both correct. the one youll actually type in code is this one.
