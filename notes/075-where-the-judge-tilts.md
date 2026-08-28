# 075: where the judge tilts

builds on: [074](./074-let-a-model-grade-it.md), [072](./072-the-same-questions-every-run.md), [038](./038-why-the-made-up-answer-sounds-right.md)
arc: evals, how you know any of it works (5 of 11), ~2 min

074s judge worked because 072 handed it a rubric, must_say "30 days". some golden rows dont have one. "explain the refund policy to a customer" has no string that has to show up, so you type "is this a good answer?" and let the judge decide. thats where it tilts.

| the answer given | judge says |
|---|---|
| "roughly a month, check the item page" | fail, "vague" |
| same fact, two extra sentences of policy talk | pass, "thorough" |
| same fact, phrased the way the model itself writes | pass, "clear and helpful" |
| all 50 rows, that same soft rubric | 48 pass |

(shapes, not a run i logged)

row two got me. i didnt touch the fact. same answer, more words, and more words read as more careful. same instinct that makes a long pull request description feel safer to approve than a one liner. 038 was about a wrong answer coming out polished anyway, and polish is exactly what the judge is reading.

row three is the genuinely weird one. if your app and your judge are the same model, its grading its own dialect, and text that sounds like its own output scores better than the same thing said bluntly.

the last row isnt an answer, its the column. when nearly everything passes, the number stops moving when you change the prompt, and a score that cant go down cant tell you anything.

a smarter judge doesnt fix this. the rubric does, which is 072 doing the work again. a concrete must_say wont delete the tilt, it just leaves the judge less room to fill in with taste.
