# 102: swap it out, swap it back

builds on: [101](./101-whats-in-the-request-nobody-typed.md), [100](./100-two-gates-around-the-call.md)
arc: the decisions, safety, privacy, and picking your model (4 of 10), ~2 min

101 left a card number sitting in a request i was about to send. heres me taking it back out.

```text
what the user typed
  did rahul m get the refund on his card ending 4417

the map my code builds, and keeps
  PERSON_1  ->  rahul m
  CARD_1    ->  4417

what leaves my server
  did PERSON_1 get the refund on his card ending CARD_1

what the model sends back
  the refund for PERSON_1 to the card ending CARD_1 cleared tuesday

what the user reads, map walked backwards
  the refund for rahul m to the card ending 4417 cleared tuesday
```

its a round trip, not a delete. my code swaps each sensitive span for a label and keeps the real values in a map that stays on my server. the model gets the shape of the sentence and none of the values. it answers about PERSON_1 because PERSON_1 is all it ever saw. then i walk the map the other way and the user reads a normal sentence.

took me a minute to see why this works. the model doesnt need to know rahul is rahul, it just needs something stable to point at. the label is a variable name. feels obvious now, wasnt this morning.

the half that doesnt work: swapping survives only when nothing has to look inside the value. change my question to "is 4417 the card we have on file" and CARD_1 is an empty box, theres nothing in it to check. same for anything you need compared or counted. those go as they are, or the answer does.

and finding the spans is 100s problem wearing a different hat, a classifier wrong in both directions. miss one and it ships anyway.
