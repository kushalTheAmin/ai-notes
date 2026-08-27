# 047: the model remembers nothing, your code fakes it

builds on: [046](./046-system-vs-user.md), [045](./045-roles-are-markers.md), [006](./006-context-window.md), [004](./004-tokens-are-money.md)
arc: the prompt is the program (3 of 11), ~2 min

046 left me with system as a strong lean learned in tuning. so how does that lean survive to turn five? it doesnt. i re-send it.

```
u = a message i send, a = the reply that comes back
every message ~10 tokens, to keep the sums easy

turn 1   post [system, u1]                 2 msgs -> 20 input tokens
         get  a1
              ^ my code shoves this into the array. the api kept nothing

turn 2   post [system, u1, a1, u2]         4 msgs -> 40 input tokens
         get  a2

turn 3   post [system, u1, a1, u2, a2, u3] 6 msgs -> 60 input tokens

         text in the array, once each:  60 tokens
         input i actually paid for:     20 + 40 + 60 = 120
```

theres no memory on the endpoint. every call is a fresh flatten from 045, and the model sees the array you posted, nothing before it. multi-turn chat is a trick my code plays. i keep the transcript in a variable, append the models own reply onto it tagged assistant, and post the whole thing again. in the react app its a state array i push onto.

which is why turn 3 costs what it costs. every earlier message is input tokens again (004), on every call. and the array only grows, so a long chat walks into the ceiling from 006.

i went in expecting a session id on the endpoint. theres none by default, which still feels wrong to me. some apis do store the transcript for you now, but its the same array replayed every call and you still pay for it.

what you drop when it stops fitting is its own note later in this arc.
