# 066: search wide, then sort narrow

builds on: [065](./065-reads-both-at-once.md), [060](./060-where-the-vectors-live.md), [064](./064-two-searches-one-ranking.md)
arc: giving the model your data (11 of 14), ~2 min

065 ended on a cost i left sitting there. a full model run per chunk. point that at a real store and youre finished. so you dont point it at the store.

```
store: 4,000,000 chunks
   |
   |   stage 1, cheap, touches everything
   |   the index from 060 + the merge from 064
   |   ~12,000 comparisons
   v
50 candidates
   |
   |   stage 2, expensive, touches only these 50
   |   the pair scorer from 065
   |   50 full model runs
   v
5 chunks  ->  into the prompt

skip stage 1, rerank the store:   4,000,000 model runs
put ten times more docs in it:    stage 2 still costs 50
```

stage 1 stops being the thing that picks your answer. its job is picking who gets read. so you ask it for 50 instead of 3, same search from 060, bigger slice.

then the part that made it click for me. stage 2s bill is set by the number you picked, not by how much you own. dump ten times more docs in tomorrow and stage 2 doesnt feel it. the expensive model never meets the pile, and thats the whole reason this shape exists.

same instinct as a cheap where clause before an expensive join. feels obvious now, wasnt this morning.

one thing it cant do. if the right chunk didnt make the 50, the reranker never sees it, and a better score cant rescue what stage 1 threw out. widen to 200, better odds, four times the work. 50 is a dial, not a law.

so how would you know whether the right chunk is in your 50? you cant eyeball that. 067 is where that starts.
