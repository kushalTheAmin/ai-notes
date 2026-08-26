# 026: every number, for every token

builds on: [025](./025-a-parameter-is-one-number.md), [024](./024-twice-the-input-four-times-the-work.md)
arc: whats inside the box (5 of 10), ~2 min

025 counted the numbers, eight billion of them. heres the bill. to write one token, the model does arithmetic over all of them.

```
model = load("*.safetensors")     # 8,030,000,000 numbers, 16 GB

answer = []
while len(answer) < 300:                              # a short reply
    scores = touch_every_number(model, prompt + answer)
    answer.append(pick_the_winner(scores))

# numbers touched:
#   8,030,000,000  x  300  =  2,409,000,000,000
```

look at where that call sits. inside the loop. i kept reading it as once per request, its once per token. a 300 token reply means the model walked all 16 GB of numbers 300 separate times, once for each token it wrote.

so you have two axes now. 024 was cost by how much you send in. this is cost by how big the box is, and it charges on every token that comes out.

which explains a couple of things at once. the 8B folder from 025 runs on a laptop, its 405B sibling does not, because those numbers all have to sit somewhere the machine can reach fast, over and over. and a bigger model bills more per output token for the dumb-simple reason that there are more numbers to walk.

one caveat, some newer models are built to skip most of their numbers on each token, which is exactly why they feel fast for their size. the plain ones skip nothing.

in my day job i argue about a 300 KB bundle. this thing reads 16 GB, 300 times, to write you one paragraph.
