# 097: what your http log line is missing

builds on: [095](./095-a-date-or-a-moving-pointer.md), [096](./096-a-date-somebody-else-picked.md), [087](./087-the-two-numbers.md)
arc: running it, speed, cost, and when things break (16 of 17), ~2 min

095 and 096 were both failures that never threw anything you could see. a pointer that moved, an id with an expiry on it. so what would you have had to write down to catch either one.

```jsonc
{
  "ts": "2026-08-29T14:02:11Z",
  "route": "/summarize",
  "status": 200,
  "ms": 2140,

  "model": "chat-fast-2026-03-11",  // who actually answered (095, 096)
  "prompt_version": "summarize@7",  // which prompt was live (077)
  "tokens_in": 1840,                // where the bill came from (087)
  "tokens_out": 210,
  "cached_in": 1600,                // did the cache hit (085)
  "finish": "stop",                 // clean stop, or cut at the cap (040)
  "attempt": 2,                     // did a retry pay for this (089)
  "request_id": "req_01HX9K"        // the id support will ask for
}
```

the top four lines are what our request logging at work already writes, status and duration, and for a rest call thats honestly enough. everything under the gap is stuff a model call needs and a normal http call never did.

model is the field i would have skipped. it looks like a constant, its sitting right there in the config. but an alias moves under you (095), and a fallback answers from a different model entirely (093), so the id that replied isnt always the one you asked for. logging it turns "was this the same model last tuesday" into one query.

tokens_in and cached_in are where the money lives. a spend spike is either more calls or fatter prompts, and without those two you are guessing which. attempt is quieter, it tells you retries are eating your latency budget (087) before a user does.

the tempting fields are the prompt text and the answer text. thats also exactly where user data ends up, so logging them is a decision, not a default. arc 9 has that one.
