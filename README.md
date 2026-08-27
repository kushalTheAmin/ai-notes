# ai-notes
learning applied ai, one small note at a time

start here: [001, characters vs words, and why both fail](./notes/001-characters-vs-words.md)

total notes: 48

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
- [026, every number, for every token](./notes/026-every-number-every-token.md), the model runs arithmetic over all eight billion of its numbers to produce a single token, once per token and not once per request, which is why big models are slow to serve and cost more per token out
- [027, what a bigger model actually buys](./notes/027-what-bigger-actually-buys.md), the same five asks at 8B and 405B, where the extra numbers buy more memorized text and a longer instruction held together, and where they buy nothing at all
- [028, the numbers got frozen on a date](./notes/028-numbers-frozen-on-a-date.md), training wrote the file once and then it ended, every call since only reads it, so the knowledge carries the date its pile of text stopped and no amount of chatting adds to it
- [029, a base model doesnt answer, it continues](./notes/029-base-model-doesnt-answer.md), straight out of training the model just carries on writing the page your question came from, and a second much smaller pass over request and reply examples is what makes answering the likely continuation
- [030, fine-tuning moves the shape, not the facts](./notes/030-fine-tuning-shape-not-facts.md), you can run that second pass on your own examples, and the shape every example shares gets learned while the fact sitting in just one of them comes back confidently wrong
- [031, the box, closed](./notes/031-the-box-closed.md), the whole arc in one picture, a file built once out of two training passes and read whole on every single token, with the guessing loop running on top of it

## ARC 4 - how it writes, and the knobs you own
- [032, raw scores arent percentages yet](./notes/032-raw-scores-arent-percentages.md), what the model hands back is unbounded numbers, some of them negative, and two steps turn them into percentages that add to 1
- [033, temperature is one divide](./notes/033-temperature-is-one-divide.md), the same four scores run at 0.4, 1.0 and 2.0, where a small divisor spreads them apart and a big one squashes them together, and the ranking never moves either way
- [034, greedy takes the top row, sampling rolls for it](./notes/034-greedy-vs-sampling.md), greedy returns the favourite every time and kills temperature, sampling rolls one number and walks the rows until the running total passes it, so each token wins as often as its percentage says
- [035, top-k cuts the list before the roll](./notes/035-top-k-cuts-the-tail.md), keep the k best rows and delete the rest, then rescale the survivors so they add back to 1, which quietly hands the deleted tails probability to the favourite
- [036, top-p cuts by running total, not by count](./notes/036-top-p-cuts-by-running-total.md), add percentages down the list until the total passes p and keep whatever you touched, so a certain model keeps two rows and a torn one keeps four at the very same setting
- [037, theres no row for "i dont know"](./notes/037-no-row-for-i-dont-know.md), the same two steps run on a prompt the model has seen a million times and on a class i invented while writing the note, and both lists come back adding to 100.0% with a winner on top
- [038, why the made-up answer sounds right](./notes/038-why-the-made-up-answer-sounds-right.md), a real export and one i invented run through the exact same steps and come out looking the same, and nowhere in those steps is there anything that asks whether it is true
- [039, asking the model how sure it is](./notes/039-asking-how-sure-it-is.md), the winning percentage is about which word beat which and it more than doubles when you set top-k, and asking in words just runs the same loop over tokens like "im highly confident"
- [040, how the loop actually stops](./notes/040-how-the-loop-stops.md), one prompt run three ways, the done token winning a row on its own, a stop string the api matches on the way out, and a token ceiling that cuts mid-word, with only the stop_reason flag telling a finished answer apart from a truncated one
- [041, the same prompt, twice, two different answers](./notes/041-same-prompt-two-answers.md), two calls at temperature 0 come back with the scores nudged in the 4th decimal, which is enough to swap a near-tied top row and send the rest of the answer down a different sentence
- [042, the model thinks by writing](./notes/042-thinking-by-writing.md), one sum forked two ways, where a plain model has to commit to the first digit of the answer before doing any working out, and a reasoning model spends tokens on the steps instead, because the text already written is the only scratch space it has
- [043, the thinking shows up on the bill](./notes/043-thinking-on-the-bill.md), one usage block where 1100 of 1200 output tokens went on thinking i never got to read, billed at the same rate as the answer, and a max_tokens ceiling that counts those tokens too
- [044, one tokens journey out, and every knob you own](./notes/044-one-token-on-the-way-out.md), the whole arc as one pipeline, where temperature divides before the exp step, k and p cut the list, and something takes the top row or rolls for it, with no step anywhere in it that can add a row the model didnt already have

## ARC 5 - the prompt is the program
- [045, roles are markers inside one stream of tokens](./notes/045-roles-are-markers.md), the messages array i post gets flattened into one flat list of tokens with small markers for who said what, and it ends on the assistant marker with nothing after it, which is where the guessing starts
- [046, system vs user, and why system usually wins](./notes/046-system-vs-user.md), there is no code anywhere comparing the two messages, the model follows the system one because tuning made that the habit, which makes it a strong default and never a guarantee
- [047, the model remembers nothing, your code fakes it](./notes/047-your-code-fakes-the-memory.md), the endpoint keeps nothing between calls, so multi-turn chat is my own code re-posting the whole transcript every turn and paying for the older messages again each time
- [048, few-shot, showing beats telling](./notes/048-showing-beats-telling.md), nothing in the array proves who wrote what, so a couple of assistant turns i made up myself set the shape of the answer better than a sentence of rules describing it
