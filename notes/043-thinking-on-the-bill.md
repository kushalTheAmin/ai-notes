# 043: the thinking shows up on the bill

builds on: [042](./042-thinking-by-writing.md), [004](./004-tokens-are-money.md), [040](./040-how-the-loop-stops.md)
arc: how it writes, and the knobs you own (12 of 13), ~2 min

042 ended with the model talking to itself on the page. every word of that talking is an output token.

```
request
  "max_tokens": 2000            <- room for thinking AND answer

response
  content: [ the reply, 100 tokens, the part i get to read ]
  usage: {
    "input_tokens":    40,
    "output_tokens": 1200       <- 1100 of these were thinking
  }

output rate from 004: $15.00 per 1,000,000 tokens

  reply        100 tokens  ->  $0.0015
  thinking    1100 tokens  ->  $0.0165
  --------------------------------------
  billed      1200 tokens  ->  $0.0180
```

so the answer i actually got cost $0.0015. the thinking behind it cost eleven times that. eleven of every twelve tokens on this bill is text i never read.

whether you get to read it depends on the provider. some hand back the full thinking, some give you a summary, some nothing at all. you pay the same either way, its output tokens, the pricier of the two rates from 004.

now look at max_tokens again. 040 said it counts tokens and cuts, doesnt care what the text says. it counts the thinking too. so you set 500 expecting a short answer, the model spends all 500 working out loud, and what comes back is cut off or empty, with the flag from 040 reading max_tokens. billed for all 500 either way.

thats the one that got me. i had max_tokens filed as how long can the reply be. its how much room the model gets in total.
