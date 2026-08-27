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
- [ ] CAPSTONE: one tokens journey out, and every knob you control

## ARC 5 - the prompt is the program
- [ ] system vs user messages: who outranks whom
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
baton: 042 and 043 were the two halves of the split reasoning checkbox, the mechanism then the money, and both are now written. that closes every brick in arc 4. the only thing left in the arc is its capstone.

043 opened on 042s last line, the model talking to itself on the page, and turned it into one sentence, every word of that talking is an output token. the visual was an annotated artifact, a request and response pair with max_tokens 2000 up top annotated as room for thinking AND answer, then a usage block with input_tokens 40 and output_tokens 1200 annotated as 1100 of these were thinking, then the cost split at 004s $15 per million rate, reply 100 tokens $0.0015, thinking 1100 tokens $0.0165, billed 1200 tokens $0.0180. the click is that eleven of every twelve tokens on that bill is text i never read. the caveat that keeps it honest is that readability is a provider thing, some hand back the full thinking, some a summary, some nothing, and the rate does not change. the second beat was the 040 collision, max_tokens counts the thinking too, so a 500 ceiling set for a short answer can get eaten entirely and come back cut off or empty with the flag reading max_tokens, billed for all 500. latency was left out on purpose even though 026 would have carried it, two beats was already the whole budget.

the next checkbox is the arc 4 capstone, "one tokens journey out, and every knob you control". its job is assembly, one picture where a single token leaves the model and passes every brick in the arc, each part labelled with its note number. the raw scores and the two steps that make them percentages (032), the divide (033), greedy or a roll (034), the k cut (035), the p cut (036), and then the loop deciding to keep going or stop (040) with the ceiling (040) sitting over the whole thing. the framing that has been running all arc is that not one of these knobs can add a row for "i dont know" (037) or check whether the winner is true (038), they only change which existing row wins, so the capstone should land there rather than on a knob checklist. 041 and 042 and 043 sit slightly outside the single token path, they are about what the loop does across many tokens, so give them a place in the picture but do not force them into the token pipeline. CAPSTONE GAP CHECK before drafting, every brick 032 to 043 is written so the assembly should hold without adding one.

process note: 178 prose words, second run inside the 140 to 190 band. it got there by refusing the latency sentence, not by trimming. the capstone gets up to 350 so that pressure lifts, but the ceiling is not a target.

last visuals: annotated artifact (043), mermaid diagram (042), worked example (041). the capstone needs an assembly diagram by definition, which means mermaid again two notes after 042. that is allowed, the rule is never the same type three running, but keep it visibly different from 042s fork, a pipeline with labelled parts rather than two branches.
last exits: stops (043), forward (042), forward (041). the last one stopped, so the capstone may point forward, and pointing at arc 5 is the natural close for it.

## NOTES
