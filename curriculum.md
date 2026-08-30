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
- [x] the toolbox is a prompt: tool names and descriptions are instructions (110)
- [x] the schema clamp: json that cant come out wrong (111)
- [x] a shared socket for toolboxes: any agent, any toolbox (112)
- [x] a failed tool call goes back in: errors are context (113)
- [x] "no more tool calls" isnt done: the check lives outside the model (114)
- [x] what a loop costs: every round replays the whole history (115)
- [x] tool results eat the window: truncate or paginate (116)
- [x] when the run outlives the window: fold old rounds into a summary (117)
- [x] the plan is just tokens: files are the agents real memory (118)
- [x] sub-agents: a fresh window with a narrower job (119)
- [x] computer use: when the tool is the screen (120)
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

baton: 120 established that computer use makes the tool a screen, so the tool result is a screenshot going into the array the way 054 puts in any image, and the tool call is a coordinate, click 412, 290. it kept the loop identical to 082 and changed only what the observe step is made of. it named the fragility plainly, theres no dom and no test id, the model finds the button by looking at pixels and hands back two numbers, so a banner that pushes the page down 40 pixels sends the click somewhere else and you learn that from the next screenshot rather than from an error. it said why anyone takes that deal, some systems have no api and the screen is the only interface there is. it handed blast radius off to arc 11 in its last line rather than opening it. the next checkbox is the arc 10 capstone, and it is assembly only: every brick from 109 through 120 as a labelled part of one working agent, each label carrying its note number, up to 350 words. run the capstone gap check first.

for the record, what 120 established: a mermaid sequence diagram, three participants, model and my code and the screen, six messages running screenshot plus goal in, click 412, 290 out, the real click, a fresh screenshot back, that screenshot in again and then type "invoice", with a note reading one action per round. numbers are 412, 290 and a 40 pixel shift, both arbitrary positions rather than costs. it named 119, 109, 054 and 082. its real world detail is grabbing a button by its test id in my react work. it ended by handing blast radius to arc 11, so it points forward.

previously, what 119 established: a plain text worked example, two labelled scenarios, inline in the parents own window with three calls at 3,200, 2,900 and 4,100 tokens accumulating to 10,200 of raw hits, against the same job handed to research_agent, its own fresh array holding the same 3 calls and the same 10,200 tokens and going away when it returns, with one ~15 token sentence coming back and the parent array growing by one line. rounds 4 to 6. it named 118, 116, 115 and 082. its real world detail is handing a ticket to someone without replaying every standup. it just stopped, no forward pointer.

previously, what 118 established: a mermaid flowchart, seven nodes, one plan of 800 tokens forking into left in the array and written to plan.md, the array branch running to resent every round and then the fold can rewrite it, the file branch running to array keeps the filename and then read back word for word. numbers are 800 tokens for the plan, written on round 3, ten more rounds of replay at 8,000 tokens, six steps, read back on round 14. it named 115 for the replay bill and 117 for the fold. its real world detail is a grocery list that drifts in my head and doesnt on paper. it ended pointing forward at 119 in one short clause.

so as of 120 the arc has a described toolbox, a place to fetch it from, a loop that recovers from a failed call, a done check that does not ask the model, an itemized bill for one round, a rule for how much of a tool result gets in, a way for the run to survive outgrowing the window, somewhere durable to put what must not be summarised away, a way to run a whole job in a window this one never sees, and a tool that is a screen when there is no api. still no check anywhere on whether a call should happen, arc 11 owns that.

overlap to keep an eye on for the capstone: it is assembly, so its job is linking, not teaching. every one of 109 through 120 gets named by number as a part of one picture, and nothing new gets introduced. the four context notes 115 through 118 plus 119 collapse into one part of that picture, dont re-litigate them one by one. do not reuse a worked number from any brick for a different point, 115 owns 2,974 and 2,600, 116 owns 47 and 4, 117 owns 29,700 and 240, 118 owns 800 and 8,000, 119 owns 10,200 and ~15, 120 owns 412, 290. the capstone must end where arc 11 begins, on the fact that nothing in this arc ever asked whether a call should happen, and it should say that once rather than previewing arc 11s notes.

