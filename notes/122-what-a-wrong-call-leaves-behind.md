# 122: what a wrong call leaves behind

builds on: [121](./121-the-working-agent-assembled.md), [109](./109-when-the-answer-stops-being-a-suggestion.md)
arc: agents you can trust (1 of 13), ~2 min

121 ended with me telling you to go find the line in your agent that says no. i went looking in mine. theres no such line, and before writing one i had to answer something smaller. which calls even need it. so i listed the toolbox out and asked one question of every row.

| the call | a wrong one leaves behind | can i take it back |
| --- | --- | --- |
| search_docs | nothing, some spent tokens | nothing to take back |
| get_order_by_id, wrong id | one customers order on another ones screen | no |
| issue_refund | money out of the account | yes, a second call reverses it |
| email_customer | a mail somebody already read | no |

that middle column is blast radius, how far a wrong call reaches past my own code and how much of it sticks.

my first cut was read vs write. reads are safe, writes are scary. it held for about a minute, until row two. get_order_by_id changes nothing anywhere, its a read by any definition, and a wrong id still puts one persons order in front of another person. i cant unsee that for them. in my .NET work a GET handing back the wrong users record is an incident, i just never carried that over to tools, and finding a read sitting in the same column as the email genuinely caught me out.

then issue_refund, easily the scariest name on the list, turns out to be the recoverable one. money moved, a second call moves it back.

so sort your toolbox by what a wrong call leaves behind and whether you can take it back. which calls need the line that says no falls out of that column.
