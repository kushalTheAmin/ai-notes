# 046: system vs user, and why system usually wins

builds on: [045](./045-roles-are-markers.md), [030](./030-fine-tuning-shape-not-facts.md), [029](./029-base-model-doesnt-answer.md), [022](./022-guess-the-next-token.md)
arc: the prompt is the program (2 of 11), ~2 min

045 ended on me having role filed wrong in my head, as a field the serving code branches on. it left a hole though. if system is just a marker sitting in the same flat stream the user text sits in, whats actually making the model obey the system message?

```
what i pictured happening:

  if (user.conflictsWith(system)) {
    obey(system)                    // a rule. checked, every call
  }

what actually runs:

  stream = flatten([system, user])  // 045. the role picks a marker, thats all
  loop { guessNextToken(stream) }   // 022

  // nothing in there compares the two messages
  // system wins because 029 and 030 made following it the habit
  // and a habit is a strong lean, not a check
```

i went looking for the check and there isnt one. the role decides which marker token goes in and then its all just text.

so the lean comes from tuning. that second pass in 029 was full of examples where whatever sat after the system marker got followed, and the ranking round after it pushed the same way. following the system message became the likely continuation. thats the entire mechanism.

which means system does buy you something real. its a reliable default and newer models hold it better because theyre trained harder on exactly this. what it doesnt buy you is a guarantee. a vague system line like "be helpful and concise" up against a very specific user instruction is not a fight system always wins. specific tends to beat vague.

feels obvious now, wasnt this morning. i had been writing system prompts like config and they behave more like a strongly worded comment.
