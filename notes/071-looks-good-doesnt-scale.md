# 071: "looks good" doesnt scale

builds on: [070](./070-from-my-docs-to-an-answer.md), [067](./067-did-the-right-chunk-come-back.md), [068](./068-where-in-the-list-it-landed.md), [069](./069-did-the-answer-come-from-the-docs.md)
arc: evals, how you know any of it works (1 of 11), ~2 min

070 left the four questions from 067 sitting there as a placeholder for an answer key. this note is about why four was always going to break.

```
after one prompt tweak, did the answer get better?

  recall 067, mrr 068  ->  ranks come back with the search.  free
  groundedness 069     ->  i open the 5 chunks and check
                           every claim.                      2 min

  4 questions   ->   4 x 2 =    8 min of me, per run
  50 questions  ->  50 x 2 =  100 min of me, per run

  a normal afternoon of fiddling: 12 tweaks, so 12 runs

  4 questions   ->   8 x 12 =    96 min   (1.6 hours)
  50 questions  -> 100 x 12 =  1200 min   (20 hours)

  same 12 runs, model side:
  50 x 12 = 600 calls, 20 at a time  ->  a few minutes
```

heres the split i didnt see coming. the retrieval half already runs itself. once i wrote down which chunk should answer each question, recall and mrr recompute for free every run, the ranks fall out of the search results anyway. the answer has no key like that. right now the only thing checking it is me, opening the chunks and reading claims (069), about two minutes if im quick.

so four questions costs eight minutes a run and thats nothing. then count how many times you touch a prompt in one afternoon. moving the docs above the question, adding a citation line, putting the examples back. a dozen is a slow day.

now say fifty questions instead of four, because four isnt covering 10,000 docs. my number is twenty hours, the model finishes in minutes. reading is the only step in this loop that runs at exactly one person, and honestly by answer forty im skimming, and a skimmed answer gets waved through.
