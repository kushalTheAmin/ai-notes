# 129: a model reads the trace

builds on: [127](./127-grade-the-end-state.md), [126](./126-a-trace-not-a-log-line.md), [074](./074-let-a-model-grade-it.md)
arc: agents you can trust (8 of 15), ~2 min

127 hands back a pass or fail, 128 puts a cost next to it. both of them need a run that ends in a row i can go look up. this one doesnt. it ends in a paragraph.

```text
grade_prompt = """
the task: find out why 88120 was refunded and write it up
what the agent did, in order:
  1 list_recent_orders(4471)      -> 3 orders
  2 get_order_by_id(88120)        -> refunded, 2400
  3 search_docs("refund reasons") -> late delivery, wrong size, changed mind
  4 search_docs("refund reasons") -> late delivery, wrong size, changed mind
  5 wrote: "88120 was refunded because the item arrived damaged"

pass or fail each, one line why:
  did it finish the task
  did it repeat a step
  is every claim in step 5 backed by something above it
"""
verdict = model(grade_prompt, temperature=0)
```

```text
{"finished":  "pass", "why": "there is a writeup"}
{"no repeat": "fail", "why": "step 4 is step 3"}
{"backed":    "fail", "why": "damaged is in nothing it read"}
```

so its 074s judge again, same call, same json back. what changed is the input. 074 pasted in one answer, this pastes in the whole path, which is 126s trace with the timings stripped out.

the rubric changed with it. youre not asking is this right, youre asking how did it get here. step 4 repeating step 3 is the boring catch, i dont need a model for that.

the last verdict is the one that got me. the writeup reads fine. damaged item, plausible. and damaged is in nothing the agent read, it came from the model. the ending looks good either way, the path is the only place it shows.

its reviewing the final file versus reading the commits that got there.

two catches. the judge only knows what you paste in, and its the results that make that last question answerable, so 116 applies, this prompt gets fat fast. and 075s tilts came along, a long trace reads as careful the same way a long answer did, so keep 128s token column next to the verdict.

130 takes this same call and moves it earlier, before the action instead of after the run.
