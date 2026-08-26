# 005: why hindi and gujarati cost more than english
builds on: [004-tokens are money](./004-tokens-are-money.md), [003-BPE, merging by frequency](./003-bpe-merging-by-frequency.md)
arc: how machines read text (5 of 8), ~2 min

004 priced a request by counting tokens in and tokens out. it never asked what language the text was in. turns out that matters a lot.

| same sentence, same meaning | older vocabulary | newer vocabulary |
| --- | --- | --- |
| the food is very tasty | 5 tokens | 5 tokens |
| खाना बहुत स्वादिष्ट है | 22 tokens | 6 tokens |
| ખાવાનું બહુ સ્વાદિષ્ટ છે | 42 tokens | 9 tokens |

real counts, from two tokenizers openai shipped, one older, one newer.

the gujarati row means exactly what the english row means. the old vocabulary charges you 42 against 5, so over 8x the input cost.

003 already explained why. a vocabulary is built by merging whichever pairs turn up most in the training text, and that text was mostly english, so english words earned their merges. gujarati pairs never showed up often enough, so the tokenizer falls back to raw bytes. a gujarati letter takes 3 bytes where an english letter takes 1, and most of those 42 pieces arent even whole letters.

the newer column is what i didnt see coming. 42 down to 9. vocabularies got bigger and the new ones actually made room for scripts like these. the gap mostly closed. mostly. 9 against 5 is still nearly double to say the same thing.

so if your users type in a script that isnt english, check the tokenizer before you promise a cost per message. money is one cost. those tokens fill something else up too, thats 006.
