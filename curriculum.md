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
- [x] model selection: picking by task, not leaderboard (107)
- [x] CAPSTONE: the checklist i would run before shipping any llm feature (108)

## ARC 10 - agents: when output starts doing things
- [x] answer vs action: what changes when the output executes (109)
- [ ] the toolbox is a prompt: tool names and descriptions are instructions
- [ ] the schema clamp: json that cant come out wrong
- [ ] a shared socket for toolboxes: any agent, any toolbox
- [ ] a failed tool call goes back in: errors are context
- [ ] "no more tool calls" isnt done: the check lives outside the model
- [ ] what a loop costs: every round replays the whole history
- [ ] tool results eat the window: truncate or paginate
- [ ] when the run outlives the window: fold old rounds into a summary
- [ ] the plan is just tokens: files are the agents real memory
- [ ] sub-agents: a fresh window with a narrower job
- [ ] computer use: when the tool is the screen
- [ ] CAPSTONE: the working agent, assembled, every moving part named

## ARC 11 - agents you can trust
- [ ] read vs write: blast radius decides which calls need a gate
- [ ] injection grows hands: when poisoned text can act
- [ ] cap the tool, not the model: least privilege for agents
- [ ] the gate that doesnt drown you: approving the risky few, not everything
- [ ] a trace, not a log line: observability for a twenty step run
- [ ] grade the end state: did the thing actually happen
- [ ] count the steps: cost and length as a score
- [ ] an agent reviews an agent: the judge moves in front of the gate
- [ ] memory across runs: what it keeps, and whose data that is
- [ ] budgets and kill switches: caps per run, not per request
- [ ] when not an agent: if you know the steps, write the pipeline
- [ ] CAPSTONE: the trusted agent, assembled

## THREAD

baton: 109 opened arc 10 by reframing, not by adding mechanism. it put one reply next to another, the text field and the tool_calls field, same model and same 95%, and showed that the only thing that moved is whether a person sits between what the model said and it being true. it named my code as the thing that still calls run, and 082s loop as the default that never asks. 110 picks up from the tool_calls block being taken at face value: it must show where those tool names and descriptions come from, that the toolbox is written in english and goes into the prompt, so a bad description is a bad instruction rather than a bad config file. no gating and no permissions yet, arc 11 owns those and 109 deliberately left the door open by saying nothing forces me to call run.

for the record, what 109 established: the fork between an answer and an action lives in the shape of the reply, not in the model. a plain text block, not mermaid and not a table, holding one refund question resolved two ways, the chat bubble path costing a scroll when wrong and the issue_refund path costing a refund that already happened. it carried 104s bottom row forward as the subject of the whole arc, wired 051 into 082s loop, and its exit points forward at the toolbox.

the growth rules are unchanged inside the new arcs: splits for granularity, capstone gap check for at most one brick, strict order within an arc, capstone written last. one sanctioned exception to the no-names line: the socket note in arc 10 may name mcp once, translated in the same sentence it appears in, a published standard is not a vendor. everything else stays shapes over names.

process note on headers: every notes (n of m) was backfilled on 2026-08-30, splits had been growing arcs while old headers kept the size the arc had on their writing day. from now on any split or add that changes an arcs size also fixes the (n of m) in that arcs already-written notes, same run, committed with the split.

lines the repo has held and should keep holding: no named vendor and no named benchmark, arc 9 held that from 099 through 108 and 109 held it too, issue_refund and search_docs are made-up tool names in my own example. caches are laid and closed, arc 8 owns them and 098 owns their assembly. bm25 scoring is still an unlaid brick on purpose. arc 7 owns measurement.

process note: 104 at 233, 105 at 220, 106 at 198, 107 at 205, 108 at 314 under the 350 capstone ceiling, 109 at 214. the brick cluster stays loose and steady and only the capstone runs long, which is what the wider budget is for.

last visuals: plain text block, one question resolved into two reply shapes with the consequence of being wrong annotated under each (109), mermaid flowchart, ten nodes, two diamonds and a branch that rejoins, every label carrying its note number (108), table, three rows and three columns, public rank against my own score with the order inverting (107). mermaid is free again after this one, the streak is broken.
last exits: forward (109), stops (108), stops (107). one forward against two stops, so the next note may point forward, but the one after that should stop.

process note on visuals: mermaid stacks subgraphs in whatever order it likes and it flipped the two on 065, and on 070 it put the once-per-doc group beside the per-question one rather than above it. so 070s prose says "one group" and "the other group" instead of top and bottom, and 098 names its groups seconds, minutes and months for the same reason. do not write positional references into prose about a mermaid block, github may lay it out differently than a local render. 106 hit this while drafting, "that first fork" became "the fact question" so the prose names the node by its content instead of its place. 108 hit it twice, "the first fork" became "the rule question" and "every other question below" became "every other question here", both for the same reason. tables are safe for this, 099 says "top row" and "row two" and github renders rows in file order, and 104 leans on top two rows and bottom two rows the same way. plain text blocks are safe too, 102 labels each step in file order and github shows them that way, and 109 says top block and bottom block for the same reason. <br/> inside mermaid node labels renders fine, 103 proved it and 106 used it on all seven labels.

## NOTES
