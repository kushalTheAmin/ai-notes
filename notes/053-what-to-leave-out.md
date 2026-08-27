# 053: the context budget, deciding what to leave out

builds on: [052](./052-when-the-text-isnt-mine.md), [051](./051-the-model-asks-your-code-acts.md), [047](./047-your-code-fakes-the-memory.md), [006](./006-context-window.md)
arc: the prompt is the program (9 of 11), ~2 min

052 left me suspicious of the ticket text my tool went and fetched. turns out theres a second problem with that text. its 3,900 tokens.

```
one turn of my support bot. model window: 8,000 tokens (006)

  what im putting in the array         tokens   if it has to go
  --------------------------------------------------------------
  system prompt and rules                 400   no, its the job
  4 few-shot examples (048)               800   drop 2      -> 400
  chat history, 18 turns (047)          2,600   keep last 6 -> 900
  ticket text my tool fetched (051)     3,900   trim it     -> 800
  this turns question                     100   no
  --------------------------------------------------------------
  input                                 7,800
  room left for the answer                200   the answer needs more

  after those three cuts
  input                                 2,600
  room left for the answer              5,400
```

047 said what you drop when it stops fitting gets its own note. this is it.

heres what i got wrong. i assumed the chat history would be the row crushing me, since thats the one that grows every single turn. youd probably guess history too. it wasnt even close. one raw tool result was nearly half the window by itself.

so i stopped ranking these by importance. what actually decides it is how much room a cut gives back against how much it costs me, and the biggest dump of fetched text usually wins that trade in one move. the system prompt and the actual question arent in the pool at all. cutting either one breaks the thing im building.

none of the three cuts here are clever. fewer examples, a shorter history window, truncate the tool result before it ever hits the array. they just have to be a decision my code makes on purpose, because 006 was clear that the api trims nothing for you, it rejects the call.

one bonus i didnt expect. trimming that ticket also puts less untrusted text in front of the model (052).
