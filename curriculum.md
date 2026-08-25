# curriculum

arc map for ai-notes. checkboxes track progress. never reorder a concept behind
one that depends on it.

## ARC 1 — how machines read text

- [x] characters vs words, and why both fail (001)
- [ ] what a token is
- [ ] BPE: merging by frequency
- [ ] tokens are money: how pricing actually works
- [ ] context window
- [ ] why tokenization causes weird failures
- [ ] CAPSTONE: what the model sees, and what it costs, when i send a request

## ARC 2 — meaning as numbers

- [ ] a vector is a list of numbers
- [ ] dot product, by hand
- [ ] cosine similarity
- [ ] what an embedding is
- [ ] nearby means similar
- [ ] one word, many meanings: context changes the vector
- [ ] embedding models are separate products from chat models
- [ ] CAPSTONE: how "search by meaning" works end to end

## ARC 3 — whats inside the box

- [ ] next-token prediction is the whole game
- [ ] attention in one note: every token looks at every other token — the superpower and the cost
- [ ] why compute scales badly with input length
- [ ] training vs inference: baked-in knowledge has a cutoff
- [ ] base model vs assistant: what tuning changed
- [ ] what fine-tuning can fix and what it cant
- [ ] CAPSTONE: the box, closed — everything an applied engineer must know about internals and nothing more

## ARC 4 — how it writes, and the knobs you own

- [ ] logits to probabilities
- [ ] temperature
- [ ] greedy vs sampling, top-p
- [ ] why models make things up — and why its not a bug you can patch
- [ ] stop sequences and max tokens
- [ ] determinism: why the same prompt varies and what that breaks
- [ ] reasoning models: when the model thinks first, and what those tokens cost
- [ ] CAPSTONE: one tokens journey out, and every knob you control

## ARC 5 — the prompt is the program

- [ ] system vs user messages: who outranks whom
- [ ] conversation state: the model remembers nothing — your code fakes the memory
- [ ] few-shot: showing beats telling
- [ ] structured output: getting json you can actually parse
- [ ] when json breaks: validation and retry
- [ ] tool calling: the model asks, your code acts
- [ ] prompt injection: user input IS code now
- [ ] context budget: what to include when you cant include everything
- [ ] CAPSTONE: anatomy of a production prompt

## ARC 6 — RAG: giving the model your data

- [ ] closed-book vs open-book
- [ ] long context vs retrieval: when you can just send everything, and when you cant
- [ ] chunking: the decision that quietly decides quality
- [ ] retrieval: embed, search, stuff the context
- [ ] why retrieval fails: the vocabulary gap
- [ ] keyword + semantic: hybrid search
- [ ] reranking: cheap search, expensive sort
- [ ] measuring retrieval: recall@k and mrr in plain terms
- [ ] groundedness: did the answer come from the docs
- [ ] CAPSTONE: doc-QA system end to end, every design decision named

## ARC 7 — evals: how you know any of it works

- [ ] "looks good" doesnt scale
- [ ] the golden dataset: 50 examples beat vibes
- [ ] exact match vs semantic scoring
- [ ] llm-as-judge, and its biases
- [ ] regression: the prompt change that broke three other things
- [ ] evals in ci: treating prompts like code
- [ ] CAPSTONE: an eval harness for the arc 6 system

## ARC 8 — agents, cost, and production reality

- [ ] an agent is a while loop with an llm inside
- [ ] when the loop goes wrong: runaway agents and hard stops
- [ ] streaming: why the ui types
- [ ] provider prompt caching: pay less for the part of the prompt that never changes
- [ ] semantic caching: the same question twice shouldnt cost twice
- [ ] latency and cost budgets: the two numbers that kill llm features
- [ ] rate limits and retries
- [ ] observability: logging llm calls like http calls
- [ ] content moderation: the filter in front of and behind the model
- [ ] images in: multimodal requests without the mystery
- [ ] model selection: picking by task, not leaderboard
- [ ] CAPSTONE: the checklist i would run before shipping any llm feature

## THREAD

baton: note 001 showed why splitting text into whole words (infinite
vocabulary, unseen words break it) or single characters (sequences balloon,
units carry no meaning alone) both fail. note 002 picks up from "the fix
splits the difference" — introduce what a token actually is, as a middle
ground between a character and a word.
last visuals: table (001)

## NOTES

