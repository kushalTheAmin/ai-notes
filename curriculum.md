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
- [ ] the score moved, is it real: why small eval sets lie
- [ ] regression: the prompt change that broke three other things
- [ ] evals in ci: treating prompts like code
- [ ] error analysis: stop guessing, read the failures and bucket them
- [ ] after you ship: thumbs, feedback, and checking quality in the wild
- [ ] CAPSTONE: an eval harness for the arc 6 system

## ARC 8 - running it: speed, cost, and when things break
- [ ] an agent is a while loop with an llm inside
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
baton: 075 finished the pair that 074 was split out of. it took the judge call 074 built and showed the verdict moving for reasons that have nothing to do with the answer being right. the setup it chose matters for what comes next: some golden rows have no must_say (an open question like "explain the refund policy"), so the rubric goes soft, "is this a good answer?", and thats the condition all three tilts need. the table is one answer four ways, fail when terse, pass when padded with two sentences of policy talk, pass when phrased the way the model itself writes, and 48 of 50 passing on that same soft rubric. it carries the caveat that a concrete must_say doesnt delete the tilt, it just leaves less room for taste. it lands on the rubric being the fix, which is 072 doing the work again, and it ends there rather than pointing forward.

the next checkbox is "the score moved, is it real: why small eval sets lie", and 075 handed it a live thread. 075s last table row is a score that stopped discriminating because everything passes. the next note is the other reason a score lies, the set is small so the number wobbles on its own. this is where the fifty from 072 finally gets examined, it was deliberately left alone through 072 to 075 and it is now this notes to spend. the shape to aim for: one prompt change, the score moves a few points, and the same move is what you would get from flipping two or three rows by chance. keep it countable, whole answers out of 50, no standard deviation and no significance vocabulary, both of those are notation the reader closes the tab on. if the draft wants confidence intervals, thats the split rule firing.

do not introduce pairwise A/B judging anywhere in this arc, that mode was never built here and propping it up mid-note costs a paragraph the budget doesnt have.

bm25 scoring stayed a missing brick through all of arc 6 and that was correct. 064 prints a keyword score as a bare number on purpose, since the point is that the scale is unknowable to you. it stays unlaid, dont let a later arc drag it in.

process note: 069 at 154, 070 at 324 on the capstone ceiling, 071 at 190, 072 at 221, 073 at 191, 074 at 202, 075 at 218. the band called for 075 was 170 to 230 and it landed inside without cutting a tilt, because the soft rubric framing let two of the three ride in the table instead of costing a paragraph each. 076 is a numbers note, so the visual will eat the budget, 150 to 200 is the band and the prose should mostly point at the table.

last visuals: comparison table, one answer four ways against a soft rubric with the verdicts beside it (075), pseudocode, the grade call filled in with a real golden row plus the two verdicts that come back (074), comparison table, four answers scored two ways against one question (073). the table has now run twice in three notes, so 076 must not be a comparison table, that would be the three in a row rule. a worked example with real counts, two runs over the same 50 rows with the rows that flipped listed out, fits the concept better anyway.
last exits: stops (075), forward (074), stops (073). two of the last three stop, so 076 is free either way, and a forward pointer into "regression" is natural if it fits without a teaser formula.

process note on visuals: mermaid stacks subgraphs in whatever order it likes and it flipped the two on 065, and on 070 it put the once-per-doc group beside the per-question one rather than above it. so 070s prose says "one group" and "the other group" instead of top and bottom. do not write positional references into prose about a mermaid block, github may lay it out differently than a local render.

## NOTES
