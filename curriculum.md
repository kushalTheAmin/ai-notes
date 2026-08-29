# curriculum

## ARC 1 - how machines read text
- [x] characters vs words, and why both fail (001)
- [x] what a token is (002)
- [x] BPE: merging by frequency (003)
- [x] tokens are money: how pricing actually works (004)
- [x] why hindi and gujarati cost more than english: tokens per word isnt equal (005)
- [x] context window (006)
- [x] the model cant see inside a token: why it cant count letters (007)
- [x] numbers get chunked, not counted: why arithmetic gets shaky (008)
- [x] a space or a capital letter changes the ids (009)
- [x] CAPSTONE: what the model sees, and what it costs, when i send a request (010)

## ARC 2 - meaning as numbers
- [x] a vector is a list of numbers (011)
- [x] dot product, by hand (012)
- [x] cosine similarity (013)
- [x] what an embedding is (014)
- [x] nearby means similar (015)
- [x] one word, many meanings: context changes the vector (016)
- [x] embedding models are separate products from chat models (017)
- [x] classify with no training: nearest labeled example wins (018)
- [x] near-duplicates: the same score, with a threshold on it (019)
- [x] clustering: finding the groups when nothing is labeled (020)
- [x] CAPSTONE: how search by meaning works end to end (021)

## ARC 3 - whats inside the box (enough to not be fooled, no more)
- [x] next-token prediction is the whole game (022)
- [x] attention in one note: every token looks at every other token, the superpower and the cost (023)
- [x] why compute scales badly with input length (024)
- [x] a parameter is one number the model learned, and 8B is how many (025)
- [x] the model reads every parameter to write one token (026)
- [x] what a bigger model actually buys, and what it doesnt (027)
- [x] training vs inference: baked-in knowledge has a cutoff (028)
- [x] base model vs assistant: what tuning changed (029)
- [x] what fine-tuning can fix and what it cant (030)
- [x] CAPSTONE: the box, closed. everything an applied engineer must know about internals and nothing more (031)

## ARC 4 - how it writes, and the knobs you own
- [x] logits to probabilities (032)
- [x] temperature (033)
- [x] greedy vs sampling: two ways to pick a row (034)
- [x] top-k: keep the best few rows, then rescale what survives (035)
- [x] top-p: cut by running total, and why a fixed k gets it wrong (036)
- [x] theres no row for "i dont know": the list always adds to 100 and something always wins (037)
- [x] why the made-up answer sounds right, and why its not a bug you can patch (038)
- [x] asking the model how sure it is, and why you cant trust the answer (039)
- [x] stop sequences and max tokens (040)
- [x] determinism: why the same prompt varies and what that breaks (041)
- [x] reasoning models: the model does its working out in the open (042)
- [x] thinking tokens on the bill: paying for output you dont get to read (043)
- [x] CAPSTONE: one tokens journey out, and every knob you control (044)

## ARC 5 - the prompt is the program
- [x] the request is a list of role-tagged messages, and it all becomes one token stream (045)
- [x] system vs user: what outranking buys you, and what it doesnt (046)
- [x] conversation state: the model remembers nothing, your code fakes the memory (047)
- [x] few-shot: showing beats telling (048)
- [x] structured output: getting json you can actually parse (049)
- [x] when json breaks: validation and retry (050)
- [x] tool calling: the model asks, your code acts (051)
- [x] prompt injection: user input IS code now (052)
- [x] context budget: what to include when you cant include everything (053)
- [x] images in: multimodal requests without the mystery (054)
- [x] CAPSTONE: anatomy of a production prompt (055)

## ARC 6 - RAG: giving the model your data
- [x] closed-book vs open-book (056)
- [x] long context vs retrieval: when you can just send everything, and when you cant (057)
- [x] chunking: the decision that quietly decides quality (058)
- [x] retrieval: embed, search, stuff the context (059)
- [x] where vectors live: from scanning every doc to a real index, and what approximate costs (060)
- [x] filtering before searching: metadata, permissions, and why vector search alone isnt enough (061)
- [x] why retrieval fails: the vocabulary gap (062)
- [x] keyword search: the literal word match, and what it catches that meaning misses (063)
- [x] hybrid: merging two ranked lists when the scores dont compare (064)
- [x] the reranker: one model reads your question and the chunk together (065)
- [x] two-stage retrieval: search wide and cheap, sort narrow and expensive (066)
- [x] recall@k: did the right chunk come back at all (067)
- [x] mrr: recall throws away where in the list it landed (068)
- [x] groundedness: did the answer come from the docs (069)
- [x] CAPSTONE: doc-QA system end to end, every design decision named (070)

