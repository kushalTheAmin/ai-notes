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
- [x] a trace, not a log line: observability for a twenty step run (126)
- [x] grade the end state: did the thing actually happen (127)
- [x] count the steps: cost and length as a score (128)
- [x] a model reads the trace: grading the runs a lookup cant score (129)
- [x] the judge moves in front of the gate: a filter before a person sees it (130)
- [x] memory across runs: a store the loop reads before round 1 (131)
- [x] a line in memory outlives the run that wrote it, wrong ones included (132)
- [x] the key decides who reads a memory row back (133)
- [x] a memory row is a second copy, and how long it lives (134)
- [x] a counter in the loop: the cap that stops a run (135)
- [x] the kill switch: stopping the runs already going (136)
- [ ] when not an agent: if you know the steps, write the pipeline
- [ ] CAPSTONE: the trusted agent, assembled

## THREAD

baton: 136 took the second half of the budgets and kill switches split, the manual stop. its visual is a mermaid sequence diagram, four participants, me, a stop flag and two runs already going, with run A asking at round 3 and getting no, me setting the flag, run A asking at round 4 and breaking, and run B not asking until round 6 and breaking there. it makes one move and adds a price. the move, the flag is one row outside every run that each loop reads fresh at the top of a round, so the stop reaches the runs already in flight, which a deploy and a config change cannot, and the click is that you cannot reach into a running loop at all, the loop has to go looking for the stop itself, so a kill switch is a question rather than a kill. the price, it lands at the next round boundary and not now, so a run sitting inside a slow tool call keeps going until it comes back around, and 136 uses 135 flat for the stop landing in an arbitrary place and 122 flat for which half of a half-finished run hurts, re-explaining neither. it also names the crude version once, killing the process, same mess and no record of it. the next checkbox is when not an agent, if you know the steps write the pipeline. that one is about shape rather than control, the case where the loop was the wrong thing to build because the steps were known up front, so it sets a fixed sequence of calls against a model deciding the order every round. 082 owns the loop itself, 115 owns what a round costs, 128 owns cost and length as a score and 135 and 136 own the two stops, so the when not an agent note cannot make cost its whole argument, its subject is knowing the steps in advance. 130 owns putting a check before an action, and 132 and 134 own memory going stale and memory outliving a delete, so none of that is available to it either.

previously, what 136 established: a mermaid sequence diagram, four participants and six messages, no arithmetic anywhere in it and nothing computed. its only numbers are round labels, run A at 3 then 4 which are consecutive and run B at 6, and the prose leans on run B by its name rather than by position, which the process note below requires. it invents no tool names and no order numbers at all, a deliberate break from 135s block after several notes on the same refund. it names 135 once for the arbitrary landing and 122 once for the half-finished write and re-explains neither, and it stays clear of 083, which already owns my code brings its own exits, by sitting entirely on the stop that comes from outside a run. its honest reaction is having taken a while to accept that you cannot reach into a loop thats already running. its real world detail is a cancellation token in .net, which is also its you line, and the line that code which never checks the token never stops is the payoff. it stops. 217 words, drafted at 239 and trimmed in five sentences.

previously, what 135 established: a flat plain text worked example, a header task line, a caps line, six round lines and a closing line. its arithmetic is real and independently rechecked, 1,800 then 2,400 then 3,600 then 4,300 then 4,900 then 5,400 sum to 22,400 across the running total column, each per-round cost is larger than the one before it so the block agrees with 115, and 22,400 clears the 20,000 cap by 2,400 at round 6 of the 8 allowed, so the token cap trips with two rounds spare and the prose says exactly that. it reuses order 88120 and the tool names list_recent_orders, get_order_by_id and search_docs, and invents no new numbers beyond the caps and the costs. it names 114 for the check living outside the model and 122 for which half of a half-finished run hurts, and re-explains neither. deliberately flat and inside one run so it does not collide with 128s five run lines or 126s indented trace, and it says nothing about a duplicate call being a tell, that is 129s. its honest reaction is the cap having no idea where it lands. its real world detail is the timeout you put on an http client because you dont trust the other end, which is also its you line. it points forward, one line, naming 136 as the stop i flip by hand. 232 words, planned mid-band on purpose.

