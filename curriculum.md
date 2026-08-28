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
- [ ] hybrid: merging two ranked lists when the scores dont compare
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
baton: 063 put the second search on the table. keyword search, a hashmap from each word to the chunks holding it, the thing you already built with a LIKE query behind a search box. the comparison table ran two questions at 062s expenses.md, "how long do i have to claim a work lunch back" which shares literally zero tokens with the doc and which meaning-search still ranks first, and "whats the Nova deadline" which the literal match takes in one lookup while the embedding drifts to whatever else says deadline. each column wins one row and whiffs the other, and that diagonal is the whole note. the one caveat carried: real keyword search is not grep, it weights rare words heavier than common ones, which is why an invented name like Nova is such a loud signal.

063 also corrected the plan the last baton had set. hybrid does NOT rescue 062s exact question, there you typed money back and the doc said reimbursement, so the literal list has even less to grab than the embedding did. do not let the next note claim otherwise. 063 ends on two rankings and neither one being the good list.

the next checkbox is "hybrid: merging two ranked lists when the scores dont compare". it exists because the merge is genuinely not obvious and that is the note: a cosine score and a keyword score are not on the same scale, so you cannot add them. the move is to throw the scores away and merge on rank position instead, one over the rank, summed across the two lists, which is why a chunk that placed decently in both beats one that won a single list. keep bm25 scoring out of it, that stays a missing brick and gets split if it wants a paragraph.

process note: 060 landed at 207, 061 at 190, 062 at 181, 063 at 217. the aim is 170 to 190 and 063 broke it, on purpose, to carry both the caveat and the correction to 062. next one comes back under 190.

last visuals: comparison table, two questions by two search methods against one doc (063), annotated artifact, two doc excerpts marked for word overlap and rank (062), worked example, six scored chunks run through both filter orders (061). the merge is a numbers job, so 064 wants a worked example with the two rank columns and the sum on the page, and that is fine by the no-three-in-a-row rule since the last worked example was 061. it does mean four text-shaped visuals running, so 065 owes this arc a mermaid.
last exits: forward (063), stops (062), forward (061). a forward at 064 is still legal, two running is the ceiling, so if 064 points ahead then 065 has to just stop.

## NOTES
