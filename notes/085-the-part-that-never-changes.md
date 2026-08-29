# 085: the part of the prompt that never changes

builds on: [047](./047-your-code-fakes-the-memory.md), [083](./083-when-the-loop-wont-stop.md), [004](./004-tokens-are-money.md), [051](./051-the-model-asks-your-code-acts.md), [048](./048-showing-beats-telling.md)
arc: running it, speed, cost, and when things break (4 of 11), ~2 min

047 said it first, every call re-sends the whole array, and 083 did the addition. heres the part of that bill you can stop paying.

```
one question to my doc-QA agent. what i post:

   system prompt                300 tokens
   6 tool definitions         1,200         same bytes,
   4 few-shot examples        2,500         every single call
 --------------------------------------- cache marker
   the users question           200         new every call

 per token: normal input 1x, cached read 0.1x

   no cache     4,200 x 1                = 4,200
   cache hit    4,000 x 0.1  +  200 x 1  =   600
```

everything above the marker is identical on every call, so the provider keeps the processed version of it for a few minutes and charges a fraction to reuse it. same tokens, a seventh of the bill. it comes back quicker too, since that work is skipped rather than discounted.

the catch is that it matches from the very start of the prompt, as one exact prefix. change one word in your system prompt and everything after it misses. put the users question above the tool definitions and you cache nothing. so the order of my array is a billing decision now, which took me a minute to accept.

two things keep it honest. on the api i use i mark the cut myself and pay a small premium to write it, some providers just do it for you. and theres a minimum, roughly a thousand tokens, so a small prompt doesnt qualify at all.
