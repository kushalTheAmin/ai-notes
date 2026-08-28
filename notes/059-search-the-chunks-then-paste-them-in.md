# 059: search the chunks, then paste them in

builds on: [058](./058-cutting-the-docs-into-pieces.md), [021](./021-search-by-meaning-end-to-end.md), [056](./056-closed-book-open-book.md), [052](./052-when-the-text-isnt-mine.md), [045](./045-roles-are-markers.md)
arc: giving the model your data (4 of 12), ~2 min

058 left me with a folder of chunks and nothing that picks one. this is the picking, and its ten lines.

```
# runs once, when a doc lands
for chunk in chunks:                                # 058
    store.add(text=chunk, vec=embed(chunk))         # 014, 017

# runs on every question
def ask(question):
    q = embed(question)                             # same model. 017
    scored = [(cosine(q, c.vec), c) for c in store] # 013
    top = highest_first(scored)[:3]

    context = "\n\n".join(c.text for score, c in top)
    return chat("docs:\n" + context + "\n\nquestion: " + question)
```

the top two lines run once, when the doc arrives. 021 already built that for my recipe folder, its just pointed at chunks now instead of whole notes.

ask() is 021s search with one step bolted on the end, and that step is the entire note. look at the last two lines. i join the three winning chunks with newlines and glue them onto the question as a string.

if you were expecting a documents parameter on the api, same, i went looking for one. some field where you hand over your sources and something clever happens behind the curtain. theres no such field. the chunks show up as characters in the user message, exactly like 056 pasting one paragraph in by hand. a few providers do sell a file-search feature that hides all this, and its running the same assembly, just on their side of the wire.

that loop over every array in the store is free at 400 chunks and not at 4 million, which is a later problem.

what stuck with me is that the model cant tell retrieved text from text i typed. its all one stream (045). so whatever got pulled out of my docs is now instructions, and 052 already showed how that goes.
