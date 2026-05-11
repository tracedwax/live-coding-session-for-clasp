# 📋 Workshop Flow

A 1-hour session designed for non-engineers who want to automate Google Workspace tasks with Apps Script and AI-assisted development.

---

## Overview

| Block | Duration | Who | What |
|-------|----------|-----|------|
| Icebreaker | 5 min | Everyone | Quick intros — who are you, what do you wish you could automate? |
| Live Demo | 10 min | Martin | Watch the finished automation run end-to-end |
| Module 1 — Guided Build | 15 min | Everyone (breakout rooms) | Build the roster deck with AI assistance |
| Module 2 — Free Build | 15 min | Everyone (breakout rooms) | Build something of your own with Clasp |
| Show & Tell + ROTI | 10 min | Everyone | Share what you built; rate your return on time invested |

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

## Block 3 — Hands-On Build (30 min)

**Goal:** Participants build two things — first a guided example, then something of their own.

> **💡 Note for participants:** You haven't “failed” if your script isn’t fully working by the end. The goal is to build intuition for how Clasp and Apps Script work together.

### Module 1 — Guided Build (15 min)

Follow [Module 1](module-1.md) to build the roster → slides automation using your AI tool.

- Open your AI tool (Windsurf, Antigravity, Copilot, etc.) and create a new project directory
- Participants work in **breakout rooms** (3–4 people per room)
- Each room has a facilitator for troubleshooting
- AI tool guides the implementation — participants prompt their way through reading roster data and generating a slide deck

> **🎯 Module 1 success:** You’ve run `createDeck` and seen a generated slide deck URL in the Execution log.

### Module 2 — Free Build (15 min)

Follow [Module 2](module-2.md) to build something of your own choosing with Clasp and Google Workspace.

- Stay in breakout rooms — keep collaborating
- Pick an idea from the suggestions or describe your own to your AI tool
- Get as far as you can — a working prompt counts as progress

> **🎯 Module 2 success:** You’ve started something new and can describe what it does (or would do).

---

## Block 4 — Show & Tell + ROTI (10 min)

**Goal:** Celebrate wins, spark ideas, and capture honest feedback.

- 2–3 volunteers share their screen — Module 1 deck, Module 2 attempt, or both
- Discussion prompts:
  - *“What was the hardest part?”*
  - *“What would you add or change?”*
  - *“What else in your workflow could use this kind of automation?”*
- Wrap-up: where to go next, how to keep experimenting

### Return on Time Invested (ROTI)

As we close, ask everyone to answer in chat or aloud:

**Before we wrap up, please drop a quick 0–4 rating for your return on time invested today:**
- **0 – Useless.** Total waste of time; you’d have been better off skipping it.
- **1 – Mostly useless.** Some value, but not enough to justify the time spent.
- **2 – OK.** Enough value to justify showing up, but nothing more.
- **3 – Mostly useful.** Good use of your time; you learned something new or moved work forward.
- **4 – Very useful.** Invaluable; you would have missed something important if you weren’t here.

Then: **What is one thing that would move this session up one full point for you?**

---

## Facilitator Notes

- **Breakout room ratio:** Aim for 1 facilitator per 3–4 participants
- **Common failure points:** Clasp auth issues (usually fixed by `clasp login` again), Apps Script API not enabled at [script.google.com/home/usersettings](https://script.google.com/home/usersettings), corporate account restrictions
- **Backup plan:** If someone can’t get Clasp working, they can pair with a neighbor or use the browser-based Apps Script editor as a fallback
- **Time buffer:** 5 min available across the session. If Module 1 runs fast, give Module 2 the extra time. If Module 1 runs slow, Module 2 becomes a “here’s what you’d do next” discussion rather than a hands-on build.
