# 078: the eval run in ci, and what turns the build red

builds on: [077](./077-fixed-five-broke-two.md), [076](./076-the-score-moved-is-it-real.md), [072](./072-the-same-questions-every-run.md)
arc: evals, how you know any of it works (8 of 11), ~2 min

077 left me reading eval runs like a pull request diff. so put the run where diffs live. the prompt is a file in my repo and ci already watches files, same place lint runs on every pull request.

```
# ci job. trigger: any commit that touches prompts/

new  = run_golden(prompts/answer.txt)    # the 50 rows from 072
base = load(runs/last-green-on-main.json)

broke = [id for id in rows
         if base[id] == pass and new[id] == fail]

# 077: #7 flips on its own, so make each one prove it
broke = [id for id in broke
         if fails(id, new_prompt, 3 tries)
         and passes(id, old_prompt, 3 tries)]

if broke: exit 1      # red, and the message is the ids
else:     exit 0

# grounded 44/50 vs 41/50 gets printed. it gates nothing
```

the wiring is the easy half. what took me a minute is what turns the build red, because a unit test hands back true or false and this hands back 44 out of 50.

my first instinct was fail if the score drops. that gate is wrong in both directions. 076 ran one prompt twice and got 41 then 43 with nothing changed, so a no-op commit can go red. and 077 went 41 to 44 while #22 broke, so it sits green on the run where i needed it most.

so dont gate on the score, gate on the rows. anything passing on main and failing now is red.

heres the part i like. a score that drops is already a row that regressed, theres no other way for a total to fall. so the row gate catches everything the score gate would, plus the breaks hiding inside a win.

it costs you something. #7 flips by itself, so this goes red on noise too, and thats why the ids have to prove it first.
