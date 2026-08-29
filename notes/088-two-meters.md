# 088: two meters, and you trip whichever empties first

builds on: [087](./087-the-two-numbers.md), [053](./053-what-to-leave-out.md), [004](./004-tokens-are-money.md)
arc: running it, speed, cost, and when things break (7 of 12), ~2 min

087 was my budget, two numbers i picked. this is a cap the provider picked, and it doesnt care about mine.

```
my tier: 60 requests a minute, 200,000 tokens a minute

  a minute of              requests             tokens
  61 tiny classify calls   61 of 60    OVER     9,455 of 200,000
  18 big doc-QA calls      18 of 60             230,400 of 200,000   OVER
```

both rows get the exact same thing back, http 429, too many requests. thats the bit that took me a minute. its separate meters and you only have to empty one.

top row is a classify feature, tiny prompts, 155 tokens a call. it gets cut off sitting under 5 percent of its token allowance. bottom row is the doc-QA thing from 087. 18 calls in a whole minute, basically no traffic, but each one carries a pile of retrieved chunks (053), so roughly 12,800 tokens go up the wire every time. 18 times 12,800 is 230,400.

so the first question on a 429 is which meter, because the fixes pull opposite ways. batch your work into fewer, fatter calls and you fix the top row while making the bottom one worse.

two things my table smooths over. its not a clean reset at the top of each minute, its a rolling window, so the meter is always leaking back a bit. and some providers count input and output tokens on separate meters, so its more lines than my two.

089 is what you actually do when the 429 lands. doing nothing for a moment turns out to be the right move.
