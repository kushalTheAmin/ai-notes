# 092: how long do you wait before you stop waiting

builds on: [091](./091-not-every-error-deserves-a-retry.md), [089](./089-wait-then-double.md), [087](./087-the-two-numbers.md)

arc: running it, speed, cost, and when things break (11 of 17), ~2 min

091 said a timeout means you stopped waiting. i wrote that down and then noticed i had never actually decided when.

```
087s budget: 1 second to first text
089s loop:   5 attempts, sleeping 1s, 2s, 4s, 8s between them

the provider is hanging. nothing comes back.

  no timeout
    attempt 1 waits ... forever

  timeout 30s
    5 attempts x 30s   = 150s waiting
    the sleeps         =  15s
    the user waits       165s

  timeout 5s
    5 attempts x 5s    =  25s
    the sleeps         =  15s
    the user waits        40s

  timeout 5s, 2 attempts
    2 attempts x 5s    =  10s
    one sleep          =   1s
    the user waits        11s
```

that number is yours whether you pick it or not. some sdk clients default to ten minutes, and plain fetch in my react app doesnt time out at all unless i hand it an abort signal, so "i didnt set one" quietly means "forever".

then the part that got me. the timeout is not the wait. 089 runs the call five times with sleeps stacked in between, so 30 seconds is really 165, against the 1 second 087 wrote down. tighten it to 5 and youre at 40. cut to 2 attempts and youre at 11, which is still eleven times the budget.

one caveat, if youre streaming (084) then time the wait to the first token, not the whole answer. a long answer is allowed to take long.

so the timeout and the retry count are one decision. i had them in two different files and never added them up.
