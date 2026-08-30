# 113: a failed tool call goes back in

builds on: [112](./112-any-agent-any-toolbox.md), [083](./083-when-the-loop-wont-stop.md), [051](./051-the-model-asks-your-code-acts.md)
arc: agents, when output starts doing things (5 of 13), ~2 min

112 left the tools arriving from a server, code i dont own, over a network. so it fails sometimes.

```
the messages array, one entry per line

1  user     wheres my order 4471
2  model    call get_order_by_id, order_id 4471
3  tool     error: no order 4471 on this account   <- appended, not thrown
4  model    call list_recent_orders                <- it read line 3
5  tool     one order, id 44718
6  model    call get_order_by_id, order_id 44718
7  tool     status shipped
8  model    looks like 4471 was missing a digit, 44718 is shipped
```

my instinct was a try/catch around the call. log it, throw, red box for the user. thats how i handle a dead api in react.

but the loop from 082 is a conversation, and an exception isnt something the model can read. so i dont throw. the error text goes into the array as that calls result, the same slot a real result would have sat in, and the loop runs another round.

line 3 is the whole note. the model reads it, picks a different tool, finds the real id, tries again. i kept looking for where id have to write that recovery. you dont write it, it falls out of the error being in the context.

one thing to keep straight, this is for errors the model can act on. a timeout or a 429 is your codes problem, retry those yourself (089), dont spend a round on them.

and nothing here stops it failing forever, 083s counter does. knowing when the loop is actually finished is 114.
