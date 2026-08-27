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
- [ ] temperature
- [ ] greedy vs sampling, top-p
- [ ] why models make things up, and why its not a bug you can patch
- [ ] asking the model how sure it is, and why you cant trust the answer
- [ ] stop sequences and max tokens
- [ ] determinism: why the same prompt varies and what that breaks
- [ ] reasoning models: when the model thinks first, and what those tokens cost
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
baton: 032 opened arc 4 by taking the one line 022 and 031 both ended on, the model hands back a score per token and the picking happens after, and showing what those raw scores actually are. named them logits, unbounded numbers where the only meaning is which is bigger, some of them negative. then the two steps that make them usable, Math.exp on every row (fixes the sign, keeps the order, stretches the gaps) and divide each by the total (now they add to 100%). worked it on four rows, 3.2 / 2.1 / 1.0 / -0.4 becoming 68.0 / 22.6 / 7.5 / 1.9 percent. named the pair softmax. the line the next note has to pick up is the gap stretching: 1.1 points of raw score turned into a 3x difference in probability, and the note ends saying theres a knob that squeezes or stretches those gaps before the exp step even runs. that knob is temperature, the next checkbox, and it is deliberately unexplained so far, only pointed at. temperature divides every logit before softmax, so 032s worked example is the exact table it should reuse and re-run. what 032 explicitly did NOT do is pick a token, we still have 100,000 percentages and no choice made, which is what greedy vs sampling and top-p pick up after temperature. 032 points forward, so 033 may too but the note after it must just stop.
last visuals: worked example (032), mermaid (031), worked example (030)
last exits: forward (032), stops (031), forward (030)

## NOTES
