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
- [x] when the loop goes wrong: runaway agents and hard stops (083)
- [x] streaming: why the ui types (084)
- [x] provider prompt caching: pay less for the part of the prompt that never changes (085)
- [x] semantic caching: the same question twice shouldnt cost twice (086)
- [x] latency and cost budgets: the two numbers that kill llm features (087)
- [x] rate limits: two meters, requests a minute and tokens a minute (088)
- [x] retrying a 429: wait, then double the wait (089)
- [x] jitter: when every client retries at the same moment (090)
- [x] which errors are worth retrying, and which never are (091)
- [x] the timeout you set yourself: how long to wait before you stop waiting (092)
- [x] fallback: a second model when the first one is down (093)
- [x] failing gracefully: what the user gets when every attempt is gone (094)
- [x] pinned or floating: the model id you send is either a date or a moving pointer (095)
- [x] deprecations: the version you pinned has an end date (096)
- [x] observability: logging llm calls like http calls (097)
- [x] CAPSTONE: what happens after deploy, keeping an llm feature alive (098)

## ARC 9 - the decisions: safety, privacy, and picking your model
- [x] should this even be an llm: when boring code wins (099)
- [x] content moderation: the filter in front of and behind the model (100)
- [x] what leaves your server: the personal data in a request nobody typed today (101)
- [x] redaction: swapping the sensitive parts out before the call, and what you cant swap (102)
- [ ] what the other side keeps: retention, training, and the logs that are yours
- [ ] designing for wrong: shipping a feature that fails 5% of the time, on purpose
- [ ] api models vs open weights: renting a model vs owning one
- [ ] which lever: prompt harder, add retrieval, or fine-tune
- [ ] model selection: picking by task, not leaderboard
- [ ] CAPSTONE: the checklist i would run before shipping any llm feature

## THREAD

baton: 102 took the card number back out of 101s request. the visual was a worked example, one sentence traced through five labeled steps, the typed question, the map my code keeps, the swapped sentence that leaves the server, the reply that comes back still carrying the labels, and the sentence the user reads after the map is walked backwards. the walk was that its a round trip and not a delete, the real values sit in a map on my server and the model only ever sees PERSON_1. the click is that the model doesnt need to know rahul is rahul, it needs something stable to point at, so the label is a variable name. the honest half is that swapping only survives when nothing has to look inside the value, so anything that gets compared or counted has to go as it is. it closed on 100s classifier wearing a different hat, miss a span and it ships anyway. exit just stopped.

next is "what the other side keeps: retention, training, and the logs that are yours". 101 named whats in the envelope and 102 took part of it out, so 103 is the last of the three and it asks what happens to the part that still leaves. the shape wants the two sides of one call, my logs (097 already made those a decision, dont re-teach the log line) and their logs, and the fact that a retention window and a used-for-training flag are two separate questions people fold into one. the honest half is that the answer is a contract setting and not a code change, so its the first thing in arc 9 you cannot fix in your own repo. do not re-open the audit (101) or the swap (102), and do not name a provider or compare policies, model selection later in this arc owns comparisons.

caches stay laid and closed, arc 8 owns all of them and 098 owns the assembly, dont let arc 9 reopen a mechanism. bm25 scoring is still an unlaid brick on purpose. the flag 097 planted is spent after 103, the last of the three checkboxes the original data-leaves-the-building box split into. 099 deliberately did not name any specific model or provider, and 101 and 102 held that line too.

process note: 096 at 206, 097 at 216, 098 at 324 as a capstone, 099 at 217, 100 at 216, 101 at 182, 102 at 206. 216 had shown up three times, so 102 got trimmed off it on purpose. 103 should sit under 200.

last visuals: worked example, one sentence traced through five labeled steps with a two-row map (102), annotated jsonc request array, four content blocks with one comment each (101), mermaid flowchart, seven nodes, two gates with a blocked branch off each (100). no type repeats yet, 103 is free, and a mermaid block would be the freshest of them.
last exits: stops (102), forward (101), stops (100). only one of the last three points forward, so 103 may do either.

process note on visuals: mermaid stacks subgraphs in whatever order it likes and it flipped the two on 065, and on 070 it put the once-per-doc group beside the per-question one rather than above it. so 070s prose says "one group" and "the other group" instead of top and bottom, and 098 names its groups seconds, minutes and months for the same reason. do not write positional references into prose about a mermaid block, github may lay it out differently than a local render. tables are safe for this, 099 says "top row" and "row two" and github renders rows in file order. plain text blocks are safe too, 102 labels each step in file order and github shows them that way.

## NOTES
