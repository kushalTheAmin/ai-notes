# 007: why a model cant count letters
builds on: [002-what a token is](./002-what-a-token-is.md), [006-the context window](./006-context-window.md)
arc: how machines read text (7 of 10), ~2 min

006 finished the money and space side of tokens. this is the other side, where tokens make a model look dumb at something a kid can do.

```
"how many r's in strawberry?"

what you see
  s t r a w b e r r y
      ^         ^ ^        three of them

what the model gets
  str  |  aw  |  berry     <- one real tokenizer, real ids
  496     675    15717

  [496, 675, 15717]
```

look at that bottom row. no letter r in it. no letters at all. the word walked in as three integers and the spelling got left at the door, exactly like roti became rot and i back in 002.

so when a model answers "two", its not bad at counting. it never got the thing you asked it to count. when it does get this right, its because enough text in training spelled words out letter by letter and it memorized that berry holds two r's, the same way it memorized paris is in france. recalled, not looked at.

i find this genuinely funny. the same model writes me a working react component and then miscounts letters in a word. those two feel like they belong on one difficulty scale. they dont.

you will hit this the second you ask a model to reverse a string or count characters in one. the fix isnt a better prompt. do it in code, or ask the model to write the code that does it.
