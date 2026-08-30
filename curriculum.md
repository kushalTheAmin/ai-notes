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
- [x] CAPSTONE: the working agent, assembled, every moving part named (121)

## ARC 11 - agents you can trust
- [x] read vs write: blast radius decides which calls need a gate (122)
- [x] injection grows hands: when poisoned text can act (123)
- [x] cap the tool, not the model: least privilege for agents (124)
- [x] the gate that doesnt drown you: approving the risky few, not everything (125)
- [ ] a trace, not a log line: observability for a twenty step run
- [ ] grade the end state: did the thing actually happen
- [ ] count the steps: cost and length as a score
- [ ] an agent reviews an agent: the judge moves in front of the gate
- [ ] memory across runs: what it keeps, and whose data that is
- [ ] budgets and kill switches: caps per run, not per request
- [ ] when not an agent: if you know the steps, write the pipeline
- [ ] CAPSTONE: the trusted agent, assembled

## THREAD

baton: 125 took the leftovers from 124 and gave them to a person. its flowchart runs a proposed call past two questions before anybody is interrupted, can a rule decide it, which sends it to 124s in code check, then can i take it back, which lets the reversible ones run, so only the calls that are both undoable and not settleable in advance pause the loop. the denial path returns a tool result rather than killing the run, so 113 still holds. the point it lands is that a gate firing on everything is a rubber stamp with extra latency, so every question you can turn into a rule is a question nobody has to answer. the next checkbox is a trace, not a log line, observability for a twenty step run. it should pick up that 125 left a run full of decisions, auto ran, refused in code, approved, denied, with nothing recording which was which, and per the overlap list below it owns the run level view, 097 already owns the fields of one call, and 119 already named the unauditable sub-agent sentence this fixes.

for the record, what 125 established: a mermaid flowchart, eight nodes, a proposed call through the rule question and the take it back question, with a pause node splitting into approved and denied. no arithmetic anywhere in it, no tool names either, it works off 122s table by reference rather than restating the rows. its prose never points at the diagram by position, it doesnt name the forks at all, it walks the policy in words instead. its honest reaction is having had it backwards, assuming approval was the main safety feature and the code checks were tidying up around it. it has no invented personal event in it, the dialog you stop reading is written at the reader. it stops.

previously, what 124 established: a 13 line pseudocode block, two versions of email_customer, wide with a free text body and the rule sitting in a comment quoting the system message, capped with a customer id check against the current order and a template id checked against a list of three. no arithmetic in it, the only number is order 88120 reused from 052 and 123. it names 111 explicitly to stay off its ground, 111 clamps the shape at the pick and stopped on a well formed id thats the wrong customer, 124s check is the thing that catches that because it knows which order the run is about. it also names 113, both refusals return strings so the model reads the error next round. its real world detail is a deploy key scoped to one bucket, and its honest reaction is taking a minute to see the model as just another caller getting an account. it stops.

previously, what 123 established: a plain text annotated artifact in two halves, the tool result my code appended after a search_docs call with a poisoned html comment inside a wiki page, and the tool call the model writes on the same round, each with a caret annotation under it. the injected line aims at email_customer with a link, deliberately, because 122 put email_customer in the cant take it back column while issue_refund is the reversible one. it reuses order 88120 from 052 and the tool names search_docs, list_recent_orders and email_customer. no arithmetic in it. its honest reaction is realising 052 already carried the fix and i had filed it as chat app advice. it points forward, it names the next two notes without previewing their content.

previously, what 122 established: it opened arc 11 by picking up 121s closing line, go find the line in your agent that says no, and answering the smaller question underneath it, which calls even need one. it laid blast radius as a term, how far a wrong call reaches past my own code and how much of it sticks, and it corrected read vs write as the wrong axis. the visual was a four row three column comparison table, the call, what a wrong one leaves behind, can i take it back. it stops.

so arc 10 is closed and arc 11 is four bricks in. the repo now has an agent that can be described to, called, recovered when a call fails, stopped when it thinks its finished and isnt, and kept inside its window by four different moves plus delegation, and as of 122 a way to rank its own tools by what a wrong call costs, as of 123 a reason that ranking is urgent, as of 124 the first thing that acts on it, tools written narrow, and as of 125 a person standing behind the few calls the code cant settle. what it still has nowhere is a trace, a score for a finished run, or a budget. those are the next checkboxes and they should be written as if the table in 122, the poisoned wiki page in 123, the two versions of email_customer in 124 and 125s two filters are all already on the readers desk.

