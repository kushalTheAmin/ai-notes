# 039: asking the model how sure it is

builds on: [038](./038-why-the-made-up-answer-sounds-right.md), [037](./037-no-row-for-i-dont-know.md), [035](./035-top-k-cuts-the-tail.md)
arc: how it writes, and the knobs you own (8 of 12), ~2 min

038 ended on a maybe and i want to close it. 037s real list topped out at 68%, the invented one at 14%. so read the winners percentage, threshold it, ship. i genuinely thought this was the escape hatch.

```
# the call you want
answer, confidence = ask("does axios export retryPolicy?")
if confidence < 0.8: dont_ship_it()

# the loop you get, once per token
scores = read_every_parameter(prompt)   # 026
pcts   = exp_and_divide(scores)         # 032
token  = pick_a_row(pcts)               # 034

# route 1, read the winners percentage
pcts[token]  ->  14.0%    # 33.7% once top-k rescales it, same token

# route 2, ask it in words
"how sure are you?"  ->  "im highly confident"   # ran the loop above
```

route 1, the number. that 14.0% is a number about rows. it says this word beat the other words by this much, and nothing in that loop checked whether axios exports the thing. it also isnt one number. 032 says 14.0. set top-k to 4 from 035 and the tail is deleted, so the four survivors get rescaled, 14.0 divided by 41.5 is 33.7. same model, same invented method, and the number more than doubled because i moved a knob.

it does carry something. a top row down at 14% usually means the model was torn between words. but torn between words is not the same as catching itself making things up.

route 2, just ask. "how sure are you" is a question, so the answer is tokens, out of the loop above. it will say highly confident about retryPolicy in the same steady voice it uses for isAxiosError. 037 already said this about "i dont know", i just didnt think it applied to confidence too.

theres no readout. you thought you were reading a gauge, it was just more output.
