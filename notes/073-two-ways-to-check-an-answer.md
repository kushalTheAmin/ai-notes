# 073: two ways to check the answer

builds on: [072](./072-the-same-questions-every-run.md), [013](./013-cosine-similarity.md), [014](./014-what-an-embedding-is.md)
arc: evals, how you know any of it works (3 of 11), ~2 min

072 left a must_say list in the file with nothing reading it. you wrote down "30 days", the model wrote a whole sentence. what turns that into pass or fail.

two ways, and they break on different rows.

| the model answered | must_say check | meaning vs "30 days from purchase" |
|---|---|---|
| "you get 30 days from purchase" (right) | pass | 1.00 pass |
| "about a month after you buy it" (right) | FAIL | 0.86 pass |
| "you get 60 days from purchase" (wrong) | FAIL | 0.97 pass |
| "i cant find that in the docs" (wrong) | FAIL | 0.41 fail |

(passing at 0.75. scores are the shape of it, not a real run)

the must_say check is a substring search, the same includes() you write every day. free, instant, same answer every time. the other one embeds both sentences (014), takes the cosine (013), and cuts at a threshold you picked by hand (019).

top two rows are good answers, bottom two are bad ones. row two is the string check being wrong, "about a month" is fine and it gets marked failed. row three is meaning being wrong, and this is the one i keep re-reading. change 30 to 60 and the sentence says something else entirely, but the score barely moves. embeddings score what a sentence is about, not whether its true. 019 saw this already with log in and log out at 0.87.

i wanted one of them to win. neither does, so you run both, string first, its free.