previously, what 134 established: a mermaid flowchart, five nodes, one delete request with three targets and a fifth node connected to nothing on that path, only a dotted arrow out of it. no arithmetic anywhere in it, nothing computed. its prose never says which way the picture flows, it names the stores by what they are. 4471 carries from 131 and 133, 103 is named once for the log store and once by number, and it invents no tool names, no order numbers and no dates, a year later is the only span in it and it is a figure of speech. its honest reaction is having kept calling the store a cache, and the cache-has-a-real-version-behind-it line is the payoff. its real world detail is the delete-user endpoint as a list of tables held in somebodys head, which is also its you line. it stops. 222 words, drafted at 232 and trimmed in three places.
previously, what 133 established: a 12 line pseudocode block, two caret annotations, both aligned by column, no arithmetic anywhere in it and nothing computed. it invents no numbers, 4471 carries from 131, ticket 8812, rahul m and card ends 4417 all carry from 101, acme carries from 101 too, and the tuesday run deliberately has no order number so there is nothing new to check. ACCOUNT is a placeholder rather than a value. it names 131 for the store and 101 for the ride-along data, and stays off 132s ground entirely, no word about a row being stale or planted. its honest reaction is having typed memory[4471] in 131 like it was a variable name. its real world detail is a cache keyed wrong showing someone elses name in the ui, which is also its you line. it points forward, one line, naming 134. 171 words, planned small from the start.
previously, what 132 established: a three column comparison table, four rows, no arithmetic anywhere in it, nothing is computed, and the only counted claim is that thursday reads all three rows, which matches the three rows above it. it reuses order 88120 and the tool name search_docs, and invents nothing new, the wiki page is 123s. it names 123 for the adversarial instance and uses 122s blast radius flat as the term. its honest reaction is having had memory filed under nice-to-have, and its real world detail is the config row someone set in prod years ago that everything still reads off, which is also its you line. it stops. 232 words, drafted at 244 and trimmed in seven places.

previously, what 131 established: a plain text annotated artifact, two labelled runs, one memory row and two caret annotations. no arithmetic anywhere in it, nothing is computed, four rounds is the only count and it appears identically in the block and the prose. it reuses order 88120 from 052, 123, 124 and 127, 88121 from 127, and customer 4471 from 129, and invents no new tool names, the only named call is read_file carried from 118. it names 118 and 047 explicitly to stay off both their ground, and names 028 for the weights caveat. its honest reaction is two, took me a minute to see theres nothing new here, and i went looking for the memory api for way too long. its real world detail is calling it a user_preferences table with a prompt bolted on the end, plus the you line about having cached a users settings. it points forward, one line, naming 132 without previewing it. 215 words, planned small rather than trimmed small, drafted at 246 and cut in six places.

previously, what 130 established: a mermaid flowchart, five nodes, one entry and three labelled exits, no numbers anywhere in it at all. it deliberately extends 125s picture rather than redrawing it, 125s pause is the node this one routes into, and the prose never says which way the diagram flows, it names the exits by their content. no arithmetic, nothing computed. no tool names and no order numbers, same break from the refund example that 128 took. its honest reaction is the first version i sketched having two exits, approve or deny, and that being the bug. its real world detail is the spam filter in front of my inbox, no invented event in it. it stops. 228 words.

previously, what 129 established: a 15 line pseudocode grade prompt plus a 3 line json verdict block. task is find out why 88120 was refunded and write it up, five steps, list_recent_orders(4471) returning 3 orders, get_order_by_id(88120) returning refunded 2400, search_docs("refund reasons") returning late delivery, wrong size, changed mind, then the identical call again, then step 5 writing that the item arrived damaged. no arithmetic in it, the only computed claim is that step 4 duplicates step 3 and that damaged appears in none of the results above it, both true as written. 2400 and 88120 carry from 127, customer 4471 is new and is only an argument value. it returns to the refund example after 128 deliberately left it out, but the task is a writeup rather than an action so it doesnt read as a rerun. it names 074 to stay off its ground, 074 owns the judge and the json, 129 only changes what goes into it. its real world detail is reviewing the final file versus reading the commits that got there. its honest reaction is the last verdict being the one that got me, the writeup reads fine and the reason is invented. it points forward, one line, naming 130 as the same call moved earlier. 234 words.

