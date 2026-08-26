# 008: numbers get chunked, so arithmetic gets shaky
builds on: [003-BPE, merging by frequency](./003-bpe-merging-by-frequency.md), [007-why a model cant count letters](./007-cant-count-letters.md)
arc: how machines read text (8 of 10), ~2 min

007 was letters hiding inside a token. digits hide the same way, but with digits theres a second problem stacked on top, and thats the one that breaks addition.

```
# adding, the way you do it and the way a calculator does it: RIGHT to left
carry = 0
for place in [ones, tens, hundreds, thousands]:
    column = digitAt(a, place) + digitAt(b, place) + carry

# how the tokenizer cuts a number: LEFT to right, at most 3 digits at a time
pieces = []
while digits.length > 0:
    pieces.push(digits.splice(0, 3))

"1234"  ->  "123", "4"    ids [4513, 19]    ones digit is its own token
 "567"  ->  "567"         id  [19282]       ones digit is buried in here
```

the two loops run in opposite directions. thats the whole problem.

place value is a right to left idea, ones then tens then hundreds. the cutting rule goes the other way and has no concept of it. 003 said nobody hand-writes these cuts, frequency decides them. digits are the exception, the tokenizer i pulled those ids from has an actual hardcoded rule for runs of digits. still nothing about math in it.

so watch what that did. the ones digit of 1234 came out as its own token, 19. the ones digit of 567 is welded inside 19282 along with the 5 and the 6. to add those numbers you need both ones digits sitting in one column. theres no column anywhere in that array.

models get plenty of arithmetic right anyway, training text is full of it and the common shapes are memorized. some tokenizers split every single digit, which helps a lot. but its still pattern matching over chunks, so the longer the numbers get, the shakier it gets.

i had always filed model math failures under reasoning. good chunk of it is just where the scissors landed.

009 does this one more time, with a space.
