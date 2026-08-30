# 111: the arguments cant come out malformed

builds on: [110](./110-the-toolbox-is-written-in-english.md), [049](./049-json-you-can-parse.md), [109](./109-when-the-answer-stops-being-a-suggestion.md)
arc: agents, when output starts doing things (3 of 13), ~2 min

110 got the right tool picked and walked away from the arguments on purpose. the pick runs on english. the arguments dont.

| the rule i want | asked for in the description | written into the schema |
| --- | --- | --- |
| always send an order id | it can leave it out | required, it cant leave it out |
| status is open or closed | it can invent `pending` | enum, `pending` cant be written |
| the id is a string | it can send bare `4471` | typed, comes back `"4471"` |
| no keys i didnt ask for | it can add `reason` | closed object, blocked at the pick |

every tool carries a parameter schema next to its name, and 110 called that more text in the prompt. it is, but it has a second job. once a tool is picked, its schema becomes the legality filter from 049, running at every token of the arguments. left column is a rule i used to write into the description and hope. right column is the same rule where it cant be ignored.

i had these two backwards. i wrote paragraphs into descriptions and treated the schema as documentation. the description is a request, the schema is a clamp. anything you can say as required, as a type, as an enum, move it out of the english.

this holds where the provider actually enforces the schema. where it doesnt, its just more text and youre back on 050s validate and retry.

shape is clamped, choice isnt. `{"order_id": "4477"}` when the user asked about 4471 is perfectly well formed, every field present and the right type, and in 109s world that one runs.
