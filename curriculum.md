# curriculum

## ARC 1 - how machines read text
- [x] characters vs words, and why both fail (001)
- [x] what a token is (002)
- [x] BPE: merging by frequency (003)
- [x] tokens are money: how pricing actually works (004)
- [x] why hindi and gujarati cost more than english: tokens per word isnt equal (005)
- [x] context window (006)
- [x] the model cant see inside a token: why it cant count letters (007)
- [ ] numbers get chunked, not counted: why arithmetic gets shaky
- [ ] a space or a capital letter changes the ids
- [ ] CAPSTONE: what the model sees, and what it costs, when i send a request

## ARC 2 - meaning as numbers
- [ ] a vector is a list of numbers
- [ ] dot product, by hand
- [ ] cosine similarity
- [ ] what an embedding is
- [ ] nearby means similar
- [ ] one word, many meanings: context changes the vector
- [ ] embedding models are separate products from chat models
- [ ] embeddings arent just for search: classify, cluster, dedup with the same vectors
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
baton: 007 established that a token is opaque. the model receives ids with no letters inside them, so anything letter level, counting, spelling, reversing, is recall from training rather than inspection, and the fix is to do that work in code. it used real ids from a real tokenizer to show the letters vanishing. 008 takes the same opacity and points it at digits: a number is cut into chunks by the same frequency rules from 003, and those chunk boundaries have nothing to do with place value, which is where arithmetic starts to wobble. it must not re-explain that ids hide their contents, 007 did that, it only has to show what changes when the contents are digits.
last visuals: worked example (007), worked example (006), comparison table (005)
last exits: stops (007), stops (006), forward (005)

## NOTES
