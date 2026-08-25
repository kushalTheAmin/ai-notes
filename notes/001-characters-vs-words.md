# 001: characters vs words, and why both fail
builds on: nothing, this is the start
arc: how machines read text (1 of 7), ~2 min

before a model can do anything with your text it has to chop it into pieces it can count. there are two obvious ways to chop, and both break down fast.

| split | the sentence becomes | count | the catch |
|---|---|---|---|
| by word | `the` `roti` `needs` `more` `ghee` | 5 pieces | every piece has to already be in the vocabulary list |
| by character | `t-h-e-_-r-o-t-i-_-n-e-e-d-s-_-m-o-r-e-_-g-h-e-e` | 24 pieces | none of them mean anything alone |

split by word and every piece already carries meaning. roti is a word i grew up hearing at the dinner table, and it lands as one clean chunk, as long as roti is already in the models word list. thats the catch. that list has to hold every real word, in every language, plus every typo, slang term, and camelcase variable name like getUserById, and it never stops growing. show it a new word and the whole approach breaks.

split by character instead and that problem vanishes, every language is just letters so roti is always r-o-t-i. but a five word sentence just became twenty-four little pieces, and before the model can relate roti to the rest of the sentence it first has to work out that r, o, t, and i belong together. do that across a paragraph and youre burning compute stitching letters back into words instead of understanding anything.

i expected one of these to obviously be the right call. neither is, they fail in opposite directions. words are efficient but the vocabulary is infinite. characters are universal but shred meaning into pieces too small to use. the fix is a third option, chunks smaller than words but bigger than letters. thats a token, and its what 002 is about.
