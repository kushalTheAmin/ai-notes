# 045: roles are markers inside one stream of tokens

builds on: [044](./044-one-token-on-the-way-out.md), [022](./022-guess-the-next-token.md), [002](./002-what-a-token-is.md)
arc: the prompt is the program (1 of 11), ~2 min

044 ended on the only lever i had left, what i send in. so i opened the request body to look at it properly, and theres no prompt string in there. its an array, and every item carries a role.

```
what i post:

  [
    {"role": "system", "content": "reply in one short line"},
    {"role": "user",   "content": "kem cho?"}
  ]

what the model reads:

  <start>system<sep>reply in one short line<end>
  <start>user<sep>kem cho?<end>
  <start>assistant<sep>
  ^                    ^
  |                    +- nothing after this. it guesses from here
  +- marker tokens, a few per message. you pay for these too
```

top block is the json i post, same shape as any api i hit from typescript. bottom block is what the provider turns it into first. one flat list of tokens, the ordinary kind from 002. the roles survive as small marker tokens saying where a message starts, whose it is, where it ends.

the last line is what made it click. the whole thing ends on the assistant marker. so the model is doing what 022 said it does, guessing the next token, and everything above it, my system message included, is just text its continuing from.

markers differ per model and hosted apis dont show you theirs, but the shape holds everywhere. some apis take the system text as its own field instead of an array item, it lands in the same stream either way.

took me a minute. i had role filed as a field the serving code branches on.
