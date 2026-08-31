# 137: when i didnt need the loop

builds on: [121](./121-the-working-agent-assembled.md), [115](./115-one-round-itemized.md), [099](./099-should-this-even-be-a-model-call.md), [129](./129-a-model-reads-the-trace.md)
arc: agents you can trust (16 of 17), ~2 min

fifteen notes of this arc bolted things onto the loop, a gate, a trace, a cap. this one asks what i should have asked first.

```
# agent: the model picks what runs next, and how many rounds
while True:
    reply = model(history)
    if reply.tool_call:
        history.append(run(reply.tool_call))
    else:
        break

# pipeline: i picked the order once, at write time
ticket   = get_ticket(id)                  # code
category = model_classify(ticket.text)     # model call 1
docs     = search_docs(category)           # code
draft    = model_write(ticket.text, docs)  # model call 2
send(draft)
```

the loop buys one thing, the model deciding what runs next and how many rounds there are. the tools, the results going back in, my code did that anyway.

so i wrote out the steps for 099s support inbox. get the ticket, classify it, search the docs, write the reply. i knew that whole order before i started. nothing waits on a model to pick whats next.

the pipeline calls the same model at the two spots that need judgment, every other line is plain code. no array riding along on every round (115). the path is fixed too, so theres no path left to grade (129).

i reached for the loop because it felt like the modern answer. drawing it out felt silly, it was already a flowchart in my head.

the caveat, when the next step depends on what the last one found and you cant list the branches today, thats the loop earning it. otherwise go write your own agents steps out. if you can, you didnt need it.
