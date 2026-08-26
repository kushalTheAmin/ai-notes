# ai-notes
learning applied ai, one small note at a time

start here: [001, characters vs words, and why both fail](./notes/001-characters-vs-words.md)

total notes: 10

## ARC 1 - how machines read text
- [001, characters vs words, and why both fail](./notes/001-characters-vs-words.md), the two obvious ways to split text and why they both break
- [002, what a token is](./notes/002-what-a-token-is.md), why a model never reads your sentence, only a list of numbers
- [003, BPE, merging by frequency](./notes/003-bpe-merging-by-frequency.md), how a tokenizers vocabulary gets built, by counting and merging, not by hand
- [004, tokens are money, how pricing actually works](./notes/004-tokens-are-money.md), why input and output tokens are billed at different rates, with the math on a real usage block
- [005, why hindi and gujarati cost more than english](./notes/005-hindi-gujarati-cost-more.md), the same sentence in another script turns into more tokens, so it quietly costs more
- [006, the context window](./notes/006-context-window.md), the hard token ceiling on one request, and why your prompt and the reply share it
- [007, why a model cant count letters](./notes/007-cant-count-letters.md), the ids a model receives have no letters in them, so spelling questions are recall, not reading
- [008, numbers get chunked, so arithmetic gets shaky](./notes/008-numbers-get-chunked.md), digit chunks are cut left to right, but place value runs right to left, so the columns never line up
- [009, a space and a capital letter change the ids](./notes/009-space-and-capital-change-ids.md), the vocabulary key is the exact bytes, so the same word tokenizes differently depending on what sits in front of it
- [010, what the model sees, and what it costs, when i send a request](./notes/010-what-i-send-and-what-it-costs.md), one real request traced end to end, from the string i type to the ids, the bill, and the ceiling, with every earlier note tagged on the part it explains
