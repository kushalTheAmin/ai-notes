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
- [ ] the request is a list of role-tagged messages, and it all becomes one token stream
- [ ] system vs user: what outranking buys you, and what it doesnt
- [ ] conversation state: the model remembers nothing, your code fakes the memory
- [ ] few-shot: showing beats telling
- [ ] structured output: getting json you can actually parse
- [ ] when json breaks: validation and retry
- [ ] tool calling: the model asks, your code acts
- [ ] prompt injection: user input IS code now
- [ ] context budget: what to include when you cant include everything
- [ ] images in: multimodal requests without the mystery
- [ ] CAPSTONE: anatomy of a production prompt

## ARC 6 - RAG: giving the model your data
- [ ] closed-book vs open-book
- [ ] long context vs retrieval: when you can just send everything, and when you cant
- [ ] chunking: the decision that quietly decides quality
- [ ] retrieval: embed, search, stuff the context
- [ ] where vectors live: from scanning every doc to a real index, and what approximate costs
- [ ] filtering before searching: metadata, permissions, and why vector search alone isnt enough
- [ ] why retrieval fails: the vocabulary gap
- [ ] keyword + semantic: hybrid search
- [ ] reranking: cheap search, expensive sort
- [ ] measuring retrieval: recall@k and mrr in plain terms
- [ ] groundedness: did the answer come from the docs
- [ ] CAPSTONE: doc-QA system end to end, every design decision named

## ARC 7 - evals: how you know any of it works
- [ ] "looks good" doesnt scale
- [ ] the golden dataset: 50 examples beat vibes
- [ ] exact match vs semantic scoring
- [ ] llm-as-judge, and its biases
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
baton: 044 closed arc 4. it established the knobs as an ordered pipeline over one list of scores, temperature divide first (033), then exp and divide into percentages (032), then the k cut (035), then the p cut (036), then rescale, then take the top row or roll (034), then glue on and check the stop (040). it landed on the arc framing, no knob in that path can add a row that wasnt already on the list (037), nothing in it asks whether the winner is true (038), and the winners percentage moves when you set k so it isnt a gauge (039). the last line handed the problem upward, if none of these knobs fixes a wrong answer then the only thing left to change is what you send in, and named arc 5 as where that goes.

the next checkbox is the first brick of arc 5, "system vs user messages: who outranks whom". per the arc-opener rule it builds on 044, the arc 4 capstone, and the baton it must pick up is that last line, the lever moved from the sampling knobs to the text you send. arc 5 is called "the prompt is the program" so this first note should quietly establish that the thing you send is not one string, its a list of role tagged messages, and then do the one atomic job on the checkbox, what system outranking user actually means and what it does not mean. careful on that second half, the honest version is that role separation is trained behaviour and not enforcement, a strong instruction in a user message can still win, so the caveat belongs in the note rather than being saved for the prompt injection checkbox later in the arc. do not spend the note on injection itself, that brick is already on the list. the split test is worth running before drafting, "what the roles are" and "what outranking really buys you" might be two notes.

process note: 044 came in at 308 prose words against a 350 capstone ceiling. arc 5s bricks are back on the 120 to 250 budget, and after two runs in the 140 to 190 band it would be good to land there again.

last visuals: mermaid diagram (044), annotated artifact (043), mermaid diagram (042). mermaid has now run twice in three notes, so 045 must not be mermaid. an annotated artifact fits the roles note naturally, a real messages array dissected, though that would be an artifact twice in three too. a small comparison table or a worked example would break the run cleanly.
last exits: forward (044), stops (043), forward (042). two of the last three point forward, so 045 must just stop.

## NOTES
