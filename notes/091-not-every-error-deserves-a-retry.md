# 091: not every error deserves a retry

builds on: [089](./089-wait-then-double.md), [090](./090-everyone-wakes-at-once.md)

arc: running it, speed, cost, and when things break (10 of 14), ~2 min

089 and 090 got the timing of the loop right. the loop is still wrong, because it retries everything that failed.

| what came back | retry it? | why |
| --- | --- | --- |
| 429 too many requests | yes | the meter from 088 refills, later works |
| 500 or 503 from the provider | yes | their box, and it may be fine in two seconds |
| timeout, connection reset | yes, carefully | see below |
| 401 bad api key | never | the same key is still the same key |
| 400 malformed request | never | your json is broken now and in eight seconds too |
| 404 no such model | never | you typoed the model name, attempt 5 has the same typo |
| 413 prompt too long | never | sleeping doesnt shrink your prompt |

the codes arent the rule, theyre the answer to it. the rule is one question: if i send these exact same bytes again, unchanged, could it work? a 429 could. a 500 could. a bad key cant, and no amount of doubling will change its mind.

my instinct is to wrap the call in try/except and retry whatever falls out. one line, feels safe. what it actually buys you on a bad key is five identical failures, 15 seconds of sitting still, and five requests spent on the meter for nothing. the user waits fifteen seconds for the error they were getting anyway.

the timeout row is the one i kept misreading. a timeout says you stopped waiting. it does not say the model stopped working. that call may have finished, and billed. retry it, but if it writes anything downstream, make running it twice safe.

go read your retry wrapper. if it catches Exception, its retrying your typos.

092 is the other half, what you do when the retryable one just keeps coming back.
