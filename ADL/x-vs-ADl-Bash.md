# 3. “Bash for AI” Simple Automation Sample

## Use case: inbox triage + meeting prep assistant

This one should feel like a script.
Simple, useful, automatable, easy to maintain.

This is the “bash for AI” feel:

* trigger
* inspect input
* classify
* take action
* produce output

### What this demonstrates

* simple text-based automation
* AI only where useful
* runs reliably
* easy for internal teams

### Sample behavior file

```md
Skill: morning_exec_brief

Description
Create a morning brief from inbox, calendar, and priority accounts.
This should run every weekday at 7:00 AM.

Trigger
schedule: weekday 07:00 Europe/Berlin

Context
The user is an executive.
The brief should be short and operational.
Focus on:
- urgent emails
- meetings today
- customer or investor signals
- blockers needing response

Steps

Step 1
Call @fetch_today_calendar()!

Step 2
Call @fetch_unread_emails(hours=16)! 

Step 3
Call @fetch_priority_contacts()!

Step 4
Use AI to classify unread emails into:
- urgent reply needed
- informational
- can wait
- delegate

Step 5
For urgent emails, extract:
- sender
- topic
- requested action
- implied deadline

Step 6
For today's meetings, extract:
- time
- participants
- purpose
- preparation needed

Step 7
If an email is from a priority contact, mark it as priority even if not urgent.

Step 8
Generate output in this format:

Morning Brief

1. Today’s Meetings
- 09:00 – HRC pilot scope review
  Need: pricing decision and architecture summary
- 14:00 – investor follow-up
  Need: latest pipeline and traction note

2. Urgent Emails
- Battery Ventures: waiting for response on update
- Customer Ops lead: asks for revised scope by noon

3. Priority Signals
- One message from Swisscom contact
- One message from legal on contract language

4. Recommended First Actions
- Reply to Battery Ventures
- Send revised scope to customer
- Review 09:00 meeting prep

Step 9
Call @post_to_slack(channel="exec-brief")!
Call @email_digest()!
```

---

### Why this one matters

This is where your “bash for AI” framing becomes obvious.

It feels like:

```bash
fetch-calendar
fetch-emails
classify
summarize
post
```

But with AI used inside the script for the fuzzy parts.

### Even more “bash-like” variant

You could show an even tighter syntax:

```md
job: morning_exec_brief
schedule: weekday 07:00 Europe/Berlin

run:
  - calendar = @fetch_today_calendar()
  - emails = @fetch_unread_emails(hours=16)
  - priority = @fetch_priority_contacts()
  - triage = ai.classify(emails, ["urgent", "info", "wait", "delegate"])
  - prep = ai.extract_meeting_prep(calendar)
  - brief = ai.compose_exec_brief(calendar, triage, priority, prep)
  - @post_to_slack(channel="exec-brief", body=brief)
  - @email_digest(body=brief)
```

That instantly communicates:

> This is shell scripting for AI-powered business automation.

---

# How to present these three together

Use this progression:

## 1. Complex Voice Agent

Shows **reliable real-time interaction**

* bounded
* safe
* no loops
* business logic enforced

## 2. Automation Bot

Shows **policy-driven business action**

* retention
* cancellation
* confirmations
* backend actions

## 3. Bash for AI

Shows **simple internal automation scripting**

* scheduled jobs
* email triage
* prep flows
* lightweight but powerful

---

# waht these samples prove

These examples show that structured AI programs can cover:

* **voice**
* **chat**
* **bots**
* **internal automation**

using the same mental model:

```text
Behavior file
→ Execution runtime
→ AI + tools
```

---

# Pitch line 



> This is not prompt engineering and not workflow spaghetti.
> It is a structured behavior file that lets businesses build reliable AI automations across voice, chat, and internal ops.

---
