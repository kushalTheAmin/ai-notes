# 063: the search that understands nothing

builds on: [062](./062-when-you-and-the-doc-use-different-words.md), [016](./016-one-word-many-meanings.md)
arc: giving the model your data (8 of 13), ~2 min

after 062 i went hunting for a better embedding model. wrong direction. the thing that finds Nova is plain keyword search, the kind you already built behind a search box with a LIKE query. real ones index up front, a hashmap from each word to the chunks holding it.

```
the doc you want, both times:

handbook/expenses.md   (062)
"Reimbursement. Submit itemised meal receipts in
 Nova within 60 days of the expense date."
```

| you type | closest by meaning | matching words literally |
| --- | --- | --- |
| how long do i have to claim a work lunch back? | rank 1. lunch sits near meal, claim back near reimbursement | nothing. no word in common |
| whats the Nova deadline? | buried under every doc that says deadline | rank 1, one lookup |

read the columns down. each one wins a row and whiffs the other.

top row is what embeddings are genuinely good at. nobody wrote a synonym list anywhere and it still lands.

bottom row flips. you type the internal tool name and it comes straight back. the embedding does try to understand that word, and thats the problem. it has a sense for "nova", the star, whatever it saw in training (016), and nothing at all for your expenses tool, so the question drifts toward whatever else says deadline.

the dumbness being the feature is what got me. nothing in there to misread.

one honest bit, its not grep. real keyword search weights rare words heavier than common ones, which is exactly why an invented name like Nova is such a loud signal.

and no, this doesnt rescue 062. you typed money back, the doc said reimbursement, and the literal list has even less to grab there. two rankings now, neither is the good one. 064 merges them.
