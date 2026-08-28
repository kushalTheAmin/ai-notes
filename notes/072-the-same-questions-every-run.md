# 072: the same questions, every run

builds on: [071](./071-looks-good-doesnt-scale.md), [067](./067-did-the-right-chunk-come-back.md), [069](./069-did-the-answer-come-from-the-docs.md)
arc: evals, how you know any of it works (2 of 10), ~2 min

071 ended on the half that runs itself, and it only ran itself because i wrote those labels down by hand back in 067. so write all of them down, the answer too. a golden dataset is that file, a fixed set of questions and, for each one, what should come back.

```
evals/golden.jsonl    one question per line, 50 of them, checked in

{"id": 7,
 "q": "whats the refund window",
 "chunk": "billing.md#refunds",             <- 067/068 score the rank
 "must_say": ["30 days", "from purchase"]}  <- a right answer has these

{"id": 8,
 "q": "can i get money back after 6 weeks",
 "chunk": "billing.md#refunds",             <- same chunk, no shared word (062)
 "must_say": ["no", "30 days"]}


 mon  prompt A, same 50 q   recall@5 0.62 (31/50)   grounded 41/50
 fri  prompt B, same 50 q   recall@5 0.72 (36/50)   grounded 46/50
                            +0.10                   +5 answers

 fri  prompt B, but 10 questions added first
      recall@5 0.70 (42/60).  0.70 next to 0.62 is two papers,
                              so the gap between them says nothing
```

it sits beside the code like a test fixture, because thats what it is.

heres the bit that took me a minute. the file being boring is the feature. first new failure that came in, i wanted to open the file and add it right there, and thats the move that breaks it. a score is never a number on its own, its half of a comparison, and both halves have to have sat the same paper. you do grow it, just not mid-comparison. add the questions, then re-run the old prompt so both sides are back on the same file.

fifty isnt a magic number, its a guess at coverage. count the kinds of question your users ask, the three-word ones, the ones using no word any doc contains, the ones about a page nobody wrote. four doesnt reach.

writing the expected answer down doesnt make it check itself though. "30 days" has to match a whole sentence some model wrote, and thats less obvious than it looks.