previously, what 128 established: a flat plain text worked example, five run lines with a rounds count and a token count each, then three summary lines, pass rate 5/5, median 4 rounds and 9,600 tokens, worst 11 rounds and 38,400 tokens. its arithmetic is real, rounds sort to 4, 4, 4, 5, 11 for a median of 4 and tokens sort to 9,200, 9,400, 9,600, 12,400, 38,400 for a median of 9,600, and 38,400 is exactly 4x that median while 11 rounds is 2.75x the median 4. deliberately flat and unnested so it doesnt collide with 126s indented trace. no tool names and no order numbers in it at all, which is a break from 122 through 127 and keeps it from reading as a sixth pass over the same refund. its real world detail is reading it like p95 on a work dashboard, its honest reaction is i wouldnt ship run 5, and it stops. 190 words.

for the record, what 127 established: it turned a run into something scorable. it left the transcript alone and went to the database instead, twenty saved runs of one task against one expected ending, exactly one refund row for 88120, and its table carries two rows with the identical last message and opposite scores, so the point it lands is that the sentence a run ends on is not the thing you grade. it also widened the question past did the thing happen, row three refunded a second order on the way and fails for the row that shouldnt be there, so the check is the whole ending. it named 114 to stay off its ground, 114 runs that query inside the loop once to stop one bad reply going out, 127 runs it after, over saved runs, and hands back a pass rate, and it borrowed 072s golden dataset shape, the right answer for a run being a row rather than a sentence. its visual was a three column comparison table, four rows, the runs last message against the refunds table after it against pass or fail. its numbers are order 88120 carried from 052, 123 and 124, a second order 88121 that exists only for the extra row case, and amounts 2400 and 900. no arithmetic anywhere in it, nothing is computed. its honest reaction is row three, the double refund it didnt see coming. its real world detail is calling the whole thing an integration test, assert on the database, not on what the code said. it restates 114s limit by reference in one clause instead of re-explaining it, the task needs an ending you can look up. it stops.

previously, what 126 established: a plain text annotated artifact, a 12 line trace of one run, seven top level steps with three nested under step 4, tokens in and out and a duration on each, three caret annotations. its arithmetic is real and self consistent, the sub-agents three steps sum to its 4.4s, every step sums to the 10.8s in the header, and each model calls input equals the previous input plus that models output plus whatever the tool or the sub-agent handed back. the flat log line at the bottom of the block says six model call lines, and the trace does contain exactly six model calls. it names 097 to stay off its ground, 097 owns the fields of one call and said so, 126 says that list is still right and the thing it cannot give you is the shape. it also pays off 119, which said the sub-agent returns a sentence you cant audit, by saying the nesting is where you audit it. no dollars anywhere in it on purpose, cost as a score belongs to the next checkbox. its honest reaction is having scrolled a log tail hunting for the bad call when the bad call was fine on its own line. it points forward, one line, without previewing what the next note does.

for the record, what 125 established: a mermaid flowchart, eight nodes, a proposed call through the rule question and the take it back question, with a pause node splitting into approved and denied. no arithmetic anywhere in it, no tool names either, it works off 122s table by reference rather than restating the rows. its prose never points at the diagram by position, it doesnt name the forks at all, it walks the policy in words instead. its honest reaction is having had it backwards, assuming approval was the main safety feature and the code checks were tidying up around it. it has no invented personal event in it, the dialog you stop reading is written at the reader. it stops.

previously, what 124 established: a 13 line pseudocode block, two versions of email_customer, wide with a free text body and the rule sitting in a comment quoting the system message, capped with a customer id check against the current order and a template id checked against a list of three. no arithmetic in it, the only number is order 88120 reused from 052 and 123. it names 111 explicitly to stay off its ground, 111 clamps the shape at the pick and stopped on a well formed id thats the wrong customer, 124s check is the thing that catches that because it knows which order the run is about. it also names 113, both refusals return strings so the model reads the error next round. its real world detail is a deploy key scoped to one bucket, and its honest reaction is taking a minute to see the model as just another caller getting an account. it stops.

