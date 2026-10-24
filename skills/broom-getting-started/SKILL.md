---
name: broom-getting-started
description: "First-run setup for Broom. Use when the user installs Broom, wants an inbox cleaned, or asks to configure, start, or change which Gmail inboxes are cleaned, the schedule, protected senders, or coupon handling. Asks one question at a time, saves the answers to memory, and creates a routine that runs junk-mail-check."
---

# Broom getting started

Set up Broom once, then keep the saved settings current. Broom cleans Gmail with the user's existing Gmail connector. It has no mail server of its own.

Ask one question at a time. Wait for the answer before the next question. Do not paste the whole interview in one message.

Use the assistant name the user chooses. Until they choose one, say Broom.

## Before the questions

Confirm the Gmail plugin is the connector you will use. If it is not installed or not signed in, say so and help the user connect it. Do not invent another mail integration and do not ask for a password or an app password.

If Broom settings are already in memory, read them back in one short summary and ask what they want to change. Skip questions they are not changing. Then save, update the routine, and stop.

## Questions

Ask these in order. One message, one question.

1. Inboxes. Ask which Gmail inboxes to clean. For each inbox, the user connects it with the Gmail plugin, gives it a nickname, and says whether it is a business inbox. On a business inbox, only obvious spam is trashed: obvious marketing and obvious spam, and nothing that is uncertain. Accept one inbox or several. If a named inbox is not connected yet, stop and connect that account before the next question. Nicknames are how later runs refer to the inbox.

2. Assistant name. Ask what to call the assistant. If they have no preference, use Broom.

3. Schedule. Ask how often to clean, during which hours, and in which time zone. Offer the default: hourly from about 7:30 AM to 9:30 PM. If they do not name a time zone, use the time zone in the Bot's settings. Repeat the schedule back in plain language so the hours and zone are obvious.

4. Senders. Ask which senders to never trash, and which senders to always trash. Either list may be empty. A sender may be a display name, a domain, or an address the user types. Do not invent senders. Protected categories in `junk-mail-check` still win over an always-trash sender.

5. Coupons. Ask whether to list coupons, and whether a coupon email is trashed after it is listed. These are two choices. Listing can be on while the email stays in the inbox.

## Save

Read the answers back in one compact list: assistant name, each inbox nickname plus whether it is a business inbox, the interval, the hours, the time zone, never-trash senders, always-trash senders, list coupons, and trash coupon emails. Ask for a correction or a yes.

After they agree, save that list to the assistant's memory as the Broom settings. Also remember that rules change only when the user agrees. Do not put the settings into this plugin's files or into a commit.

Create a recurring routine that runs the `junk-mail-check` skill:

- Own it on this assistant.
- Use the saved interval, hours, and time zone. Say the schedule in plain language, for example hourly from 7:30 AM to 9:30 PM in the saved zone.
- The routine's only mail action is that skill. It trashes matching threads and does not permanently delete, unsubscribe, send, or reply.
- If a Gmail connection is missing, the run reports that failure instead of skipping silently or cleaning a different account.
- If a run inside the window trashes nothing, holds nothing, and has nothing new to flag, it sends no message.
- Show the routine's next run and ask the user to check When to run. Fix the schedule if it does not match what they confirmed.

A new routine waits for its next scheduled time. After the routine exists, offer one first cleanup now. Tell them the first pass looks at the last 7 days of inbox mail, and that they can ask for an older window. Run `junk-mail-check` only if they say yes.

## Learn from what the user does

On later turns, notice when the user trashes a thread Broom left in the inbox, or moves a thread Broom trashed back out of Trash. Treat that as a signal, not as a new rule.

Propose one specific update: add that sender to always-trash, or add that sender to never-trash. Say which inbox and which message prompted it, using the sender and subject only. Apply the change only after they say yes, then update memory and confirm the new list.

Do this when they mention a miss or a rescue, and when a cleanup finds a logged thread back in the inbox or finds that the user trashed something the last run held. Do not propose the same sender twice if they already said no.

If they want to unsubscribe from a sender, ask before any unsubscribe step. Never unsubscribe as part of setup.
