# 095: the model id you send is either a date or a moving pointer

builds on: [094](./094-when-every-attempt-is-gone.md), [041](./041-same-prompt-two-answers.md), [072](./072-the-same-questions-every-run.md)
arc: running it, speed, cost, and when things break (14 of 17), ~2 min

094 ended on the failure that isnt an outage. this is the shape of it. the model answers fine, it just isnt the same model.

```
// shipped in march. two ways to name what looks like one model

  { "model": "chat-fast-latest"     }   an alias, a pointer
  { "model": "chat-fast-2026-03-11" }   a snapshot, a date

// march 11, both land on the same parameters

  chat-fast-latest      ->  chat-fast-2026-03-11
  chat-fast-2026-03-11  ->  chat-fast-2026-03-11

// july 2, the provider ships a newer snapshot. nobody deployed anything

  chat-fast-latest      ->  chat-fast-2026-07-02   your app moved
  chat-fast-2026-03-11  ->  chat-fast-2026-03-11   still what you tested
```

i read that model field as a name. its a pointer. an alias resolves to whatever the provider currently ships under that label, a snapshot resolves to one frozen set of parameters (025). most providers publish both, they just spell the alias differently.

you already know this trade. `^1.2.0` against `1.2.0` in package.json. we pin those at my day job without discussing it, and the model field is the one place i keep seeing the caret left in.

the july line is a deploy you didnt run. nothing in git blame points at july 2, the line that changed isnt in your repo. nothing crashes either, the output just drifts. the json comes back with a field you didnt ask for, the prompt you spent an evening tuning stops behaving. 041 already said the same prompt varies run to run, so the drift hides inside noise you accepted months ago. feels obvious now, it wasnt this morning.

which is why the golden set from 072 catches this and nothing else does. its the only file you own that compares today against a recorded yesterday.

pinning isnt free either. a frozen snapshot gets retired on a date somebody else picked, and 096 is about that date.
