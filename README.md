# ai-notes
learning applied ai, one small note at a time

start here: [001, characters vs words, and why both fail](./notes/001-characters-vs-words.md)

total notes: 5

## ARC 1 - how machines read text
- [001, characters vs words, and why both fail](./notes/001-characters-vs-words.md), the two obvious ways to split text and why they both break
- [002, what a token is](./notes/002-what-a-token-is.md), why a model never reads your sentence, only a list of numbers
- [003, BPE, merging by frequency](./notes/003-bpe-merging-by-frequency.md), how a tokenizers vocabulary gets built, by counting and merging, not by hand
- [004, tokens are money, how pricing actually works](./notes/004-tokens-are-money.md), why input and output tokens are billed at different rates, with the math on a real usage block
- [005, why hindi and gujarati cost more than english](./notes/005-hindi-gujarati-cost-more.md), the same sentence in another script turns into more tokens, so it quietly costs more
