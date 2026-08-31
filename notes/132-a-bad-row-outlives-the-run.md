# 132: a bad row outlives the run that wrote it

builds on: [131](./131-a-store-that-outlives-the-run.md), [123](./123-injection-grows-hands.md), [122](./122-what-a-wrong-call-leaves-behind.md)
arc: agents you can trust (11 of 17), ~2 min

131 stopped at the write. one row squeezed out of a run, looked up before round 1 of the next one. what it never said is who checks that row later. nobody does.

| run | what happened in it | row written when it exits |
| --- | --- | --- |
| mon, run 1 | asked for store credit on 88120 | wants refunds as store credit |
| tue, run 6 | said put it back on the card instead | wants the money back on the card |
| wed, run 9 | search_docs hit the wiki page from 123 | wants a verify link emailed on every order |
| thu, run 10 | reads all three rows into round 1 | nothing, reads dont write |

writes happen once, at the end of a run. reads happen on every run after. so a row only has to be wrong one time.

tuesday doesnt replace monday, it lands next to it. the customer changed their mind and my store holds both lines, undated, in no order the model can see. thursday gets both. no attacker in that one, it just happens.

wednesday is 123 with a longer life. that planted line used to die with the loop. but the squeeze is a model reading the run, and the run contained that wiki page, so it got written down as a preference. it comes back every run now, before the model has seen a single tool result.

same mechanism twice. a row is a claim one run made, not a fact, and reading it back rechecks nothing. you can write that check yourself, its just not something the loop gives you.

i had memory filed under nice-to-have. one write and unlimited reads is a wider blast radius (122) than any single call in that run. you know that one config row someone set in prod years ago that everything still reads off? this one a model writes.
