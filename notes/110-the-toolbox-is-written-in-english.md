# 110: the toolbox is written in english

builds on: [109](./109-when-the-answer-stops-being-a-suggestion.md), [051](./051-the-model-asks-your-code-acts.md), [045](./045-roles-are-markers.md)
arc: agents, when output starts doing things (2 of 13), ~2 min

109 ended on a tool_calls block naming issue_refund, like the model just knew that function was there. it didnt. i told it, and i told it in english.

```
same model, same question, same two functions underneath.
i changed only the strings.

v1
  search    "search the database"
  lookup    "look up a record"

  user: wheres order 4471?
  model picks -> search        both fit. its a guess

v2
  search_help_articles
      "full text search over public help articles.
       for how-to questions. knows nothing about orders."
  get_order_by_id
      "fetch one order by its number. use whenever the
       user names an order id."

  user: wheres order 4471?
  model picks -> get_order_by_id
```

the tools array looks like config, and thats what fooled me. its not. it gets flattened into the same token stream as my system and user messages (045), so the toolbox reaches the model as more text in the prompt. the argument schema is in there too, also as text, but the pick happens on the name and that one line of description.

v1 is what i write first, every time. short names, i know what they mean. wheres order 4471 fits search about as well as it fits lookup, so it picks one. thats a coin flip i shipped.

v2 added no code. longer names, and a description that says where the tool stops. saying what a tool is not for did more work than i expected.

the bit that took me a minute: renaming a function changed the models behaviour. in my typescript day job a rename is a no-op. here the name is an instruction, so a tool rename is a prompt change and needs whatever you run on prompt changes (078). if your tool descriptions read like column names, the model is guessing.

picking the right tool and filling its arguments are two separate failures. 111 is the second one.
