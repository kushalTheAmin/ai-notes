# 133: the key decides who reads the row back

builds on: [132](./132-a-bad-row-outlives-the-run.md), [131](./131-a-store-that-outlives-the-run.md), [101](./101-whats-in-the-request-nobody-typed.md)
arc: agents you can trust (12 of 17), ~2 min

132 asked who rechecks a row. this one is quieter. who gets to read it back.

```
# monday. the run about customer 4471 ends, my code squeezes it to one row
row = "orders in bulk, wants store credit.
       past ticket 8812, rahul m, card ends 4417"
#      ^ came off a retrieved chunk (101). nobody in this run typed it

memory[ACCOUNT] = row          # keyed on my acme account

# tuesday. different customer, different agent, brand new loop
round_1 = [ system,
            "notes: " + memory[ACCOUNT],
            "wheres my order?" ]
#                       ^ rahuls card tail, in a run thats got nothing to do with him
```

i typed memory[4471] in 131 like it was a variable name. that subscript is the whole access story. whatever you key on is the set of runs that read the row back, and a key one level too wide leaks with no error and no log line.

so key it on the thing the row is about. that gets you most of the way, not all of it. look at the row itself. monday squeezed a whole run down to a line, and that run had a chunk in it about somebody else. 101 said the chunk leaves on one call. here it gets filed.

if youve ever keyed a cache wrong you know the shape of this, it usually shows up as someone elses name in the ui. this one nobody sees, it just sits in the next prompt.

134 is the other half of it, how long any of this should stick around.
