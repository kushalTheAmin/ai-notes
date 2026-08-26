# 017: the embedding model is its own product
builds on: [016](./016-one-word-many-meanings.md), [014](./014-what-an-embedding-is.md)
arc: meaning as numbers (7 of 9), ~2 min

016 ended with the mixing being done by a model i hadnt actually met. i had been picturing the chat model doing it quietly on the side. its not that. different url, different name on the pricing page, and it cant hold a conversation.

```
         chat model             | embedding model
--------------------------------------------------------------------
POST /v1/chat/completions       | POST /v1/embeddings
                                |
{ "messages": [                 | { "input": "kadhi takes an hour" }
   {"role": "system", ...},     |
   {"role": "user", ...}],      |    ^ no roles, no system,
  "temperature": 0.7 }          |      no temperature
                                |
-> "about a teaspoon per roti"  | -> [0.021, -0.033, ...]
   text                         |    1536 floats (014)
                                |
billed: tokens in AND out       | billed: tokens in only
1M tokens in  ->  $3.00         | 1M tokens in  ->  $0.02
```

count the knobs on the left. roles, a system message, temperature, all things i havent covered yet, and the right side has none of them. you pass a model name and your string, and thats the whole request. nothing to prompt, no back and forth to keep track of.

then the money. both sides read a million tokens of my text. thats $3 on the left at 004's rate, two cents on the right. 150x, and thats on input alone. the left column also has a second meter running, output tokens, which 004 showed is the pricier direction. the right column never has one, an embedding model writes no text at all. i checked that gap twice.

one thing that bites later. floats from one embedding model only mean anything next to floats from that same model. pick one, embed everything with it, and switching later means re-embedding the whole pile.
