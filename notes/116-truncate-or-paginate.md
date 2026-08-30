# 116: when the tool hands back too much

builds on: [115](./115-one-round-itemized.md), [053](./053-what-to-leave-out.md), [113](./113-a-failed-tool-call-goes-back-in.md), [006](./006-context-window.md)
arc: agents, when output starts doing things (8 of 13), ~2 min

115 counted 2,600 of round 3s tokens as text a tool handed back. 053 already told me to truncate a big tool result before it hits the array. in a loop theres a second option, and it only exists because theres a loop.

```python
hits = index.search(query)   # inside search_docs. 47 chunks, about 15,000 tokens

# truncate (053)
result = hits[0:4]
result += "43 more matches, not shown"
# the other 43 are out of reach for good

# paginate
start = (page - 1) * 4
result = hits[start : start + 4]
result += f"page {page} of 12. call again with page={page + 1}"
# the other 43 are 11 more rounds away, if it wants them
```

053 was budgeting one turn. the window (006) is the same fixed ceiling here, but 113 said results stay in the array for good, so every round adds another one and none of the old ones leave.

truncate is final. that not shown line is honesty, not access, the model can read it and still cant reach chunk 9, so it answers from the four it got. paginate hands the decision to the model instead. it reads page 1, decides thats not it, asks for page 2. each page is another full round.

what got me is that pagination isnt a nice to have here. its the only shape of this that lets the model recover from my page size being wrong.

go look at what your tool returns when the result set is big. i had never once decided that number on purpose.