so arc 10 is closed and arc 11 is fifteen bricks in. the repo now has an agent that can be described to, called, recovered when a call fails, stopped when it thinks its finished and isnt, and kept inside its window by four different moves plus delegation, and as of 122 a way to rank its own tools by what a wrong call costs, as of 123 a reason that ranking is urgent, as of 124 the first thing that acts on it, tools written narrow, as of 125 a person standing behind the few calls the code cant settle, as of 126 a record of the whole run rather than of each call in it, as of 127 a pass or fail on a finished run that the run itself gets no vote in, as of 128 a rounds and tokens number sitting next to that pass or fail, as of 129 a second model grading the path of a run that has no ending to look up, as of 130 that same judge moved into the path of a call so it screens what reaches the person, as of 131 a store that survives the loop exiting, one row written at the end of a run and read into the array of the next one, as of 132 the reason that store is a liability, rows pile up unchecked so a stale line and a planted one both keep coming back, and as of 133 the key those rows sit under deciding which future runs read them, and as of 134 the fact that the row is a second copy of that data sitting outside every cleanup path, so a delete misses it and nothing expires it, and as of 135 a rounds and tokens counter inside the loop that ends a run when either line is crossed, and as of 136 a flag living outside every run that a person sets and every loop reads at the top of a round, so one stop reaches the runs already in flight. what it still has nowhere is a straight answer on when the loop was the wrong shape to build in the first place. that is the next checkbox and they should be written as if the table in 122, the poisoned wiki page in 123, the two versions of email_customer in 124, 125s two filters, 126s indented trace, 127s pass or fail table, 128s five run lines, 129s graded trace, 130s three exit screen, 131s memory row, 132s pile of four, 133s over-wide key, 134s undeleted copy, 135s tripped cap and 136s flipped flag are all already on the readers desk.

overlap to keep an eye on for arc 11: 050 already appends a broken reply plus an error string and retries, for the models own malformed json, and 113 is the same move aimed at a tool that failed. if a note goes near retries again, name the difference explicitly. second one, arc 11 has "grade the end state, did the thing actually happen", and 114 deliberately stayed on the runtime return path, the check my code runs before the loop hands anything back. arc 11s note is measurement after the fact, scoring a finished run the way arc 7 scores an answer, so open it on that difference. third one, 119 said the sub-agent comes back with a sentence you cant audit, and arc 11s "a trace, not a log line" owns the fix, 119 only named the problem. fourth one, 097 already itemized what a log line for one model call needs, so the trace note is about a run of twenty calls rather than about logging fields. fifth one, that pairing is spent, 123 wrote it. 052 owns injection where the damage is what the model says and 123 owns it where the damage is what my code does, so no later note in this arc re-explains the attack, they use it flat. 123 also already said the fix is keeping the dangerous thing out of reach of a followed instruction, so checkboxes 3 and 4 supply the two halves of that rather than announcing the idea. sixth one, 122 owns blast radius and owns the read vs write correction, so no later note in this arc redefines either, they use the term flat. 122 also deliberately left the gate itself alone, so "the gate that doesnt drown you" still has all of its own material. seventh one, 124 owns scoping and owns the in the code not in the prompt framing, and it took the two obvious moves, checking the caller against the run and replacing a free text argument with a fixed list, so the gate note cannot re-run either. 124 also named 111 to stay off the schema clamps ground, any later note going near argument validation should do the same. eighth one, 125 owns the human gate and owns the fatigue argument, approving everything is approving nothing, so no later note in this arc re-argues it. 125 also spent the auto versus ask split, so the budgets and kill switches note has to be about caps that stop a run on their own rather than about who gets asked. ninth one, 126 owns the run as the unit of observation, the shared id, the nesting and the read-it-after-the-fact trace, and it deliberately left dollars out of its block so cost and length as a score is untouched material. the budgets note comes after that one and should treat the counting as already done, its own subject is what happens when a number crosses the line mid run. tenth one, 127 owns the end state check and owns the pass rate, including the widened version where an unexpected row fails a run, so no later note in this arc re-argues outcome grading, they use it flat. the agent reviews an agent checkbox has to be about judging the runs the lookup cant score, not about repeating this one. eleventh one, 128 owns cost and length as a score and owns the median against worst read, and it spent the argument that a passing run can still be a bad run, so the budgets note cannot re-open it and is only about a number crossing a line mid run. 128 also left dollars as one pointer at 004, so no later note in this arc needs to price anything out. twelfth one, 129 owns grading a run by its path and owns the its-the-input-that-changed framing against 074, so the gate note cannot re-introduce the judge, it inherits it and only moves when it runs. 129 also spent the 075 tilt carry-over and the you-only-see-what-you-paste-in caveat, so neither is fresh material. thirteenth one, 130 owns the judge as an inline control, owns fail closed, and owns the shrink the pile in front of 125 framing, so the budgets note is about a counter crossing a line with no model in it, and the when not an agent note cannot re-argue putting a check before an action. 130 also spent the latency-in-the-path cost against 087, so no later note in this arc needs to price the extra call again. fourteenth one, 131 owns cross-run memory as a mechanism, owns the its-047-one-level-up framing and owns the split from 118 on who does the reading, and it deliberately spent nothing on whether the row is right or on how long its kept. so 132 inherits the row and only asks who rechecks it, and 133 inherits it again and only asks whose it is, and neither re-explains where it came from. 131 also named 028 for the nothing-was-learned caveat, so no later note in this arc needs to re-argue that memory is not training. fifteenth one, 132 owns the accumulating store, owns a row is a claim not a fact, and owns the second life of 123s planted line, so 133 cannot re-argue that a row can be wrong and the when not an agent note cannot reach for memory going stale as its example. 132 also spent the write-once read-forever asymmetry, so the budgets note is about a counter inside one run and nothing carried between runs. sixteenth one, 133 owns the key as the access control list and owns the split from 101, 101 is one call leaving and 133 is the same data filed, so 134 cannot re-argue scoping and cannot reach for another persons data in the row as its example, it inherits both. 133 also deliberately spent nothing on expiry or deletion, so all of that is 134s, and 103 already owns retention and training as two separate account settings, so 134 is retention one level up, in a store i wrote myself, and should name 103 to stay off it. seventeenth one, 134 owns the memory row as a derived copy, owns the delete-misses-it and nothing-expires-it pair, and owns the its-not-a-cache framing, so the budgets note cannot reach for memory as its example at all and the when not an agent note cannot use a stale or undeleted row either, 132 and 134 have both spent that ground. 134 also spent the one honest price of an expiry, the agent forgetting things worth remembering, so no later note re-argues it. eighteenth one, 135 owns the per-run counter, owns whichever-cap-trips-first and owns the stop landing in an arbitrary place mid run, so the kill switch note cannot re-argue any of them, it inherits the counter and is only about a stop coming from outside the run. 135 also spent the per run versus per request framing and used 122 flat for the half-finished write, so neither is fresh material for the rest of the arc. nineteenth one, 136 owns the stop that comes from outside a run, owns the loop-has-to-check-for-itself click and owns the next-round-not-now delay, so the when not an agent note cannot reach for control or stopping as its argument at all, and 083 back in arc 8 already owns my code brings its own exits, which is why 135 and 136 both stayed off it.

