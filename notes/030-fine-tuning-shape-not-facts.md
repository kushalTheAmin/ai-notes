# 030: fine-tuning moves the shape, not the facts

builds on: [029](./029-base-model-doesnt-answer.md), [025](./025-a-parameter-is-one-number.md)
arc: whats inside the box (9 of 10), ~2 min

029 ended on the second training pass, the small one that makes a model answer instead of continue. you can run that pass yourself, on your own examples. thats fine-tuning. i had the obvious idea straight away, point it at our teams runbook and ship a bot that knows our stuff.

```
my tuning file: 60 request/reply pairs. 3 of them:

  req  whats our deploy window?
  rep  - tue and thu, 2-4pm IST
       - no deploys after 4pm friday
       ticket: OPS-114

  req  who owns the billing service?
  rep  - team atlas
       - oncall lives in #billing-oncall
       ticket: OPS-231

  req  where do staging logs go?
  rep  - grafana, filter env=staging
       - kept 7 days
       ticket: OPS-088

  the shape (bullets, terse, ticket line) ... in all 60
  each fact (2-4pm, atlas, 7 days)        ... in 1 of 60

after tuning, a question it never saw:

  req  how do i rotate an api key?
  rep  - rotate it in the console
       - old key stops working in 24h
       ticket: OPS-402
               ^^^^^^^ shape: perfect. this ticket does not exist.
```

the shape is in all 60 examples. each fact is in exactly one. every step of tuning nudged the numbers toward bullets and short lines and a ticket at the end, sixty times over. the deploy window got a single nudge, competing with everything else in the pile.

so on a question it never saw, the format comes out perfect and the ticket number is invented. thats the part that got me. wrong answer, house style, and i would have believed it.

you can push a fact in by repeating it enough. but 025 already found no facts table in that file, so what you get is a lean toward some wording, not a lookup. and when that fact changes you run the tuning again, where a doc is one line to edit.

so tuning buys you how it answers. what it knows has to show up some other way, handed in at request time, which is a whole arc on its own later.
