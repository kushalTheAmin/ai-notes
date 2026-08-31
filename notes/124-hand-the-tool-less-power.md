# 124: hand the tool less power

builds on: [123](./123-injection-grows-hands.md), [111](./111-the-arguments-cant-come-out-malformed.md), [046](./046-system-vs-user.md)
arc: agents you can trust (3 of 17), ~2 min

123 ended on keeping the dangerous thing out of reach of an instruction the model followed. the cheapest version of that is to give the tool less to work with, before the run starts.

```
# wide. the limit lives in the prompt:
#   "only email the customer on the current order"
def email_customer(customer_id, body):
    send(lookup(customer_id).email, body)

# capped. same tool, the limit lives in the code:
TEMPLATES = ["order_shipped", "order_delayed", "refund_sent"]

def email_customer(customer_id, template):
    if customer_id != run.order.customer_id:
        return "error: not the customer on this order"
    if template not in TEMPLATES:
        return "error: no such template"
    send(lookup(customer_id).email, render(template))
```

both versions offer the model email_customer. the top one puts the rule in the system message, and 046 already said what that buys you, priority over the user turn, not enforcement. its still text. the bottom one doesnt care what the model was argued into, a wrong id hits a return before send ever runs. 111 stopped right about here, on an id thats perfectly well formed and still the wrong customer, which no schema can catch. that check can, it knows which order this run is about.

the template swap is the bit i underrated. 123s injected call was email_customer(88120, "verify your order at <link>"). against the capped version theres no body argument at all, so the link has nowhere to ride. the field the attacker needs doesnt exist.

both those returns are strings, so 113 still applies, the model reads "error: no such template" next round and tries something else. it just cant try anything off the list.

110 said the tool description is instructions to the model. the function body isnt instructions to anyone, it runs or it refuses. you already do this with a deploy key thats scoped to one bucket. took me a minute to see the model as just another caller getting an account.
