# 049: structured output, getting json you can actually parse

builds on: [048](./048-showing-beats-telling.md), [037](./037-no-row-for-i-dont-know.md), [035](./035-top-k-cuts-the-tail.md)
arc: the prompt is the program (5 of 11), ~2 min

048 got me a shape thats likely, and 037 is why thats all it is. theres always a full list of rows and one wins, and "Sure, heres the json" is a perfectly good row.

so, same task as 048, extract the city from "flight to ahmedabad". this time i attach a schema: an object with a string key `city`.

| row | percentage | with the schema |
| --- | --- | --- |
| `Sure` | 41.0% | not legal, cut |
| `{` | 31.0% | 100.0% |
| `Here` | 22.0% | not legal, cut |
| `The` | 6.0% | not legal, cut |
| **total** | 100.0% | 100.0% |

```
one survivor, so the rescale is a short one

  0.31 / 0.31 = 1.00
```

you have seen this table, its 035. same cut, same rescale, different reason. top-k cut by count because i turned a knob. this cuts by legality, only `{` can legally start a json object, so the other three go to zero and the survivor takes the whole 100.

it runs again at every step. after `{` its heading for a quoted key, and `city` is the only key in my schema, so `city` isnt the likely token there, its the only one.

i kept assuming there was a clever prompt hiding behind this. theres nothing hiding, the filtering happens somewhere else entirely, down at the pick, on the candidate list.

two things. a plain json mode with no schema only promises the braces balance, not that your keys are in there. and valid is not correct, `{"city": "delhi"}` parses fine for a flight to ahmedabad and is still wrong (038).
