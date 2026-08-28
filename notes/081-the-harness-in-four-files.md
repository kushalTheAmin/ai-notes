# 081: the whole eval harness, in four files

builds on: [070](./070-from-my-docs-to-an-answer.md), [071](./071-looks-good-doesnt-scale.md), [072](./072-the-same-questions-every-run.md), [073](./073-two-ways-to-check-an-answer.md), [074](./074-let-a-model-grade-it.md), [075](./075-where-the-judge-tilts.md), [076](./076-the-score-moved-is-it-real.md), [077](./077-fixed-five-broke-two.md), [078](./078-what-turns-the-build-red.md), [079](./079-read-the-failures-sort-them-into-piles.md), [080](./080-who-tells-you-its-broken.md)
arc: evals, how you know any of it works (11 of 11), ~2 min

080 left golden.jsonl growing on its own, filling up with questions people actually typed. thats the last brick. heres the whole arc sitting in one folder.

```
evals/

  golden.jsonl  50 rows. question, the chunk that answers it,
                must_say. rows also arrive from live traffic       072 080

  run.py        per row: ask the arc 6 system (070), score it
                  rank of the right chunk   free, from the search  067 068
                  must_say substring        free, instant              073
                  judge call, temp 0        one model call a row       074
                                            rubric stays concrete      075
                writes runs/<name>.json, one line per row id

  diff.py       this run vs runs/last-green.json
                  broke = passed there, failing here                   077
                  re-run each id 3x before believing it                076

  ci.yml        on any commit to prompts/: run, diff, exit 1 if
                broke is not empty. the score prints, gates nothing    078

  me            open the broke ids, sort into piles                071 079
```

all of it exists because of one number in 071. checking an answer by hand is two minutes, and you pay it again on every prompt tweak, so fifty questions across an afternoon of fiddling is twenty hours of me. the harness never made that check cheaper. it moved it. the machine reads all fifty, i read the six that came back red.

run.py calls the arc 6 pipeline (070) like any other function. two of the scores are free, the ranks fall out of the search results anyway (067, 068). the answer is the part that needs a model, so the judge grades it against the must_say string (074), with 075 taped to the side, keep the rubric concrete or it starts scoring length and tone.

diff.py is the one i would not have written a month ago. i thought a run produced a score. it produces fifty rows, and the score is a sum that forgets which rows built it (077). so i compare ids against the last green run, and anything passing there and failing here gets re-run three times before i believe it, because four rows flip on their own (076).

ci.yml lives in the same folder as the workflow that runs jest on our react app, and it fails the same way, one red x on the pull request. it prints 44/50 and gates on nothing (078).

which of those four files would you have written first? i wrote run.py, and it turned out to be the least interesting one. the scoring is a couple of lines. everything else is the file, the comparison, and the piles.

arc 8 is the other half of the deploy in 080. this harness tells you the answers are good. it has nothing to say about the answer that took nine seconds to show up.
