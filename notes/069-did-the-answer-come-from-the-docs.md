# 069: did the answer come from the docs

builds on: [068](./068-where-in-the-list-it-landed.md), [056](./056-closed-book-open-book.md), [038](./038-why-the-made-up-answer-sounds-right.md)
arc: giving the model your data (14 of 15), ~2 min

068 stopped on both numbers stopping at the chunk. this is the first one that opens the answer.

```
what got retrieved and sent

  doc-1   "refunds: 14 days from delivery. sale items are final."
  doc-2   "refunds go back to the original payment method."

what came back, one claim per line, each checked against those two

  14 days from delivery             doc-1     grounded
  sale items cant be returned       doc-1     grounded
  money goes back to your card      doc-2     grounded
  processing takes 3 to 5 days      nothing   UNGROUNDED   true, its on our billing page
  theres a 5 dollar restocking fee  nothing   UNGROUNDED   invented (038)

  groundedness = 3 supported / 5 claims = 0.6
```

the unit is a claim, not the answer. you cut what the model wrote into separate statements, then for each one you go hunting for a chunk that actually says it. found one, grounded. found nothing, ungrounded.

now read the last two lines, thats the whole note. the restocking fee is invented. the 3 to 5 days is true, i could show you the page. both score the same.

that felt wrong to me for a minute. groundedness isnt asking is this true. its asking did this come from the text i sent. a true claim off the frozen file (028) is the model answering closed book while looking open book, which is the blend 056 warned about, and you cant cite it because theres nothing to cite.

so it fails. correctness is somebody elses metric.