overlap to keep an eye on for arc 11: 050 already appends a broken reply plus an error string and retries, for the models own malformed json, and 113 is the same move aimed at a tool that failed. if a note goes near retries again, name the difference explicitly. second one, arc 11 has "grade the end state, did the thing actually happen", and 114 deliberately stayed on the runtime return path, the check my code runs before the loop hands anything back. arc 11s note is measurement after the fact, scoring a finished run the way arc 7 scores an answer, so open it on that difference. third one, 119 said the sub-agent comes back with a sentence you cant audit, and arc 11s "a trace, not a log line" owns the fix, 119 only named the problem. fourth one, 097 already itemized what a log line for one model call needs, so the trace note is about a run of twenty calls rather than about logging fields. fifth one, that pairing is spent, 123 wrote it. 052 owns injection where the damage is what the model says and 123 owns it where the damage is what my code does, so no later note in this arc re-explains the attack, they use it flat. 123 also already said the fix is keeping the dangerous thing out of reach of a followed instruction, so checkboxes 3 and 4 supply the two halves of that rather than announcing the idea. sixth one, 122 owns blast radius and owns the read vs write correction, so no later note in this arc redefines either, they use the term flat. 122 also deliberately left the gate itself alone, so "the gate that doesnt drown you" still has all of its own material. seventh one, 124 owns scoping and owns the in the code not in the prompt framing, and it took the two obvious moves, checking the caller against the run and replacing a free text argument with a fixed list, so the gate note cannot re-run either. 124 also named 111 to stay off the schema clamps ground, any later note going near argument validation should do the same. eighth one, 125 owns the human gate and owns the fatigue argument, approving everything is approving nothing, so no later note in this arc re-argues it. 125 also spent the auto versus ask split, so the budgets and kill switches note has to be about caps that stop a run on their own rather than about who gets asked.

the growth rules are unchanged inside the new arcs: splits for granularity, capstone gap check for at most one brick, strict order within an arc, capstone written last.

process note on headers: every notes (n of m) was backfilled on 2026-08-30, splits had been growing arcs while old headers kept the size the arc had on their writing day. from now on any split or add that changes an arcs size also fixes the (n of m) in that arcs already-written notes, same run, committed with the split. arc 11 is 12 checkboxes as it stands, so its notes carry (n of 12) until something splits.

lines the repo has held and should keep holding: no named vendor and no named benchmark, arc 9 held that from 099 through 108 and arc 10 held it all the way through 121, issue_refund, search_docs, get_order_by_id and list_recent_orders are made-up tool names in my own examples and 121 reuses issue_refund rather than inventing a new one. caches are laid and closed, arc 8 owns them and 098 owns their assembly. bm25 scoring is still an unlaid brick on purpose. arc 7 owns measurement. 058 owns how big a chunk is, thats a different knob from how many chunks reach the model and 116 stayed off it.

process note: 108 at 314 under the 350 capstone ceiling, 109 at 214, 110 at 232, 111 at 193, 112 at 222, 113 at 189, 114 at 198, 115 at 190, 116 at 187, 117 at 197, 118 at 207, 119 at 203, 120 at 205, 121 at 326. 121 drafted at 339 and came down by trimming five phrases, no brick lost its mention. both capstones landed in the 310 to 330 band and read fine, aim there rather than at the ceiling. 122 at 219, 123 at 227, 124 at 244, 125 at 249. 124 drafted at 228, then went up when the 111 cross reference went in, it was worth the words. 125 drafted at 254, over the ceiling, and came back under by tightening two sentences rather than dropping the caveat about a tool that fires constantly.

last visuals: mermaid flowchart, eight nodes, two filters and a pause branch (125), pseudocode block, two versions of email_customer, wide and capped, 13 lines (124), plain text annotated artifact, a poisoned tool result and the tool call it produced (123). flowchart, pseudocode and artifact in the last three, so nothing is blocked. the trace note is about one run of twenty calls read after the fact, so an annotated artifact of a real trace, indented calls with timings and costs down the side, is the obvious fit, and a mermaid diagram would be the wrong shape for it anyway.
last exits: stops (125), stops (124), forward (123). only one of the last three points forward, so the next note is free either way, though three stops running means pointing forward is the fresher pick.

process note on visuals: mermaid stacks subgraphs in whatever order it likes and it flipped the two on 065, and on 070 it put the once-per-doc group beside the per-question one rather than above it. so 070s prose says "one group" and "the other group" instead of top and bottom, and 098 names its groups seconds, minutes and months for the same reason. do not write positional references into prose about a mermaid block, github may lay it out differently than a local render. 106 hit this while drafting, "that first fork" became "the fact question" so the prose names the node by its content instead of its place. 108 hit it twice, "the first fork" became "the rule question" and "every other question below" became "every other question here", both for the same reason. 121 sidesteps it entirely, its prose walks the parts by what they are, the toolbox, the run, the array, the exit, and never says which way the picture flows. tables are safe for this, 099 says "top row" and "row two" and github renders rows in file order, and 104 leans on top two rows and bottom two rows the same way. plain text blocks are safe too, 102 labels each step in file order and github shows them that way, 109 says top block and bottom block for the same reason, and 113 leans its whole payoff on "line 3" of a numbered block. code blocks are safe the same way, 116 says the truncate branch and the paginate branch by their labels anyway. sequence diagrams are safer than flowcharts here, 112 rendered with its participants in declaration order, but its prose still names the actors instead of saying left or right. 118 is a two branch flowchart and dodged the whole problem by naming its branches from their content, leave it as a message and write it to plan.md instead, so it reads correctly whichever side github puts them on. mmdc runs in this container only with a puppeteer config passing --no-sandbox, without it the render dies on a root sandbox error that has nothing to do with the diagram.

## NOTES
