# 117: when the run outgrows the window

builds on: [116](./116-truncate-or-paginate.md), [113](./113-a-failed-tool-call-goes-back-in.md), [053](./053-what-to-leave-out.md), [047](./047-your-code-fakes-the-memory.md), [006](./006-context-window.md)
arc: agents, when output starts doing things (9 of 13), ~2 min

116 let the model ask for page 2, then page 3. every page is another round, and 113 said nothing ever leaves the array. so on round 11 my agent walked into the ceiling from 006.

```
rounds 1 to 9 in the array: 29,700 tokens
                  |
                  |  one extra model call
                  |  "summarise these rounds. keep every id,
                  |   filename and decision."
                  v
one message, 240 tokens, sitting where those rounds were:

  [summary of rounds 1 to 9] searched the 2024 invoices, 3 unpaid:
  INV-1841, INV-1902, INV-1907. INV-1902 was already refunded
  on 12 mar, skip it. customer id 55120. still to do: refund
  1841 and 1907.

array before   31,400 tokens    window is 32,000
array after     1,940 tokens
```

everything that isnt those nine rounds, the system prompt, the schemas, the question and the two newest rounds, is 1,700 tokens. the 29,700 is nine tool results and the short replies between them. one more round and the call gets rejected.

i kept filing this under 053 and its not the same move. 053 keeps the last 6 turns and drops the rest, 047 replays whatever is in the variable. both of those are slicing. folding is the agent taking notes on its own earlier work, and it costs a real call before the round you actually wanted.

so the fold prompt is the whole thing. what would you tell it to keep? mine says every id, filename and decision, because this is one way. whatever the paragraph left out is gone. if that already refunded line drops, round 12 pays INV-1902 twice.

the weird part for me is that the model is now reading notes about itself and cant tell.
