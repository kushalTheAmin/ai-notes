# 004: tokens are money, how pricing actually works
builds on: [003-bpe-merging-by-frequency](./003-bpe-merging-by-frequency.md)
arc: how machines read text (4 of 8), ~2 min

003 showed how a tokenizer builds its vocabulary by merging pairs. what it skipped is that every token in that vocabulary carries a price, and youre charged the moment you hit send.

api pricing splits into two rates, one for tokens you send in and one for tokens the model writes back. theyre priced differently, output usually costs more per token than input, since generating new text is the harder job, reading your prompt is cheap by comparison.

```
POST /v1/chat/completions  ->  response.usage

{
  "input_tokens": 14,
  "output_tokens": 52
}

pricing (per 1,000,000 tokens)
  input:   $3.00
  output:  $15.00

cost = (input_tokens / 1,000,000 * input_price)
     + (output_tokens / 1,000,000 * output_price)

     = (14 / 1,000,000 * 3.00) + (52 / 1,000,000 * 15.00)
     = 0.000042 + 0.00078
     = $0.000822
```

say a provider charges $3 per million input tokens and $15 per million output tokens. the usage block above came back with 14 tokens in and 52 tokens out. divide each count by a million, multiply by its rate, add the two together. that single reply cost $0.000822, under a tenth of a cent.

one request is basically free. the bill shows up once youre making thousands of requests a day, and it gets worse if your app resends the full conversation on every turn, since that input count grows every single message. i didnt expect output to be priced so much higher than input until i saw it on an actual pricing page, it changed how i think about a long system prompt versus a short one.
