# 107: the ranking has never seen your task

builds on: [106](./106-three-fixes-that-fix-different-things.md), [072](./072-the-same-questions-every-run.md), [087](./087-the-two-numbers.md)
arc: the decisions, safety, privacy, and picking your model (9 of 10), ~2 min

106 picked the move, prompt harder or add retrieval or tune. this is the other half of that decision, which model runs it. for a long time i answered that by opening a public ranking and taking whatever sat on top.

| candidate | where it ranks publicly | passed my 50 |
|---|---|---|
| the big one | 1st | 39 |
| the mid one | 4th | 44 |
| the small one | 12th | 43 |

my task is one narrow thing, pulling item and price out of gujarati receipt text into a fixed json shape. a public rank is one average over a huge mixed bag, coding, trivia, long essays, and my narrow thing barely registers in that average. and the big one didnt fail at gujarati. it kept wrapping the json in a friendly sentence, and my grader counted every one of those wrong.

then the part i had to sit with. 44 and 43 out of 50 is not a real gap (076), those two are tied, so quality has stopped deciding anything here. the two numbers from 087 decide instead, and the small one is cheaper and answers faster.

the best bit is you already built the thing that picks the model. its your golden set (072). change the id, rerun, read the score.

feels obvious typed out. it wasnt obvious while i was scrolling a leaderboard hunting for a name to paste into a config.
