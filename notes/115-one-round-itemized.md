# 115: one round of the loop, itemized

builds on: [114](./114-no-tool-call-isnt-done.md), [083](./083-when-the-loop-wont-stop.md), [085](./085-the-part-that-never-changes.md), [110](./110-the-toolbox-is-written-in-english.md), [111](./111-the-arguments-cant-come-out-malformed.md), [113](./113-a-failed-tool-call-goes-back-in.md)
arc: agents, when output starts doing things (7 of 13), ~2 min

114 gave the loop a way to know when its finished. this is what the rounds before that cost.

| part of round 3s array | tokens | who wrote it |
|---|---:|---|
| system prompt | 120 | me |
| search_docs schema (110, 111) | 180 | me |
| "did we ship the retry fix?" | 14 | me |
| round 1 reply: call search_docs | 30 | the model |
| round 1 result: 4 chunks | 1,300 | my tool (113) |
| round 2 reply: call search_docs | 30 | the model |
| round 2 result: 4 chunks | 1,300 | my tool (113) |
| what round 3 posts | 2,974 | |

083 said a round appends about a thousand tokens and did the addition across rounds. that holds up. i just never opened a single round and read the line items.

my question is 14 tokens. round 3 posts 2,974. the model itself wrote 60 of them.

two of these lines exist only because this is an agent. the schema block rides along on every round, including the rounds where nothing gets called, because a tool has to be in the prompt to be callable at all. and every result stays in the array for good (113), full text, since the model needs to see what it already found.

085 itemized one call and most of that bill sat in a stable prefix i could cache. here its flipped. the part that never changes is 314 tokens, under 085s cache minimum anyway, and the two big lines are new every round.

felt like opening a bundle analyzer for the first time. the thing you wrote is the thin slice. go add up your own agents tool results sometime.

2,600 of 2,974 is text a tool handed back. thats 116s whole problem.
