# 131: memory across runs

builds on: [130](./130-the-judge-moves-in-front-of-the-gate.md), [118](./118-files-are-the-agents-real-memory.md), [047](./047-your-code-fakes-the-memory.md)
arc: agents you can trust (10 of 15), ~2 min

every piece arc 11 has built is scoped to one run. the trace, the pass rate, 130s screen, all of it dies when the loop exits. memory is the first thing here that outlives a run.

```
run 1, monday
  round 1 array: [ system, "why was 88120 refunded?" ]
  ... four rounds, some tool calls, an answer ...
  loop exits. my code writes one row:

      memory[4471] = "orders in bulk, wants refunds as store credit"
                      ^ not the transcript. one line, squeezed out of four rounds

run 2, thursday. brand new loop, empty array
  my code looks up 4471 BEFORE round 1 and pastes the row in:

  round 1 array: [ system,
                   "notes on this customer: orders in bulk,
                    wants refunds as store credit",
                   "can i return 88121?" ]
                   ^ to the model this is just text. it cant tell monday from now
```

took me a minute to see theres nothing new here. 047 said my code fakes the memory inside one conversation by re-sending the array. this is that same fake one level up, and the store isnt the array.

the split from 118 is who reads. plan.md comes back because the agent calls read_file, mid run. this row goes in before the model gets a turn, and the agent never asks for it.

the write is a decision. dump all four rounds of monday into thursday and ive paid 115s bill for a conversation nobody asked about. so its a squeeze, a whole run down to a line worth rereading.

and nothing was learned. the weights didnt move, 028 still holds. thursday works because a select ran.

i went looking for the memory api for way too long. its a user_preferences table with a prompt bolted on the end. if youve ever cached a users settings, you have written most of this.

which leaves a row that gets read back every thursday with nobody rechecking it. 132 is about that.
