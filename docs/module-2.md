# 🛠️ Module 2 — Build Your Own

You've built one automation. Now build yours.

You have 15 minutes. Pick an idea, describe it to your AI tool, and see how far you get. A working prompt — even if the script isn't finished — counts as progress.

> **💡 Remember:** You haven't "failed" if it's not done. The goal is to build intuition — and you have the pattern now.

---

## Step 1 — Pick an Idea

Not sure what to build? Ask your AI tool:

> *"I just learned to write Google Apps Script with Clasp. Give me 5 ideas for automations I could build in 10 minutes that would save time in my work. I use Google Sheets, Slides, and Docs regularly."*

Or choose from these starter ideas:

### 🗂️ Spreadsheet Automations
- **Data classifier** — Go through a list of items in a sheet and add a label or category to each row
- **Duplicate finder** — Highlight rows where a key column value appears more than once
- **Summary email** — Read a sheet and send yourself a summary of key stats

### 📝 Document Automations
- **Doc from template** — Fill in a Google Doc template with data from a spreadsheet row
- **Meeting notes formatter** — Take a raw notes doc and add headings and bullet structure

### 📊 Slides Automations
- **Status deck** — Generate a slide per project from a tracker sheet (same pattern as Module 1, your own data)
- **Quote card generator** — Create one slide per quote from a spreadsheet, formatted as a pull quote

### 🔔 Trigger-Based Automations
- **Daily digest** — Set up a time-based trigger that runs a script each morning and logs a summary
- **New row notifier** — Watch a sheet for new entries and log them to a separate summary sheet

---

## Step 2 — Describe It to Your AI Tool

Give your AI tool a clear, specific prompt about inputs and outputs.

> **Prompt template:**
> *"Write a Google Apps Script function called `[name]` that [does what]. It should read from [source] and [produce output/take action]. Use Clasp-compatible code."*

Don't overthink it — just start. You can always refine.

---

## Step 3 — Push and Run It

```bash
clasp push
```

Then open the script editor (`clasp open`), select your function, click **▶ Run**, and see what happens.

If it errors, paste the error message into your AI tool and ask it to fix it. Error → fix → push → run is the loop.

> **⚠️ Permissions reminder:** If your script accesses a new Google service (Docs, Gmail, etc.) you haven't used before, you'll see another permissions prompt. Review what's being requested and click **Allow** to proceed.

---

## Step 4 — Share in Show & Tell

You'll have a chance to share:

- **What you tried to build** — one sentence
- **How far you got** — did it run? Did it do the thing?
- **What you'd do next** if you had another 15 minutes
