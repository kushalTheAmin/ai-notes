# 001 — characters vs words, and why both fail

builds on: nothing — starting point
arc: how machines read text (1 of 7) · ~2 min

before a language model can do anything with text, it first has to cut it
into countable pieces — and the two obvious ways to cut it both break.

| split by | this sentence becomes | the problem |
|---|---|---|
| word | i · love · unbelievably · good · tacos (5 units) | "unbelievably" never seen before → no slot, model is stuck |
| character | i · _ · l · o · v · e · _ · u · n · b · ... (30 units) | never stuck, but 30 units for 5 words, and a lone "t" means nothing |

split by word and you get clean, meaningful pieces — but the list of
possible words is infinite. slang, typos, names, made-up words, any
language the model wasnt trained heavily on: none of them have a slot in
a fixed word list. the model meets a word it has never seen and just
breaks.

split by character and that problem disappears — every sentence is built
from a few dozen letters and symbols, so nothing is ever truly unseen.
but now a 5 word sentence turns into 30 tiny pieces, and most of them
carry almost no meaning by themselves. the model has to do a lot of extra
work just to notice that t-a-c-o-s is one thing, before it can even start
thinking about what tacos means.

words are too many and too brittle. characters are too many and too
empty. the fix splits the difference — pieces bigger than a letter,
smaller than most words. thats next.
