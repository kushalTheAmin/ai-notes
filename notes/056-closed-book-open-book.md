# 056: closed book vs open book

builds on: [055](./055-anatomy-of-a-production-prompt.md), [028](./028-numbers-frozen-on-a-date.md), [045](./045-roles-are-markers.md), [053](./053-what-to-leave-out.md)
arc: giving the model your data (1 of 15), ~2 min

055 pointed at this arc as putting a lot more not-mine text in the array on purpose. heres where that starts, and the mechanism is dumber than i expected.

```
same question. my companys wiki. two requests.

CLOSED BOOK
  [ user: "whats our refund window?" ]                    ~6 tokens

  -> "usually 30 days from purchase"     came off the frozen file (028)
                                         fluent, confident, not my company


OPEN BOOK
  [ user: "use only the text below.
           <doc>refunds: 14 days from delivery.
           sale items are final.</doc>
           whats our refund window?" ]                    ~35 tokens

  -> "14 days from delivery"             came off the text i pasted


same endpoint. same array shape (045). one row got longer.
```

closed book is every request youve sent so far. you ask, the answer comes off the file that training froze (028). it sounds the same either way, and our refund policy was never in that pile.

open book is the same question with the answer sitting inside the message. i pasted the paragraph in and told it to use that and nothing else.

thats the whole move. no new endpoint, no mode to switch on. its string concatenation into a row of the array from 045, and one more line in the 053 budget table. some providers do sell a managed version that goes and fetches for you, it still lands as text in the request.

the name for this is retrieval augmented generation, RAG. get text, add it to the prompt, generate. three words in order.

the part i skipped is the hard part. i said i went and got the paragraph, except i have ten thousand docs. so which one.

one honest thing. pasting the paragraph doesnt force the model to use it. it can still answer off the frozen file, or blend both into something that sounds sourced and isnt. saying use only the text below helps a lot. its not a guarantee.
