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
- [ ] clustering: finding the groups when nothing is labeled
- [ ] CAPSTONE: how search by meaning works end to end

## ARC 3 - whats inside the box (enough to not be fooled, no more)
- [ ] next-token prediction is the whole game
- [ ] attention in one note: every token looks at every other token, the superpower and the cost
- [ ] why compute scales badly with input length
- [ ] model size: what 8B parameters means, and what bigger actually buys
- [ ] training vs inference: baked-in knowledge has a cutoff
- [ ] base model vs assistant: what tuning changed
- [ ] what fine-tuning can fix and what it cant
- [ ] CAPSTONE: the box, closed. everything an applied engineer must know about internals and nothing more

## ARC 4 - how it writes, and the knobs you own
- [ ] logits to probabilities
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
baton: 019 spent the escape hatch. with only two strings and no labels to rank against, the cosine has to stand alone, so you commit to one absolute number. 019 established how you get that number, by hand: score thirty pairs you already know the answer for, sort them, and put the line where the two groups roughly separate. it also established that they never fully separate, so every line you pick both merges things that arent dupes and misses things that are, and moving it only swaps which mistake you make. the threshold belongs to one model, swap the embedding model and you redo it. what 020 must pick up is the step where even those hand labels are gone. clustering has no known-dupe pairs to calibrate against and no label sentences either, just a pile of arrays, so the groups have to fall out of the scores themselves. dont re-explain cosine, embed(), the endpoint, what the arrays are, or that absolute scores drift by model.
last visuals: worked example (019), worked example (018), annotated artifact (017)
last exits: forward (019), stops (018), stops (017)

## NOTES
