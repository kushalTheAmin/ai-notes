# 040: how the loop actually stops

builds on: [037](./037-no-row-for-i-dont-know.md), [022](./022-guess-the-next-token.md)
arc: how it writes, and the knobs you own (9 of 12), ~2 min

037 dropped a real done token into the vocabulary and then walked straight past it. i want that one back. after three notes on what the loop wont tell you, heres the part that works.

prompt: `"name 3 gujarati snacks, numbered"`

| what ended the loop | what my code gets back | stop_reason |
| --- | --- | --- |
| nothing set, `<done>` won a row | `1. dhokla 2. fafda 3. thepla 4. khakhra` | `end_turn` |
| `stop_sequences: ["4."]` | `1. dhokla 2. fafda 3. thepla` | `stop_sequence` |
| `max_tokens: 12` | `1. dhokla 2. fa` | `max_tokens` |

(where a token ceiling lands mid-word depends on the split from 003)

row one is the model deciding. `<done>` wins a row like any other token, the loop from 022 breaks, and you get everything it wrote. i asked for 3 snacks and got 4, which is very on brand.

rows two and three are you, cutting from outside. took me a second to see how different they are. a stop sequence isnt something the model knows about. it wrote that `4.` happily, and the api matched your string against the text on the way out. max tokens never looks at the text at all. count tokens, hit the ceiling, cut. mid word, mid thought, doesnt care.

heres the one that would have bitten me. row three still looks like an answer, and sometimes the cut lands after a full stop and reads finished. the only place that difference lives is the flag. anthropic calls it stop_reason, openai calls it finish_reason.

you cant tell a cut answer from a finished one by reading it.
