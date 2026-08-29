# 084: why the ui types

builds on: [082](./082-a-while-loop-with-a-model-inside.md), [083](./083-when-the-loop-wont-stop.md), [022](./022-guess-the-next-token.md), [050](./050-when-the-json-breaks.md)
arc: running it, speed, cost, and when things break (3 of 11), ~2 min

082 got a nine second answer out of three rounds, and 083 let it run to six before killing it. the wait is real. streaming is what you do about the wait.

one 300 token answer. the model starts writing after 0.3s, then writes about 75 tokens a second.

| | one shot | streaming |
| --- | --- | --- |
| first text on screen | 4.3s | 0.3s |
| last word on screen | 4.3s | 4.3s |
| what your code holds | one finished string | pieces, joined as they land |

read the middle row twice. same 4.3 seconds either way. i had streaming filed under speed and its not, the answer doesnt arrive sooner. only the waiting changed shape.

it works because of 022. the model was always writing one token at a time. the plain call holds them all until the last one lands, then hands you the pile. streaming skips the holding. tokens leave as theyre picked.

on my react side thats a state update per chunk, which is the whole reason the cursor crawls.

the cost is that your code has no complete answer until the end. you cant know json (050) is valid until the stream closes, so you buffer the pieces anyway. errors can land after youve already painted three good paragraphs, and then you get to un-paint them.

085 is caching, and that one comes off the actual bill.
