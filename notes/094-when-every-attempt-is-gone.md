# 094: what the user gets when every attempt is gone

builds on: [093](./093-a-second-model-when-the-first-is-down.md), [086](./086-the-same-question-twice.md), [059](./059-search-the-chunks-then-paste-them-in.md)
arc: running it, speed, cost, and when things break (13 of 16), ~2 min

093 ended on a box i drew and then said nothing about, nothing left to serve. retries gone, backup provider gone. your code still has to hand something back to a person sitting there waiting.

| what you serve | what they see | what it costs you |
| --- | --- | --- |
| no plan | a spinner that never stops, or a red 500 | nothing, its the default |
| a plain error | "cant reach the model, try in a minute" | one if block |
| cached answer (086) | a real answer, maybe stale, marked stale | already built |
| chunks, no model (059) | the 3 source paragraphs, no summary | wire retrieval to the ui |
| a queue | "we will email you when its back" | a job store and a sender |

i filed this under error handling for months. its a product decision. skip it and you still picked a row, the top one, because a spinner that never resolves is what your code does when nobody chose.

the two middle rows are the interesting ones because you already paid for them. the semantic cache from 086 probably holds a near match to this question. and in doc-QA the retrieval from 059 finished before the model call died, so those chunks are sitting in a variable right now. three source paragraphs with no summary on top still answers plenty. that one got me, a doc-QA feature with no model in it is not useless.

one rule for both: say so. a stale answer handed over as a fresh one is worse than the error, since nobody can tell, including you when the complaint arrives.

thats the model being down. next one is stranger, the model doesnt go down at all, it gets deprecated out from under you.
