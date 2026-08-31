# 127: grade the end state

builds on: [126](./126-a-trace-not-a-log-line.md), [114](./114-no-tool-call-isnt-done.md), [072](./072-the-same-questions-every-run.md)
arc: agents you can trust (6 of 17), ~2 min

126 put a whole run on one screen. but every judgement in that block is me, reading it, and the tokens down the right side dont say whether the run worked.

so i stopped reading runs and looked at the database instead. twenty saved runs of one task, one expected ending, exactly one refund row for 88120. four of them:

| the runs last message | refunds table, after | score |
| --- | --- | --- |
| refunded 88120, 3 to 5 days | 88120, 2400 | pass |
| refunded 88120, 3 to 5 days | empty | fail |
| refunded 88120 | 88120, 2400 and 88121, 900 | fail |
| couldnt do it, escalating to a human | empty | fail |

top two rows are the same sentence, word for word, opposite scores. one run moved money, one narrated it. which is which? nothing in the text tells you, so the text isnt what you grade.

row three i didnt see coming. it refunded 88120, true, and it refunded 88121 on the way. did the thing happen, yes. was it a good run, no. so the check is the whole ending, including rows that shouldnt be there.

114 ran this query inside the loop, once, to stop one bad reply going out. this runs after, over saved runs, and gives me a pass rate. 072 wrote the right answer down for every question, here the right answer is a row.

its an integration test, really. assert on the database, not on what the code said. 114s limit comes with it, the task needs an ending you can look up.
