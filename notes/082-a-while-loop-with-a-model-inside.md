# 082: an agent is a while loop with a model inside

builds on: [081](./081-the-harness-in-four-files.md), [051](./051-the-model-asks-your-code-acts.md), [047](./047-your-code-fakes-the-memory.md), [070](./070-from-my-docs-to-an-answer.md)
arc: running it, speed, cost, and when things break (1 of 11), ~2 min

081 closed arc 7 on one call in, one answer out, scored. an agent is that same call, put inside a loop.

```
messages = [system, "did we ship the retry fix?"]

while True:
    reply = model(messages, tools=[search_docs])   # 045, whole array, every time
    messages.append(reply)

    if reply has no tool call:
        return reply.text                          # the only way out

    for call in reply.tool_calls:
        result = run(call)                         # 051, my code, my api key
        messages.append(result)                    # 047, straight back in the array
```

thats it. i kept waiting for the special part, some agent mode you switch on. its a while loop. the model does exactly what 051 built, reads the array and either answers or asks for a tool. the loop around it is mine.

the exit is the line worth staring at. the loop ends when a reply has no tool call in it. i dont pick that moment. the model does, by answering instead of asking. that should bother you a little. it bothers me.

point that at my doc-QA thing from 070. round one it asks search_docs("retry fix"). my code runs it, appends the chunks, calls again. round two it asks search_docs("changelog"), the first pull wasnt enough. round three it answers. one question, three model calls.

how many rounds does it take? you dont know until you run it. arc 6 searched exactly once because i wrote it that way. here it goes until it stops, and three trips is where a nine second answer comes from.
