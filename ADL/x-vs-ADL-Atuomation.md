
# 2. Automation Bot Sample

## Use case: contract cancellation bot for a telecom / SaaS / utility company

This is perfect because it combines:

* business rules
* tool calls
* compliance language
* retention offer
* cancellation execution
* fallback routing

### What this demonstrates

* reliable business automation
* flexible handling of user intent
* enforced system actions
* better than n8n-style giant branching flows

### Sample behavior file

```md
Skill: cancel_contract

Description
Handle customer requests to cancel a contract.
The assistant should verify identity, understand the reason, attempt a permitted retention offer, and then complete cancellation if requested.

Context
Applies to chat, WhatsApp, and web support.
Do not pressure the customer.
Keep the flow concise and professional.

Steps

Step 1
Acknowledge the cancellation request and ask for the customer ID or registered email.

Step 2
Call @verify_customer()!
If verification_failed
Ask for one more identifier: billing postcode.
Call @verify_customer()!
If still_failed
Transfer to @human_support()!

Step 3
Call @fetch_active_contracts()!

Step 4
If multiple contracts exist, ask which contract the customer wants to cancel.

Step 5
Ask the customer for the main reason for cancellation.

Step 6
Call @classify_cancellation_reason()!

Step 7
<reason = price>
Call @fetch_retention_offer()!
If retention_offer_available
Present the retention offer in one sentence.
Ask: "Would you like to keep the contract with this offer?"
</>

<reason = service_issue>
Ask whether they want technical support before proceeding with cancellation.
</>

<reason = moving_abroad>
Continue without retention attempt.
</>

<else>
Continue.
</>

Step 8
<customer_accepts_offer = yes>
Call @apply_retention_offer()!
You MUST confirm the new price and the effective date.
End.
</>

<else>
Continue to cancellation.
</>

Step 9
Call @check_notice_period()!

Step 10
<notice_period_applies = yes>
Tell the customer the earliest cancellation date.
</>

<else>
Tell the customer the contract can be cancelled immediately.
</>

Step 11
Ask for final confirmation:
"Do you want me to proceed with the cancellation?"

Step 12
<confirmed = yes>
Call @cancel_contract()!
You MUST provide the cancellation reference number.
You MUST state the effective cancellation date.
Call @send_confirmation_email()!
Inform the customer that written confirmation has been emailed.
</>

<confirmed = no>
Say: "No problem. I have not cancelled the contract."
End.
</>

Fallback
If the customer requests exceptions outside policy, route to @retention_specialist().
```

---

### How 

> This is a business automation bot.
> It can follow policy, enforce system actions, and still adapt naturally to customer responses.

### Why 

A business person can change:

* retention logic
* compliance sentence
* cancellation policy branch
* escalation rules

without redrawing a huge visual workflow.

---

