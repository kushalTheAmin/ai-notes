# 135: the cap that stops a run

builds on: [128](./128-count-the-steps.md), [114](./114-no-tool-call-isnt-done.md), [122](./122-what-a-wrong-call-leaves-behind.md)
arc: agents you can trust (14 of 17), ~2 min

128 counted rounds and tokens after the run, as a score. move that same counter inside the loop and it can stop the run.

```text
task: refund order 88120 if the docs allow it
caps for this run:  8 rounds,  20,000 tokens

round  call                 tokens this round   running total
    1  list_recent_orders               1,800           1,800
    2  get_order_by_id                  2,400           4,200
    3  search_docs                      3,600           7,800
    4  search_docs                      4,300          12,100
    5  search_docs                      4,900          17,000
    6  search_docs                      5,400          22,400   <- over 20,000

stopped at round 6 of 8. no refund issued, nothing written.
```

two caps here and the token one trips first, at round 6, with two rounds still spare. whichever line gets crossed first ends it.

theres no model anywhere in that. its a variable i add to at the top of every round and an if that breaks the loop. 114 already put the done check outside the model, this sits in the same place and asks something else, not are you finished but have you spent enough. and it has to be per run, because one call is cheap and predictable, fifteen of them with a history that grows every round is not.

heres the part i didnt like. the cap has no idea where it lands. this run stopped clean, nothing written. the next one stops after the refund goes out and before the customer gets told, and 122 tells you which half of that hurts. so the counter is the easy bit, the work is making the stop survivable and making the run say it was cut off instead of finished.

you put a timeout on an http client because you dont trust the other end to answer. same instinct, one level up.

136 is the other kind of stop, the one i flip by hand.