overlap to keep an eye on: 050 already appends a broken reply plus an error string and retries, for the models own malformed json. 113 is the same move aimed at a tool that failed, inside the agent loop. if a later note in this arc goes near retries again, name the difference explicitly. second one, arc 11 has "grade the end state, did the thing actually happen". 114 deliberately stayed on the runtime return path, the check my code runs before the loop hands anything back. arc 11s note is measurement after the fact, scoring a finished run the way arc 7 scores an answer. when that note gets written, open it on that difference. third one, 119 said the sub-agent comes back with a sentence you cant audit, and arc 11 has "a trace, not a log line". that note owns the fix, 119 only names the problem.

the growth rules are unchanged inside the new arcs: splits for granularity, capstone gap check for at most one brick, strict order within an arc, capstone written last.

process note on headers: every notes (n of m) was backfilled on 2026-08-30, splits had been growing arcs while old headers kept the size the arc had on their writing day. from now on any split or add that changes an arcs size also fixes the (n of m) in that arcs already-written notes, same run, committed with the split.

lines the repo has held and should keep holding: no named vendor and no named benchmark, arc 9 held that from 099 through 108 and arc 10 has held it too, issue_refund, search_docs, get_order_by_id and list_recent_orders are made-up tool names in my own examples. caches are laid and closed, arc 8 owns them and 098 owns their assembly. bm25 scoring is still an unlaid brick on purpose. arc 7 owns measurement. 058 owns how big a chunk is, thats a different knob from how many chunks reach the model and 116 stayed off it.

process note: 108 at 314 under the 350 capstone ceiling, 109 at 214, 110 at 232, 111 at 193, 112 at 222, 113 at 189, 114 at 198, 115 at 190, 116 at 187, 117 at 197, 118 at 207, 119 at 203, 120 at 205. 120 drafted at 213 and came down by cutting one item from the no-api list and three small phrases, the dom caveat untouched. the capstone gets the 350 ceiling but 108 landed at 314 and read fine, so aim there rather than at the ceiling.

last visuals: mermaid sequence diagram, model and my code and the screen, a screenshot in and a coordinate out over six messages (120), plain text worked example, two labelled scenarios, three calls totting up to 10,200 tokens in the parents window against the same job returning one sentence from a sub-agent (119), mermaid flowchart, one plan forking into the array branch and the file branch, seven nodes (118). two mermaid blocks in the last three, and the capstone wants an assembly diagram anyway, so if it goes mermaid make it a labelled parts picture rather than another sequence.
last exits: forward (120), stops (119), forward (118). two of the last three point forward, so the capstone stops, which suits a capstone closing an arc.

process note on visuals: mermaid stacks subgraphs in whatever order it likes and it flipped the two on 065, and on 070 it put the once-per-doc group beside the per-question one rather than above it. so 070s prose says "one group" and "the other group" instead of top and bottom, and 098 names its groups seconds, minutes and months for the same reason. do not write positional references into prose about a mermaid block, github may lay it out differently than a local render. 106 hit this while drafting, "that first fork" became "the fact question" so the prose names the node by its content instead of its place. 108 hit it twice, "the first fork" became "the rule question" and "every other question below" became "every other question here", both for the same reason. tables are safe for this, 099 says "top row" and "row two" and github renders rows in file order, and 104 leans on top two rows and bottom two rows the same way. plain text blocks are safe too, 102 labels each step in file order and github shows them that way, 109 says top block and bottom block for the same reason, and 113 leans its whole payoff on "line 3" of a numbered block. code blocks are safe the same way, 116 says the truncate branch and the paginate branch by their labels anyway. sequence diagrams are safer than flowcharts here, 112 rendered with its participants in declaration order, but its prose still names the actors instead of saying left or right. 118 is a two branch flowchart and dodged the whole problem by naming its branches from their content, leave it as a message and write it to plan.md instead, so it reads correctly whichever side github puts them on. mmdc runs in this container only with a puppeteer config passing --no-sandbox, without it the render dies on a root sandbox error that has nothing to do with the diagram.

## NOTES
