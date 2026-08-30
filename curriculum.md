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
- [x] what the other side keeps: retention, training, and the logs that are yours (103)
- [x] designing for wrong: shipping a feature that fails 5% of the time, on purpose (104)
- [x] api models vs open weights: renting a model vs owning one (105)
- [x] which lever: prompt harder, add retrieval, or fine-tune (106)
- [ ] model selection: picking by task, not leaderboard
- [ ] CAPSTONE: the checklist i would run before shipping any llm feature

## THREAD

baton: 106 laid the which-lever brick. the visual was a mermaid decision tree, eight nodes, one entry into three diamonds in a chain, each yes-branch dropping to a lever labelled with what it costs, retrieval at days, prompting at an afternoon, fine-tune at weeks and a dataset, and the last no-branch going to read the failures first (079). the walk was that these are not one knob at three strengths, the fact question decides everything, since rewording cant add a fact (056) and 030 said tuning teaches shape and tone not facts, so retrieval is the only one of the three that adds knowledge. the honest turn was that fine-tuning sounds like the real engineering and is the one to reach for last, earning its cost only when the model already knows enough and keeps breaking the same way. it closed on the levers stacking rather than replacing each other. exit points forward at 107.

next is "model selection: picking by task, not leaderboard". 106 ended on choosing a move, so 107 picks up the same decision one step over, you have decided to prompt or retrieve, now which model runs it. 087 already owns latency and cost as the two numbers, 027 owns what a bigger model buys and what it doesnt, 072 and 076 own the golden set and why small eval sets lie, so the note is about picking on your own task instead of a public ranking, and it must not re-teach any of those. 105 owns rent versus own and 106 owns the three levers, dont reopen either. still no named vendor and no named benchmark, the arc has held that line since 099 and 107 is the note most tempted to break it, keep it to shapes.

caches stay laid and closed, arc 8 owns all of them and 098 owns the assembly, dont let arc 9 reopen a mechanism. bm25 scoring is still an unlaid brick on purpose. arc 7 owns measurement, 106 pointed at 079 in one clause and that is the right amount, 107 will need 072 the same way, one clause not a paragraph. the arc capstone after 107 is the pre-ship checklist and it assembles 099 through 107, so leave the assembly work to it.

process note: 100 at 216, 101 at 182, 102 at 206, 103 at 193, 104 at 233, 105 at 220, 106 at 198. 106 landed in the short band as planned. 107 can sit anywhere from 180 to 230, the cluster is looser now.

last visuals: mermaid flowchart, eight nodes, three diamonds chained down with a cost label on every lever (106), plain text bill, the same day costed twice with three traffic rows each and a crossover line (105), table, four rows and three columns, same model down every row with the landing place changing (104). 107 may not be a mermaid diagram. a table would work well for a per-task comparison, and so would an annotated artifact.
last exits: forward (106), stops (105), forward (104). only one of the last three stops, so 107 must stop, no forward pointer.

process note on visuals: mermaid stacks subgraphs in whatever order it likes and it flipped the two on 065, and on 070 it put the once-per-doc group beside the per-question one rather than above it. so 070s prose says "one group" and "the other group" instead of top and bottom, and 098 names its groups seconds, minutes and months for the same reason. do not write positional references into prose about a mermaid block, github may lay it out differently than a local render. 106 hit this while drafting, "that first fork" became "the fact question" so the prose names the node by its content instead of its place. tables are safe for this, 099 says "top row" and "row two" and github renders rows in file order, and 104 leans on top two rows and bottom two rows the same way. plain text blocks are safe too, 102 labels each step in file order and github shows them that way. <br/> inside mermaid node labels renders fine, 103 proved it and 106 used it on all seven labels.

## NOTES
