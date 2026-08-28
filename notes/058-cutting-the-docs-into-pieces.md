# 058: cutting the docs into pieces

builds on: [057](./057-when-you-can-just-send-everything.md), [056](./056-closed-book-open-book.md)
arc: giving the model your data (3 of 12), ~2 min

057 ended on the pile being too expensive to send whole. so you send one piece instead, a chunk. chunking is deciding where those chunks start and stop, before anyone has asked a question.

| where i cut the handbook | what search can hand back | answers "day 10 refund on pro?" |
| --- | --- | --- |
| every sentence | "we refund it in full within 14 days" | no. refund what? and it never says pro |
| nowhere, one big piece | all 40 pages, 30,000 tokens | yes, and every question sends all of it |
| at each heading | "Pro plan / Refunds: full within 14 days, none after" | yes, on about 60 tokens |

all three rows cut the same 40 page handbook. i assumed smaller was strictly better, tighter pieces, less waste. then read row one alone. refund what? that sentence leans on the heading above it and the price two lines up. same as a recipe step that just says fold it in.

row one has a second problem. search only ever sees the pieces, and that one never says pro, so a question about the pro plan might not surface it at all.

row two answers everything and puts me back on 057s bill, 30,000 tokens a question, nine cents at $3 per million. row three keeps the heading attached and sends the refunds section, about 60 tokens.

heres the bit that made it click for me. a chunk is the unit you search and the unit you send, both. one cut decides both jobs, and you make it before you know a single question. chunks usually overlap a bit so a line sitting on a cut still lands whole somewhere.

059 is where these pieces get embedded and actually searched.
