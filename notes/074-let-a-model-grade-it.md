# 074: let a model grade the answer

builds on: [073](./073-two-ways-to-check-an-answer.md), [072](./072-the-same-questions-every-run.md), [049](./049-json-you-can-parse.md)
arc: evals, how you know any of it works (4 of 11), ~2 min

073 left me with two checks that both get ordinary answers wrong, one too strict, one too loose. so, stop writing the checker. hand the answer to a model and ask it to grade.

```
row    = golden[0]              # 072 wrote this row
answer = my_app(row.question)   # "about a month after you buy it"

grade_prompt = """
question: how long is the return window?
a correct answer must say: 30 days
the answer given: about a month after you buy it

does the answer given say that?
reply as json: {"verdict": "pass" or "fail", "why": "one short line"}
"""

verdict = model(grade_prompt, temperature=0)
```

what comes back, on the two rows 073 broke on:

```
about a month after you buy it
  {"verdict": "pass", "why": "a month is 30 days"}

you get 60 days from purchase
  {"verdict": "fail", "why": "says 60, must say 30"}
```

look at that call. theres nothing new in it. its a prompt (045), it asks for json back (049), temperature 0 so the grade wobbles as little as it can, which after 041 you know isnt never. the only new part is whats inside. the must_say line you typed by hand in 072 is the rubric now, and a second model reads it instead of includes().

and it gets both of 073s broken rows right. the paraphrase passes, the swapped number fails. neither mechanical check managed both. costs one model call per row, which next to the two minutes of reading in 071 is nothing.

my first reaction was that this is circular, using the thing to check the thing. it kind of is. the grader is the same next-token machine as the thing being graded, so 037 and 038 apply to it too, it can be confidently wrong and never flag it.

075 is where it tilts.