## ARC 7 - evals: how you know any of it works
- [x] "looks good" doesnt scale (071)
- [x] the golden dataset: 50 examples beat vibes (072)
- [x] exact match vs semantic scoring (073)
- [x] llm-as-judge: hand the answer to a model and ask it to grade (074)
- [x] where the judge tilts: longer answers, its own style, and everything passing (075)
- [x] the score moved, is it real: why small eval sets lie (076)
- [x] regression: the prompt change that broke three other things (077)
- [x] evals in ci: treating prompts like code (078)
- [x] error analysis: stop guessing, read the failures and bucket them (079)
- [x] after you ship: thumbs, feedback, and checking quality in the wild (080)
- [x] CAPSTONE: an eval harness for the arc 6 system (081)

## ARC 8 - running it: speed, cost, and when things break
- [x] an agent is a while loop with an llm inside (082)
- [ ] when the loop goes wrong: runaway agents and hard stops
- [ ] streaming: why the ui types
- [ ] provider prompt caching: pay less for the part of the prompt that never changes
- [ ] semantic caching: the same question twice shouldnt cost twice
- [ ] latency and cost budgets: the two numbers that kill llm features
- [ ] rate limits and retries
- [ ] when the provider is down: timeouts, fallbacks, failing gracefully
- [ ] the model changes under you: pinning versions and surviving deprecations
- [ ] observability: logging llm calls like http calls
- [ ] CAPSTONE: what happens after deploy, keeping an llm feature alive

## ARC 9 - the decisions: safety, privacy, and picking your model
- [ ] should this even be an llm: when boring code wins
- [ ] content moderation: the filter in front of and behind the model
- [ ] data leaves the building: pii, redaction, and what the api keeps
- [ ] designing for wrong: shipping a feature that fails 5% of the time, on purpose
- [ ] api models vs open weights: renting a model vs owning one
- [ ] which lever: prompt harder, add retrieval, or fine-tune
- [ ] model selection: picking by task, not leaderboard
- [ ] CAPSTONE: the checklist i would run before shipping any llm feature

## THREAD
baton: 082 opened arc 8 by putting the arc 5 call inside a while loop. the loop posts the whole array (045 047), the model either answers or asks for a tool (051), my code runs the tool and appends the result, round again. the exit is the only interesting line, the loop ends when a reply comes back with no tool call in it, and the model owns that moment, not me. the trace is a doc-QA question (070) taking three rounds, so one question is three model calls, which is where 081s nine second answer comes from. it does not touch what happens when the model never stops asking, that is deliberate, the next checkbox owns it.

next is "when the loop goes wrong: runaway agents and hard stops". it picks the baton up exactly where 082 left it, at `while True` with a single exit the model controls. the honest shape is the caps my code puts around a loop it does not control, a max round count, a token or dollar ceiling, a wall clock timeout, and the money angle is real since every round re-sends a longer array (047, 004). do not let it become a note about a framework or a safety lecture. and do not spend the streaming or the cost-budget material, those are their own checkboxes later in this arc.

bm25 scoring stayed a missing brick through all of arc 6 and that was correct. 064 prints a keyword score as a bare number on purpose, since the point is that the scale is unknowable to you. it stays unlaid, dont let a later arc drag it in.

process note: 073 at 191, 074 at 202, 075 at 218, 076 at 200, 077 at 208, 078 at 215, 079 at 208, 080 at 217, 081 at 346 (capstone ceiling), 082 at 190. 082 landed at the bottom of the band on purpose after eleven notes clustered at 190 to 221. keep breaking the flatness, the next one should aim 140 to 175 or push toward 240, not park at 200 again.

last visuals: pseudocode, the whole agent loop in one block with the earlier note numbers hung on the three lines that were already built (082), annotated artifact, the evals/ folder listed out with every file carrying the note number that built it (081), mermaid flowchart, one weeks traffic splitting into thumbs and a random sample (080). so no pseudocode next, and a worked example with real numbers would fit a note about caps and ceilings well.
last exits: stops (082), forward (081), stops (080). one of the last three points forward, so 083 may point forward or stop, its free.

process note on visuals: mermaid stacks subgraphs in whatever order it likes and it flipped the two on 065, and on 070 it put the once-per-doc group beside the per-question one rather than above it. so 070s prose says "one group" and "the other group" instead of top and bottom. do not write positional references into prose about a mermaid block, github may lay it out differently than a local render.

## NOTES
