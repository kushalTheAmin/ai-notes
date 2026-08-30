# 024: why twice the input is four times the work

builds on: [023](./023-attention-every-token-looks.md), [006](./006-context-window.md)
arc: whats inside the box (3 of 10), ~2 min

023 ended on four tokens making sixteen scores. every token scores itself against every other one, so the count is just tokens times tokens.

| input tokens | scores, tokens x tokens |
| --- | --- |
| 4 | 16 |
| 8 | 64 |
| 1,000 | 1,000,000 |
| 2,000 | 4,000,000 |
| 200,000 | 40,000,000,000 |

look at the doublings. 4 tokens to 8, and the work goes 16 to 64. 1,000 to 2,000, it goes a million to four million. double the input, quadruple the work. the model isnt being slow, thats the shape of the loop.

in my day job a nested loop over the same array is a code review comment. here its the whole point, its what makes " more" know about roti.

i had this filed as a vague "long prompts are heavy" thing until i wrote out that last row. 006s context window ceiling isnt a number somebody picked to annoy you, its roughly where this stopped being affordable. a long prompt also sits there a while before the first word appears, because all those scores happen before the model guesses token one.

one caveat keeps this honest. the rest of the models work grows in a straight line with your tokens, so at short lengths you never feel this. attention takes over once the input gets long. and this loop runs many times per request, so pick a row and multiply.

004 charges you per token, in a straight line. the work behind those tokens isnt. now i know why some providers charge extra past a certain input length.
