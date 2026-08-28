# 067: did the right chunk even come back

builds on: [066](./066-search-wide-sort-narrow.md), [059](./059-search-the-chunks-then-paste-them-in.md)
arc: giving the model your data (12 of 15), ~2 min

066 ended on a question i couldnt answer. is the right chunk in your 50?

turns out you just write the answer key by hand. a question, and the chunk you know answers it. run retrieval, note where that chunk actually came back.

| question | chunk that answers it | came back at |
|---|---|---|
| how do i rotate an api key | keys.md#rotation | 1 |
| whats the refund window | billing.md#refunds | 4 |
| do you support single sign-on | auth.md#sso | 9 |
| how do i delete my account | account.md#deletion | not in top 10 |

```
recall@5    2 of 4 hit    0.50
recall@10   3 of 4 hit    0.75
                 ^ rank 9 counts now, k moved
```

thats the whole metric. one yes/no per question, did the right chunk land at k or better, averaged over the key. if a question has two right chunks you score the fraction that made it, same loop. no model in the loop, just a counter. i kept expecting something harder.

k is the same dial from 066. asking stage 1 for 50 instead of 3 is a bet that recall@50 is high enough, and now its a number you can check instead of a guess.

two things it wont tell you. rank 1 and rank 9 both count as a plain yes, so a key full of barely-made-it hits scores the same as a clean one. and it only measures the four questions i bothered to write down. miss a whole question type and youre passing a test that never asked.
