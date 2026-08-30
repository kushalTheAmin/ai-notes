# 089: when a 429 lands, wait, then double the wait

builds on: [088](./088-two-meters.md), [087](./087-the-two-numbers.md)
arc: running it, speed, cost, and when things break (8 of 17), ~2 min

088 left you holding a 429 with nothing to do about it. this is what you do. you sleep.

```
wait = 1 second

for attempt in 1 to 5:
    reply = call_model(prompt)
    if reply.status is not 429:
        return reply
    if attempt is 5:
        give_up()
    sleep(wait)
    wait = wait * 2

# the waits, in order: 1s, 2s, 4s, 8s
# worst case, 5 calls and 15 seconds of sitting still
```

my instinct was to fire the retry straight away, thats what i do with a flaky network call. here it makes things worse. the meter from 088 refills as the window rolls, so an instant retry turns up while its still empty and you burn a try to learn nothing.

so why double it instead of waiting one second every time? because you dont know how far over the line you are. one call over and youre clear almost immediately. a batch job hammering the same api key needs a lot longer. doubling finds that out for you, cheap probes first, backing off harder each time the answer is still no.

the cap earns its place as much as the doubling does. take out the 5 tries and the waits just keep growing, and your user left a while back.

the bit i didnt know: providers usually send a retry-after header on the 429 telling you exactly how long to hold. if its there, use it. the doubling is for when its not.

and those 15 seconds come straight out of the latency budget from 087, before the model has written a single token.
