# 105: renting the model, or owning it

builds on: [104](./104-ten-wrong-answers-a-day.md), [025](./025-a-parameter-is-one-number.md), [087](./087-the-two-numbers.md)
arc: the decisions, safety, privacy, and picking your model (7 of 10), ~2 min

104 stopped asking about the request and started asking about the feature around it. this one widens again, right past my code. who runs the numbers.

025 said an open model is a folder with one huge file of eight billion numbers in it. you can download that folder. so theres a second option, put that file on a machine and serve it yourself. own means the weights, the machine is still rented by the hour.

i assumed this was a cost question, so i wrote one day of traffic both ways. 087s doc-QA question, 2.3 cents of model calls each.

```
same feature, same day

RENT   billed per token
  4,000 questions   x 2.3c     =  $92.00
    400 questions   x 2.3c     =   $9.20
      0 questions   x 2.3c     =   $0.00

OWN    billed per hour, one machine at $3
  4,000 questions   24h x $3   =  $72.00
    400 questions   24h x $3   =  $72.00
      0 questions   24h x $3   =  $72.00

crossover: about 3,130 questions a day
```

the zero rows are the whole thing. rented is a function of traffic, owned is a function of the clock. at 3am with nobody awake the rented bill is nothing and that machine is still billing.

so under roughly three thousand a day, rent. over it, own. rates move every month, the shape doesnt.

that felt neat, and it was the easy half. the rest never touches either line. owning means no alias moves under you (095) and nobody retires your model (096). nothing leaves the building (103). and you are the provider now, so 088s 429 becomes your own queue backing up and 093s fallback has nowhere to fall.

which half of your bill can you actually predict?
