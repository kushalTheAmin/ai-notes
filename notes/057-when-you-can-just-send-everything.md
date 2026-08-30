# 057: when you can just send everything

builds on: [056](./056-closed-book-open-book.md), [006](./006-context-window.md), [004](./004-tokens-are-money.md), [047](./047-your-code-fakes-the-memory.md)
arc: giving the model your data (2 of 15), ~2 min

056 ended on ten thousand docs and which one do i paste. the honest first answer is you dont pick, you paste all of them. sometimes thats really the right call.

```
my wiki. ~800 tokens a doc.
window 200,000 (006). input $3 per million (004).

docs   tokens sent   fits?              cost per call
----   -----------   ----------------   -------------
  12         9,600   yes, 190k spare    $0.03
 200       160,000   yes, 40k spare     $0.48
 400       320,000   no, api rejects    -

a 5 turn chat at 200 docs, pile resent every turn (047)
  5 x $0.48 = $2.40 for one conversation
```

top row is a real setup. twelve docs, the whole handbook, pasted into the system message. no embeddings, no index, no search. if your pile fits and barely moves, send everything and go do something else.

the wall i expected was row three, the 006 ceiling. that one is real, the api rejects the call instead of trimming. but look at row two. perfectly legal, 40k to spare, and every call costs 48 cents. put a conversation on it and 047 kicks in, my code resends the pile every turn, so one five turn chat is $2.40 before ive shipped to a single user.

theres a quality version of this too. bury the one useful paragraph in 160k tokens and its easier to miss. more context in doesnt mean a better answer out.

so cost bites first, while everything still technically works. i had retrieval filed as what you reach for when you run out of window. its what you reach for when you run out of money, and that line shows up way earlier.
