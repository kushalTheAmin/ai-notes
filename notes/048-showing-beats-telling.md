# 048: few-shot, showing beats telling

builds on: [047](./047-your-code-fakes-the-memory.md), [045](./045-roles-are-markers.md), [022](./022-guess-the-next-token.md)
arc: the prompt is the program (4 of 11), ~2 min

047 left me holding the whole array, assistant items and all. so nothing stops me writing assistant turns the model never said, which is the whole trick here.

```
telling it:

  system     extract the city. reply as json, key "city",
             lowercase, nothing else
             ^ four rules in one sentence, all of them
               left to the model to interpret
  user       flight to ahmedabad

showing it:

  system     extract the city
  user       book me delhi friday
  assistant  {"city": "delhi"}     <- i wrote this line
  user       pune next week
  assistant  {"city": "pune"}      <- and this one
  user       flight to ahmedabad
             ^ the model said neither, and nothing in
               the array says so (047)
```

top block describes the output i want. it can work fine, but every rule there is a sentence to interpret, and "nothing else" still leaves room for a polite line before the json.

bottom block shows the output i want. two pairs, both answered in the same shape. by 022 the model is continuing text, so the likeliest continuation after that last user turn is one more line shaped like those two. i never typed the words json or lowercase down there. the examples did it for me.

first time i did this it felt like cheating, and it still does a bit. by the time the request lands its one flat stream (045) and the markers just say assistant. stacking the same examples inside one user message works too, its the packaging thats different.

two things worth holding on to. those examples go out on every call, so a fat block of them is a bill you keep paying (004). and the copying is not clever, if all your examples answer in one word you will get one word back for a city thats two.

049 is how you pin the shape properly, for when the json has to parse every time.
