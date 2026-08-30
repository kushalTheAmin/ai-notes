# 109: when the answer stops being a suggestion

builds on: [108](./108-the-order-i-ask-them-in.md), [082](./082-a-while-loop-with-a-model-inside.md), [051](./051-the-model-asks-your-code-acts.md), [104](./104-ten-wrong-answers-a-day.md)
arc: agents, when output starts doing things (1 of 13), ~2 min

108 closed on the question i keep coming back to, where does a wrong answer land. the bottom row of 104 was the feature that acts with nobody watching. this whole arc is that row.

```
same question, same model, same 95%. two shapes of reply.

  reply.text
    "you should refund order 4471, it shipped twice"

    -> renders in a chat bubble
    -> i read it, i decide, i click the button
    -> wrong = a sentence you scroll past

  reply.tool_calls
    [ { name: "issue_refund", args: { order: 4471 } } ]

    -> goes to my code (051)
    -> run(call), the money leaves
    -> loop appends the result and calls again (082)
    -> wrong = a refund that already happened
```

nothing about the model changed between those two blocks. same weights, same prompt, same error rate. what changed is the shape of the field i read the answer out of.

the top block is every note in this repo so far. text comes back, a person is in the way, and being wrong 5% of the time costs you a scroll.

the bottom block is 051 dropped into 082s loop. the reply is a name and some arguments, and the gap between the model saying it and it being true is however long run(call) takes. took me a while to stop reading that as the model getting riskier. it didnt. i just deleted the person who used to sit between the two.

worth saying, my code is still the thing that calls run. nothing forces me to. but the loop in 082 doesnt ask, it just runs, and thats the default you start from.

next note is where those tool names come from, and theyre not config.
