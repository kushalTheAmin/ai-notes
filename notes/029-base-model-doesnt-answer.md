# 029: a base model doesnt answer, it continues

builds on: [028](./028-numbers-frozen-on-a-date.md), [022](./022-guess-the-next-token.md)
arc: whats inside the box (8 of 10), ~2 min

028 left that file frozen, and full of text where nobody was answering me. so what comes back if you send it a question.

```
one prompt, two files of numbers

prompt:  how do i center a div in css?


--- base model, straight out of 028's training lane ---

  how do i center a div in css?
  how do i make a footer stick to the bottom?
  why does my flexbox child overflow?

  asked 3 hours ago  |  12 answers  |  tags: css, html


--- assistant model, those numbers after a second pass ---

  flexbox is the usual one:

    .parent { display: flex;
              align-items: center;
              justify-content: center; }

  if the parent has no height, set one.
```

thats a real thing, you can download one and run it. its not broken and its not ignoring you. its doing 022, guessing what comes next, and on the pages it read a question is usually followed by more questions.

the fix is another round of exactly the training from 028, just tiny. a pile of examples all shaped the same way, heres a request, heres a good reply. same guessing game, same nudge when the guess is off, over conversations this time. next to the first pass its a rounding error.

after that, the likely continuation of a question is an answer. thats the whole change. same size file, same loop, still picking one token at a time.

theres a further round after that where people rank two replies and the numbers get nudged toward whichever won. most of the tone and the refusals come from there.

i had this backwards. i assumed the helpfulness came from the big expensive pass and the bit on the end was polish. its the other way round.

ever watched a model drift into writing your next message for you, inventing what you said back? thats the base model showing through.
