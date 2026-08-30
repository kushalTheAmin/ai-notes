# 087: the two numbers you pick before you build

builds on: [086](./086-the-same-question-twice.md), [084](./084-why-the-ui-types.md), [066](./066-search-wide-sort-narrow.md), [043](./043-thinking-on-the-bill.md), [004](./004-tokens-are-money.md)
arc: running it, speed, cost, and when things break (6 of 17), ~2 min

086 ended on what a call costs and how long you wait. here they are, on one question to my doc-QA thing.

```
budget i wrote down first: 1s to first text, 3c a question

  stage                      wait     cost
  embed the question        40 ms    0.00c
  vector search             30 ms    0.00c
  rerank 20 chunks         200 ms    0.20c
  model, first token       600 ms
  model, rest of answer  2,000 ms    2.10c
  ----------------------------------------
  to first text            870 ms
  to done                2,870 ms    2.30c

  2.30c x 4,000 questions a day = $92 a day
```

a budget is those two numbers picked before you build, and then every stage spends out of them. the rerank (066) is the clearest one on the sheet. 200ms and a fifth of a cent, and it buys better chunks. that trade only exists once you have a line to spend against.

the wait a user feels is 870ms, not 2.8 seconds, because 084 is already printing by then. if your code parses json out of the response instead, nobody sees anything until 2,870.

the cost row is where i got caught out. 2.3c a question reads as free. times my traffic its $92 a day, near $2,760 a month, for one feature.

the two rows also move together, which i keep forgetting. swap in a reasoning model and you wait longer for the first token and you pay for thinking tokens you never read (043). one swap, both budgets.

my digits are not yours, different model, different chunk count. having the two written down is the whole thing. without a line, every stage you add sounds cheap and you find out at the invoice.
