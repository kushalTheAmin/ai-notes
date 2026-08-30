# 099: should this even be a model call

builds on: [098](./098-everything-around-one-call.md), [019](./019-near-duplicates-and-a-threshold.md), [038](./038-why-the-made-up-answer-sounds-right.md), [041](./041-same-prompt-two-answers.md), [087](./087-the-two-numbers.md)
arc: the decisions, safety, privacy, and picking your model (1 of 10), ~2 min

098 ended with me counting sixteen notes of scaffolding around one model call. thats the price of shipping one, so arc 9 opens on whether to pay it.

heres one support inbox and five jobs it has to do.

| the job | is there a rule that decides it | what i build |
| --- | --- | --- |
| pull the order id out | yes, ORD- then 6 digits | a regex |
| route it to one of our 6 teams | mostly, a keyword table | that table, until the words drift |
| has someone asked this before | no rule, but 019 scores it | embeddings and a threshold |
| is this person angry enough to escalate | no, angry has no spelling | a model |
| write the reply | no | a model |

top row, the answer is already sitting in the text and a rule finds it every time. hand it to a model and you get a slow expensive regex that bills per call (087), wont answer the same way twice (041), and can invent an order id nobody typed (038). i did go looking for a rule for the angry row. theres no spelling of angry.

row two is the one i keep chewing on. the keyword table is fine until somebody renames a product, or writes in gujarati, or just says "the checkout thing". so the question i ask now is whether the list of cases stays closed. hard has nothing to do with it.

the bit that flipped for me: "can a model do this" was never the question. a model can do all five rows. it just does the top one worse than a regex, and charges you for it.

the rest of arc 9 is the rows where a model really is the answer, and what goes around it before real users touch it.
