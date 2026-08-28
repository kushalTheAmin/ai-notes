# 061: filter first, then search

builds on: [059](./059-search-the-chunks-then-paste-them-in.md), [060](./060-where-the-vectors-live.md)
arc: giving the model your data (6 of 12), ~2 min

060 made the search fast. but everything in this arc still ranks on cosine alone, closest meaning wins. nothing in there asks whether priya is allowed to read the thing it hands back.

```
question: "whats our refund window?"     asker: priya, team = support

chunk   score   team
c1      0.91    finance
c2      0.88    finance
c3      0.84    support
c4      0.79    legal
c5      0.72    support
c6      0.65    support

filter AFTER    top 3 by score            -> c1 c2 c3
                drop what she cant read   -> c3
                one chunk, and c5 c6 were readable all along

filter FIRST    keep team = support       -> c3 c5 c6
                top 3 by score            -> c3 c5 c6
                three chunks, all of them hers
```

so a chunk in the store is a vector plus fields. team, doc id, date, whatever you need to filter on, sitting right next to the numbers.

filter after is the version i drew first, and it leaves her with one chunk. run no filter at all and its worse, two finance chunks land in her answer and the ui looks completely normal.

its the same two operations in either order. `.sort().slice(0,3).filter(...)` and `.filter(...).sort().slice(0,3)` read almost the same in a pr, and one of them quietly ships a thin answer. i stared at that longer than im proud of.

one wrinkle: you dont run the filter as your own pass afterwards, you hand the fields to the store and it applies them during the search. when the allowed slice is tiny, that costs the index some of the speed 060 bought.

next one is stranger. sometimes the right chunk is allowed, present, and still doesnt come back.
