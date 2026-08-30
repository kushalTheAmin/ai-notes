# 114: no tool call isnt the same as done

builds on: [113](./113-a-failed-tool-call-goes-back-in.md), [082](./082-a-while-loop-with-a-model-inside.md), [083](./083-when-the-loop-wont-stop.md), [109](./109-when-the-answer-stops-being-a-suggestion.md)
arc: agents, when output starts doing things (6 of 13), ~2 min

113 left the loop able to survive a bad round, so it keeps going. the other half of that is when it stops.

```
082s exit, and the line that has to sit under it

while True:
    reply = model(messages, tools)
    messages.append(reply)

    if reply has no tool call:

        # 082 returned right here. what it can return:
        #   "refunded order 44718, 3 to 5 days"
        #   and issue_refund is nowhere in messages

        if not refund_exists(44718):   # my db. no model in this line
            return failed(reply.text)
        return reply.text

    run the calls, append the results (113)
```

082s exit is one line. no tool call in the reply, return the text. i read that as the agent finishing.

it isnt. its the model writing prose instead of asking for a function. it does that when the job is done, and the exact same thing when it only thinks it is, or when it narrated the refund instead of calling it.

that third one is the one that got me. nothing errors, so 113 has nothing to feed back. 083s counter never fires, the loop ended on round two, politely. the sentence reads perfect, right order number, delivery window, all of it. no money moved.

so the return path gets a check my own code can answer. one query against my database. either the refund row is there or it isnt, and the model gets no vote in that line.

honest limit: this works when the task has an end state you can look up. a refund does. "wheres my order 44718" doesnt, and there youre still taking the models word for it.
