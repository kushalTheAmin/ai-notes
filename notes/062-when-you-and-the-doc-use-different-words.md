# 062: when you and the doc use different words

builds on: [061](./061-filter-before-you-search.md), [059](./059-search-the-chunks-then-paste-them-in.md), [013](./013-cosine-similarity.md)
arc: giving the model your data (7 of 12), ~2 min

061 ended on a chunk thats allowed, present, and still doesnt come back. heres how that happens.

```
you type:  "can i get my money back for the client dinner?"

 rank 2    handbook/refunds.md
           "Customers may request a refund within 30 days of
            purchase. Refunds are issued to the original card."

           shares with your question:  money back / refund, get
           written for customers. has nothing for you.

 rank 31   handbook/expenses.md
           "Reimbursement. Submit itemised meal receipts in
            Nova within 60 days of the expense date."

           shares with your question:  nothing
           this is your answer. it never enters the top 3.
```

search never sees your question. it sees the vector of the words you typed, and it sorts chunks by how close they sit (013). so the ranking is partly about vocabulary on both sides.

refunds.md wins because you and it both said money back. it reads like your question and answers none of it.

expenses.md says reimbursement, receipts, Nova. zero overlap. it lands somewhere reasonable, just not top 3, and top 3 is all you paste in (059).

took me a minute to accept this. i kept thinking embeddings do meaning, so paraphrase should be free. they do bridge a lot of it, thats real. but every company has its own words, the form number, whatever your handbook calls the expenses tool, and nothing ever taught the model that those mean what you meant.

the part that gets you is that nothing errors. three chunks come back, the model writes a confident answer off the customer refund policy, and your ui looks completely normal.
