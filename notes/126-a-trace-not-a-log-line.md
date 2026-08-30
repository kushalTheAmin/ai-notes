# 126: a trace, not a log line

builds on: [125](./125-the-gate-that-doesnt-drown-you.md), [119](./119-a-fresh-window-with-a-narrower-job.md), [097](./097-what-your-http-log-is-missing.md)
arc: agents you can trust (5 of 12), ~2 min

125 left a run full of decisions. some calls ran on their own, one got refused in code, one waited for a person. nothing i was writing down said which was which, or that they were one run.

```text
run 4f2a   "refund the order kushal called about"   7 steps + 3 nested   10.8s

 1  model                   1,200 in     90 out    1.2s
 2  list_recent_orders                             0.3s
 3  model                   1,500 in    110 out    1.4s
 4  sub-agent  check the refund window              4.4s
    4a  model                 900 in     80 out    1.1s
    4b  search_docs                                0.5s   <- page came back whole
    4c  model               5,800 in     90 out    2.8s   <- biggest call in the run
 5  model                   1,700 in    120 out    1.6s
 6  issue_refund  order 88120                      0.4s   <- denied by the gate
 7  model                   1,850 in     40 out    1.5s

same run in a flat log: six "model call, 200 ok" lines in timestamp
order, shuffled in with every other run happening right now
```

097 already got one call written down properly, model id, tokens, attempt. that list is still right. what it cant give you is the shape above. six correct lines with nothing tying them together is six facts, not a story.

the fix is boring. one id made when the run starts, passed into every call it makes, and each step recording which step spawned it. you already do this for http, its the same request id threaded through your services.

now read the block. the parent never sees an input over 1,850 tokens, so from outside this run looks cheap. the 5,800 sits one level down, in a step the parent knows only as 4.4 seconds. 119 said the sub-agent hands back a sentence you cant audit, this is where you audit it, you open step 4 and read the three calls under it.

took me a while to stop scrolling a log tail hunting for the bad call. the bad call was fine on its own line. what was wrong was where it sat.

127 does something else with those right hand columns.
