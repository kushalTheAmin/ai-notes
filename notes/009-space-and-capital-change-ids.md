# 009: a space and a capital letter change the ids
builds on: [002-what a token is](./002-what-a-token-is.md), [003-BPE, merging by frequency](./003-bpe-merging-by-frequency.md)
arc: how machines read text (9 of 10), ~2 min

008 was a hardcoded rule slicing digits into chunks. this one is smaller. its one character you cant even see in your editor.

| what you type | pieces | ids |
| --- | --- | --- |
| `"roti"` | `"rot"` + `"i"` | 4744, 72 |
| `" roti"` | `" rot"` + `"i"` | 5868, 72 |
| `"Roti"` | `"Rot"` + `"i"` | 38036, 72 |
| `" Roti"` | `" Rot"` + `"i"` | 28460, 72 |

roti splits into rot and i, same as 002, and that holds in all four rows. the tail id is 72 every time. what moves is the head, a different number in each row.

002 called the vocabulary a hashmap, and the key is the exact bytes. `"rot"`, `" rot"` and `"Rot"` are three different keys, so three different ids. nothing lowercases your text first, nothing strips the space off. the space rides on the front of the word it belongs to.

the counts move too. `"understanding"` is two tokens, `" understanding"` is one. same word, double the price, over a space.

i write react all day, where `Button` and `button` mean completely different things, so the capital didnt surprise me. the space did. i had been picturing a space as the gap between two tokens. its part of the token to its right.

which is why a trailing space at the end of your prompt has a reputation for hurting output. you handed the model a space that belonged to the front of its next word, so now it has to open with a piece carrying none, which it barely saw in training.

one caveat, some older tokenizers really do lowercase everything first. none of the chat models youd call today.
