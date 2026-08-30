# 119: sub-agents, a fresh window with a narrower job

builds on: [118](./118-files-are-the-agents-real-memory.md), [116](./116-truncate-or-paginate.md), [115](./115-one-round-itemized.md), [082](./082-a-while-loop-with-a-model-inside.md)
arc: agents, when output starts doing things (11 of 13), ~2 min

118 moved one artefact out of the array. a sub-agent moves a whole job out. its a tool whose body is another loop from 082, running in its own empty message array.

```
inline, in the parents own window
  round 4   search_docs   ->  3,200 tokens of hits
  round 5   search_docs   ->  2,900 tokens of hits
  round 6   read_file     ->  4,100 tokens
            parent array now carries 10,200 tokens of raw hits

handed to a sub-agent
  round 4   research_agent("which config sets the retry cap?")
                |
                |  its own fresh array: the same 3 calls and the
                |  same 10,200 tokens, gone when it returns
                v
            "retry_max is in config/http.yaml, default 3"   ~15 tokens
            parent array grew by one line
```

the parent asked a question and got back a sentence. the three rounds of searching still happened, in an array that stopped existing when the tool returned.

about the money, those 10,200 tokens still got paid for once, inside the sub-agents own run. what you skip is 115s replay bill, the same hits riding along every round after.

i kept filing this next to 116 and that was wrong. truncating decides how much of a raw result gets into this window. with a sub-agent the raw result never reaches this window, only the conclusion does.

the catch is the sub-agent starts blind. it gets your one line brief and none of the conversation so far, so a vague brief comes back as a confident wrong sentence and you cant see how it got there. if it needs more, you pass it in, or you hand it a filename from 118.

its delegation. when i hand a ticket to someone i dont replay every standup for them, i write the ticket properly.
