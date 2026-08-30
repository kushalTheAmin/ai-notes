# 006: the context window
builds on: [005-why hindi and gujarati cost more than english](./005-hindi-gujarati-cost-more.md), [004-tokens are money](./004-tokens-are-money.md)
arc: how machines read text (6 of 10), ~2 min

005 ended on those extra tokens filling up something besides your bill. this is that something. every model has a hard ceiling on how many tokens a single request can hold, and thats the context window.

```
model context window: 200,000 tokens

this request:
  app instructions          1,200
  conversation so far     178,400
  your new message            900
  --------------------------------
  input total             180,500

  200,000 - 180,500 = 19,500 left

  the reply has to fit in that 19,500
  ask for 25,000 back -> the call errors
```

heres the part i kept misreading. the window isnt "how much you can send". its the whole request, what you send plus what the model writes back, sharing one budget. put 180,500 tokens into a 200,000 token window and the model has 19,500 tokens of room to answer in. thats it.

so a long conversation doesnt only cost more, 004 covered that part. it quietly eats the space left for the answer. if your app resends the whole thread every turn, and most apps do, you are shrinking the reply with every message you add.

two caveats that keep this true. providers usually cap the reply separately too, often well under whatever is left over, so that leftover isnt automatically yours. and going over doesnt trim anything for you, the api just rejects the call. deciding what to drop is on your code.
