# ai-notes
learning applied ai, one small note at a time

start here: [001, characters vs words, and why both fail](./notes/001-characters-vs-words.md)

total notes: 25

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

## ARC 2 - meaning as numbers
- [011, a vector is just a list of numbers](./notes/011-a-vector-is-a-list-of-numbers.md), a token id is a row number into one big table, and the row is a fixed length array of floats
- [012, dot product, by hand](./notes/012-dot-product-by-hand.md), multiply two equal length arrays slot by slot, add up the products, and the one number that falls out tells you whether they lean the same way
- [013, cosine similarity, a score that ignores size](./notes/013-cosine-similarity.md), divide the dot product by both arrays lengths and the score stops caring how big the numbers are
- [014, what an embedding is](./notes/014-what-an-embedding-is.md), send text to a model and one fixed width array of floats comes back, and the width is the same for two words or eight hundred, which is what makes any two texts comparable
- [015, nearby means similar](./notes/015-nearby-means-similar.md), the cosine between two sentences tracks what they mean, not which words they share, and that high score is all anyone means by near
- [016, one word, many meanings](./notes/016-one-word-many-meanings.md), the same word gets different floats depending on what surrounds it, because the array is computed from the whole string instead of looked up per word
- [017, the embedding model is its own product](./notes/017-embedding-model-is-separate.md), a different endpoint with no messages and no temperature, billed on input only, and around 150x cheaper per token than the chat model
- [018, classify with no training](./notes/018-classify-with-no-training.md), embed one example sentence per label, cosine a new string against each, take the highest, and thats an entire classifier with no training run in it
- [019, near-duplicates, and the one number you have to pick](./notes/019-near-duplicates-and-a-threshold.md), with no labels to rank against you have to commit to a threshold, you find it by scoring pairs you already know, and whatever you pick both merges non-dupes and misses real ones
- [020, finding the groups nobody labeled](./notes/020-clustering-no-labels.md), with no labels at all the groups fall out of the scores themselves, by assigning every item to its closest center and moving each center to the average of what it caught, until nothing switches
- [021, how search by meaning works, end to end](./notes/021-search-by-meaning-end-to-end.md), embed the whole folder once, embed the query at search time, cosine against every stored array and keep the top few, which finds the right note even when it shares no words with what you typed

## ARC 3 - whats inside the box (enough to not be fooled, no more)
- [022, all it does is guess the next token](./notes/022-guess-the-next-token.md), one call hands back a score for every token in the vocabulary, something picks one, it gets stuck on the end of the input, and the whole list runs through again
- [023, attention, every token looks at every other token](./notes/023-attention-every-token-looks.md), each token scores itself against every other token in the input with a dot product, those scores become percentages, and the token gets rebuilt as a weighted blend of its neighbours
- [024, why twice the input is four times the work](./notes/024-twice-the-input-four-times-the-work.md), every token scoring every other token means the score count is tokens times tokens, so doubling the input quadruples the work, which is where the context window ceiling and the wait before the first word both come from
- [025, a parameter is one number the model learned](./notes/025-a-parameter-is-one-number.md), an open models folder is a tiny config, a tokenizer, and one huge file of eight billion numbers, with no rules or facts table anywhere in it
