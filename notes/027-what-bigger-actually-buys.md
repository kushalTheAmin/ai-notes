# 027: what a bigger model actually buys

builds on: [026](./026-every-number-every-token.md), [007](./007-cant-count-letters.md)
arc: whats inside the box (6 of 10), ~2 min

026 said a bigger model bills more per token out. so the obvious question, more of what.

| what i ask | 8B | 405B |
|---|---|---|
| summarize this email | fine | fine |
| a gujarati proverb i half remember | invents one | usually has it |
| refactor 300 lines of typescript, keep behaviour | drifts by the end | holds it together |
| how many r's in "strawberry" | wrong | often right |
| add two 12 digit numbers | shaky | shaky |

the top row doesnt move because the small model already had it. you just paid more for the same paragraph.

the two middle rows are where the money actually goes, and theyre the same thing underneath. how much text got memorized, and how much of your instruction it keeps hold of while writing a long answer. more parameters (025) buys room for both. thats the purchase.

the strawberry row looks like another win. its the memorizing one again. 007: the r's are gone before the model receives anything, it holds ids. fifty times the numbers still gets a list with no r in it, so a big model getting that right read the spelling somewhere. and 008s digit chunks dont move at all.

i kept waiting to find a size where the model just gets it, some threshold. theres no threshold. theres a bigger pile of the same guessing.

022 still holds at 405B, its picking a likely next token. so a big model is wrong less often and much more convincingly, and that second half is the one that bites you.