the growth rules are unchanged inside the new arcs: splits for granularity, capstone gap check for at most one brick, strict order within an arc, capstone written last.

process note on headers: every notes (n of m) was backfilled on 2026-08-30, splits had been growing arcs while old headers kept the size the arc had on their writing day. from now on any split or add that changes an arcs size also fixes the (n of m) in that arcs already-written notes, same run, committed with the split. arc 11 is 17 checkboxes as of the 135 run, which split "budgets and kill switches" in two, an automatic per-run counter and a flag i flip by hand, so its notes carry (n of 17) until something splits again.

lines the repo has held and should keep holding: no named vendor and no named benchmark, arc 9 held that from 099 through 108 and arc 10 held it all the way through 121, issue_refund, search_docs, get_order_by_id and list_recent_orders are made-up tool names in my own examples and 121 reuses issue_refund rather than inventing a new one. caches are laid and closed, arc 8 owns them and 098 owns their assembly. bm25 scoring is still an unlaid brick on purpose. arc 7 owns measurement. 058 owns how big a chunk is, thats a different knob from how many chunks reach the model and 116 stayed off it.

process note: 108 at 314 under the 350 capstone ceiling, 109 at 214, 110 at 232, 111 at 193, 112 at 222, 113 at 189, 114 at 198, 115 at 190, 116 at 187, 117 at 197, 118 at 207, 119 at 203, 120 at 205, 121 at 326. 121 drafted at 339 and came down by trimming five phrases, no brick lost its mention. both capstones landed in the 310 to 330 band and read fine, aim there rather than at the ceiling. 122 at 219, 123 at 227, 124 at 244, 125 at 249. 124 drafted at 228, then went up when the 111 cross reference went in, it was worth the words. 125 drafted at 254, over the ceiling, and came back under by tightening two sentences rather than dropping the caveat about a tool that fires constantly. 126 at 222, drafted at 230 and trimmed four phrases, not because it was over but because 122 through 125 all landed in the 219 to 249 band and sitting there every run is its own tell. 127 at 208, drafted at 228 and cut in every paragraph, which moved it out of the band but still short of the 160 to 190 note thats overdue. the next one should be planned small rather than trimmed small. 128 at 190, drafted at 210 and planned to sit lower from the start rather than cut back to it, which is where the 160 to 190 note finally landed. 129 at 234, drafted at 252, over the ceiling, and trimmed in three places without losing the 116 caveat or the commits analogy. 130 at 228, drafted at 240, trimmed in four places and then given back six words for naming fail closed once and making the 087 pointer a full clause, both worth it. 131 at 215, drafted at 246 and cut in six places, planned small from the start per the note above rather than written long and squeezed. the four notes since 127 now sit at 208, 190, 234, 228 and 215, which is a wider spread than 122 through 126 managed. 132 at 232, drafted at 244, close enough to the ceiling to want trimming, and it came down by cutting a word or two in seven sentences rather than dropping the caveat about writing the recheck yourself. 133 at 171, the shortest note since 128 and planned that way from the first sketch, the pseudocode block carries both beats so the prose only had to name the key and then take one step past it. the last six now run 208, 190, 234, 228, 215, 232, 171, which is a real spread. 134 at 222, drafted at 232 and trimmed in three places, mid-band on purpose after 133 sat right down at 171. 135 at 232, planned mid-band from the sketch rather than trimmed to it. the last eight run 234, 228, 215, 232, 171, 222, 232, which is still a real spread, but two 232s inside four notes means the next one should be planned nearer 180. 136 at 217, drafted at 239 and trimmed across five sentences, which is under the two 232s but not the 180 it was aimed at, the diagram carries the mechanism and the prose still needed the delay and the killing-the-process caveat. the sub-190 note is now overdue again, 133 was the last one, so 137 should be planned down there from the first sketch rather than written long and cut.

