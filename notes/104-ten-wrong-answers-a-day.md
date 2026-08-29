# 104: shipping a feature that gets it wrong on purpose

builds on: [103](./103-every-call-makes-two-copies.md), [038](./038-why-the-made-up-answer-sounds-right.md), [094](./094-when-every-attempt-is-gone.md)
arc: the decisions, safety, privacy, and picking your model (6 of 10), ~2 min

103 ended on a limit i cant code around. same move here, pointed at the model itself. 094 was the call dying, this is the stranger one, the call works fine and the answer is just wrong. 038 said thats not a bug with a patch on it, so at 200 requests a day and 95% right, thats 10 wrong answers a day. every day. forever.

| the same model, same 95% | who catches the wrong one | what one costs |
| --- | --- | --- |
| drafts a reply, i press send | me, before it leaves | 5 seconds |
| answers with its 3 chunks shown (059) | the reader, against the source | one scroll |
| files the ticket silently | nobody, until someone goes looking | an hour, next month |
| issues the refund on its own | the finance report | real money |

i kept reading that 10 as a number to shrink. it is one, arc 7 is all about measuring it and pushing it down, but it never lands on zero. so the knob that actually moves is the other one. every row up there is the same model at the same accuracy, and what changes is where the answer lands.

top two rows, somebody sees the answer and has a way to tell. bottom two, it takes effect while nobody is watching.

so which row is your feature? if its the bottom half, the fix usually isnt a better prompt. its moving the feature up a row. add a confirm step, show the source, let the model draft and let a person press the button.

one caveat, 5% isnt a number you get to assume, yours needs measuring (072). and it wont spread evenly, the strange inputs fail far more than the easy ones.

105 changes the question completely, do you rent the model or own it.
