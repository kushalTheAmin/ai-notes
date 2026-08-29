# 101: whats in the request that nobody typed today

builds on: [100](./100-two-gates-around-the-call.md), [061](./061-filter-before-you-search.md), [059](./059-search-the-chunks-then-paste-them-in.md), [047](./047-your-code-fakes-the-memory.md)
arc: the decisions, safety, privacy, and picking your model (3 of 10), ~2 min

100 put a gate in front of the call that reads what the user sent. so i went and read the rest of what gets sent.

```jsonc
// one question to my support bot. the array leaving my server.
[
  { "role": "system", "content":
      "you are acme support. agent on shift: priya s, ext 4102" },
  // wrote this months ago. it ships on every call, forever

  // ...11 earlier turns of this chat (047), all still attached
  // whatever anyone typed on turn 3 rides along on turn 12

  { "role": "user", "content":
      "past ticket 8812, rahul m, card 4417, agent note: called 98765 43210" },
  // nearest chunk my retriever pulled in (059)

  { "role": "user", "content": "did my refund go through" }
]
```

one line down there is what a human typed today. everything above it my code attached.

the system message i wrote once and stopped seeing. the history is 047 doing its job, my code re-sending the chat so the model has memory. the chunk is 059, whatever scored nearest. when did you last read what your retriever actually hands over?

heres the bit that got me. 061 already filters retrieval by permission, so my bot is allowed to read that ticket. allowed to read and ready to leave the building are different questions, and i had them filed as one. that card tail belongs to somebody who asked nothing today.

none of it is automatically wrong. you send the chunk because the answer needs it. 097 said logging the prompt text is a decision, but the leaving happens before any log line, on every call.

102 is where i start taking some of it back out.