last visuals: mermaid sequence diagram, four participants and six messages (136), flat plain text worked example, six round lines with a running total (135), mermaid flowchart, five nodes with one of them off the main path (134). mermaid has carried two of the last three, and worked examples are spent from 135 and 128, so 137 wants a pseudocode block or a table.
last exits: stops (136), forward (135), stops (134). only one of the last three points forward, so 137 may go either way.

process note on visuals: mermaid stacks subgraphs in whatever order it likes and it flipped the two on 065, and on 070 it put the once-per-doc group beside the per-question one rather than above it. so 070s prose says "one group" and "the other group" instead of top and bottom, and 098 names its groups seconds, minutes and months for the same reason. do not write positional references into prose about a mermaid block, github may lay it out differently than a local render. 106 hit this while drafting, "that first fork" became "the fact question" so the prose names the node by its content instead of its place. 108 hit it twice, "the first fork" became "the rule question" and "every other question below" became "every other question here", both for the same reason. 121 sidesteps it entirely, its prose walks the parts by what they are, the toolbox, the run, the array, the exit, and never says which way the picture flows. tables are safe for this, 099 says "top row" and "row two" and github renders rows in file order, and 104 leans on top two rows and bottom two rows the same way. plain text blocks are safe too, 102 labels each step in file order and github shows them that way, 109 says top block and bottom block for the same reason, and 113 leans its whole payoff on "line 3" of a numbered block. code blocks are safe the same way, 116 says the truncate branch and the paginate branch by their labels anyway. sequence diagrams are safer than flowcharts here, 112 rendered with its participants in declaration order, but its prose still names the actors instead of saying left or right. 118 is a two branch flowchart and dodged the whole problem by naming its branches from their content, leave it as a message and write it to plan.md instead, so it reads correctly whichever side github puts them on. 130 is a flowchart too and dodged it the same way 118 did, its prose names the exits refusing, run it and the person rather than saying which branch sits where. mmdc runs in this container only with a puppeteer config passing --no-sandbox, without it the render dies on a root sandbox error that has nothing to do with the diagram. 134 rendered clean that way, dotted edges with a label, the -. still read .-> form, are fine. 135 has no mermaid in it, its plain text block is safe for positional prose the same way 128s was, and it leans on round 6 by its label. 136 is a mermaid sequence diagram and rendered clean with the same --no-sandbox puppeteer config, participants declared as me, the flag, run A and run B and laid out in that order, and like 112 its prose names the actors rather than saying which side they sit on.

## NOTES
