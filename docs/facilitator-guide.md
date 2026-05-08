# 📖 Facilitator Guide

Quick reference for workshop facilitators. Keep this open during the session.

---

## Timing

| Block | Start | Duration | Key Moment |
|-------|-------|----------|------------|
| Icebreaker | 0:00 | 5 min | Get everyone talking — "what would you automate?" |
| Live Demo | 0:05 | 10 min | Martin runs the finished script, shows the generated deck |
| Hands-On Build | 0:15 | 35 min | Breakout rooms open. Participants follow Module 1 |
| Show & Tell | 0:50 | 10 min | 2-3 volunteers share their screen |

> **💡 Buffer:** The hands-on block has 5 minutes of built-in buffer. If the group is fast, encourage stretch goals. If slow, cut Show & Tell to 5 minutes.

---

## Before the Session

- [ ] Share the roster spreadsheet link with all participants (they will each **File → Make a copy**)
- [ ] Confirm all participants completed [Prerequisites](prerequisites.md)
- [ ] Prepare breakout rooms (3-4 people per room, 1 facilitator each)
- [ ] Have the [Module 1](module-1.md) page open for reference
- [ ] Test `clasp create`, `clasp push`, and `clasp run` from your own machine

---

## Breakout Room Setup

- **Ratio:** 1 facilitator per 3-4 participants
- **Format:** Participants follow Module 1 at their own pace, with AI assistance
- **Facilitator role:** Don't lecture — hover, help, unblock. Let the AI tool do the teaching.
- **Check-in at 0:30:** "Has everyone pushed code at least once?"
- **Check-in at 0:40:** "Has everyone generated at least a basic deck?"

---

## Common Issues & Fixes

| Issue | Fix | Time to Fix |
|-------|-----|-------------|
| `clasp: command not found` | `npm install -g @google/clasp` | 1 min |
| `clasp run` says "API not enabled" | Go to [script.google.com/home/usersettings](https://script.google.com/home/usersettings) → toggle ON | 1 min |
| `clasp login` fails silently | Try `clasp login --no-localhost` | 2 min |
| `PERMISSION_DENIED` on spreadsheet | Share the roster spreadsheet with the participant's Google account | 1 min |
| "Cannot read property of null" from placeholder | The slide layout doesn't have the expected placeholder — use `insertTextBox()` instead | 3 min |
| Corporate account blocks Apps Script | Have them use a personal Google account | 2 min |
| Participant is completely stuck | Pair them with a neighbor who's ahead | 0 min |

---

## Stretch Goal Suggestions

If participants finish early, suggest these in order of difficulty:

1. **Add the person's start date** to each slide (easy — just read another column)
2. **Color-code by team** — different background per team (medium — mapping + fill)
3. **Add a "New Joiners" section** — filter by start date (medium — array filtering)
4. **Anniversary summary slide** — find people with start month = current month (harder)
5. **Custom slide layout** — ditch the default placeholders, position elements manually (hardest)

---

## Show & Tell Prompts

Use these to get the conversation going:

- *"What was the first thing you asked your AI tool?"*
- *"Did the AI get anything wrong? How did you fix it?"*
- *"What would you automate next at work?"*
- *"What surprised you about the process?"*

---

## Wrap-Up Talking Points

- **The AI tool is a force multiplier.** You didn't need to know Apps Script syntax — you described what you wanted and iterated.
- **Clasp makes it real.** Working in a local editor with version control is how production automation gets built.
- **Start small.** Pick one repetitive Workspace task and try automating it this week.
- **You're not alone.** Ask your AI tool for help anytime. It doesn't judge, it doesn't get tired, and it's available 24/7.
