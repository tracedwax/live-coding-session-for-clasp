# 📋 Workshop Flow

A 1-hour session designed for non-engineers who want to automate Google Workspace tasks with Apps Script and AI-assisted development.

---

## Overview

| Block | Duration | Who | What |
|-------|----------|-----|------|
| Icebreaker | 5 min | Everyone | Quick intros — who are you, what do you wish you could automate? |
| Live Demo | 10 min | Martin | Watch the finished automation run end-to-end |
| Hands-On Build | 35 min | Everyone (breakout rooms) | Build the automation yourself with AI assistance |
| Show & Tell | 10 min | Everyone | Share what you built, what worked, what surprised you |

---

## Block 1 — Icebreaker (5 min)

**Goal:** Get everyone comfortable and thinking about automation.

- Quick round of intros (name, team, role)
- Prompt: *"What's one repetitive Google Workspace task you'd love to automate?"*
- Set expectations: no coding experience required — your AI tool does the heavy lifting

---

## Block 2 — Live Demo (10 min)

**Goal:** Show the finished product so participants know what they're building toward.

Martin demonstrates the presentation-creation automation:

1. Open the **roster spreadsheet** — a list of employees with names, roles, and photos
2. Run the Apps Script from the Sheets menu
3. Watch it **automatically generate a Google Slides deck** with one slide per person
4. Show the finished deck — formatted, branded, ready to present

> **💡 Key takeaway for participants:** "This took Martin's team hours of manual copy-paste. The script does it in seconds."

---

## Block 3 — Hands-On Build (35 min)

**Goal:** Participants build the same automation themselves, step by step, using an AI coding assistant.

### Setup (5 min)
- Open your AI tool (Windsurf, Antigravity, Copilot, etc.)
- Clone the starter project with `clasp clone`
- Verify the connection to your Google Sheet

### Build (25 min)
- Participants work in **breakout rooms** (3-4 people per room)
- Each room has a facilitator for troubleshooting
- AI tool guides the implementation — participants prompt their way through:
  - Read data from the roster spreadsheet
  - Create a new Google Slides presentation
  - Generate slides from the roster data
  - Add formatting and layout

### Checkpoint (5 min)
- Facilitators check in: did everyone get a working deck?
- Quick fixes for anyone stuck

> **🎯 Success criteria:** Every participant has a working script that generates at least a basic slide deck from the roster data.

---

## Block 4 — Show & Tell (10 min)

**Goal:** Celebrate wins, share learnings, and spark ideas for what else they could automate.

- 2-3 volunteers share their screen and show their generated deck
- Discussion prompts:
  - *"What was the hardest part?"*
  - *"What would you add or change?"*
  - *"What else in your workflow could use this kind of automation?"*
- Wrap-up: where to go next, how to keep experimenting

---

## Facilitator Notes

- **Breakout room ratio:** Aim for 1 facilitator per 3-4 participants
- **Common failure points:** Clasp auth issues (usually fixed by `clasp login` again), Apps Script API not enabled, corporate account restrictions
- **Backup plan:** If someone can't get Clasp working, they can pair with a neighbor or use the browser-based Apps Script editor as a fallback
- **Time buffer:** The hands-on block has 5 min of buffer built in. If the group is moving fast, let them explore extensions (custom formatting, adding images, etc.)
