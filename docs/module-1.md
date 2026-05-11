# 💻 Module 1 — Build a Slide Deck Generator

In this module, you'll build a Google Apps Script that reads employee data from a spreadsheet and populates a branded Google Slides template — one slide per person, fully formatted.

Your AI tool will do the heavy lifting. Describe what you want, and let it write the code for you.

> **⏱ Time:** ~35 minutes (with AI assistance)

---

## What You're Building

A script that:
1. Reads names, roles, and teams from a roster spreadsheet
2. Copies a branded slide deck template
3. Duplicates the person-template slide for each roster entry and fills in their details
4. Gives you a link to the finished deck — formatted and ready to present

This is a simplified version of the automation that Martin's team uses to generate their monthly all-hands deck.

### Learning Outcomes

By the end of this module, participants will be able to:

- **Set up a Clasp project** — Scaffold, push, and run an Apps Script project from the command line.
- **Read from Google Sheets** — Pull structured data from a spreadsheet using the Sheets API.
- **Generate Google Slides** — Create a presentation and populate slides programmatically.
- **Use an AI assistant to write Apps Script** — Describe intent in plain English and iterate on generated code.
- **Identify automation opportunities** — Recognize repetitive Workspace tasks that Clasp + Apps Script can eliminate.

---

## Step 0 — Get Your Starting Materials

You'll need two things:

### Roster Spreadsheet

Open the roster spreadsheet and make your own copy:

📋 **[Roster Spreadsheet](https://docs.google.com/spreadsheets/d/165d0fwpVxn_xSP0xRyDt9zrVBHEFoGWm_hMmyMUQQSQ/edit?gid=2023017964#gid=2023017964)** → **File → Make a copy**

This gives you your own version of the data to work with. Keep the tab open — you'll need the spreadsheet URL in Step 3.

### Template Presentation

This is the branded Fireside slide deck your script will copy and populate. **Don't** copy this one — your script will make its own copy automatically. Just note the presentation ID for Step 4.

🎨 **[Template Presentation](https://docs.google.com/presentation/d/1EQRvjebRDN5f-oc6ln2jN-WTaLHpHw33mhl9fcvyBLo/edit)**

> **Presentation ID:** `1EQRvjebRDN5f-oc6ln2jN-WTaLHpHw33mhl9fcvyBLo`

---

## Step 1 — Create a New Apps Script Project

Use your AI tool to create a new standalone Apps Script project called "Slide Deck Generator" using Clasp. It should scaffold the project in a new directory and connect it to your Google account.

<details>
<summary>💡 Hint: Sample prompt and expected output</summary>

> *"Create a new Google Apps Script project called 'Slide Deck Generator' using clasp"*

This should create a new directory with two files:
- `.clasp.json` — links your local folder to the Apps Script project
- `appsscript.json` — the project manifest

> **📁 Where to create this:** Before running the commands below, navigate to a folder where you keep your projects. For most participants, a folder inside `Documents` works well. If you're not sure, ask your AI tool: *"Create a `workspace` folder in my Documents and navigate there."* Avoid running this from your Desktop or home directory root.

```bash
mkdir slide-deck-generator
cd slide-deck-generator
clasp create --title "Slide Deck Generator" --type standalone
```
</details>

---

## Step 2 — Add the Right Permissions

Your script needs permission to read Google Sheets, work with Slides, and copy files in Drive. Ask your AI tool to update the project manifest (`appsscript.json`) with the correct OAuth scopes.

<details>
<summary>💡 Hint: The scopes you need</summary>

Your `appsscript.json` should include these scopes:

```json
{
  "timeZone": "America/Los_Angeles",
  "dependencies": {},
  "exceptionLogging": "STACKDRIVER",
  "runtimeVersion": "V8",
  "oauthScopes": [
    "https://www.googleapis.com/auth/spreadsheets",
    "https://www.googleapis.com/auth/presentations",
    "https://www.googleapis.com/auth/drive"
  ]
}
```

> **⚠️ Heads up — `spreadsheets.readonly` won't work here.** Even though we're only reading data, `SpreadsheetApp.openById()` requires the full `spreadsheets` scope at runtime. The `readonly` variant only works for container-bound scripts (where the sheet is the script's parent file). The `drive` scope is needed because your script uses `DriveApp.getFileById().makeCopy()` to copy the template presentation.
</details>

---

## Step 3 — Read Data from the Roster

Create a function that reads the "Team Roster" sheet from **your copy** of the spreadsheet (from Step 0) and returns an array of objects — one per person — with their Name, Team, Manager, Email, and Start Date.

Grab your spreadsheet ID from the URL — it's the long string between `/d/` and `/edit`:

```
https://docs.google.com/spreadsheets/d/YOUR_SPREADSHEET_ID_HERE/edit
```

Ask your AI to write this function. Give it your spreadsheet URL so it can extract the ID. Then push and run it to confirm it reads the data correctly.

> **💡 "Run" means one of two things throughout this guide:** either ask your AI agent to run the CLI command for you, or open the browser editor and click ▶ Run. Both work — pick one and stick with it. Step 5 explains both options in full.

<details>
<summary>💡 Hint: Sample prompt</summary>

> *"Write an Apps Script function called `getRosterData` that reads data from my spreadsheet: `[paste your spreadsheet URL here]`. It should read the 'Team Roster' sheet and return an array of objects with columns Name, Team, Manager, Email, and Start Date."*

</details>

<details>
<summary>📝 Reference implementation</summary>

```javascript
/**
 * Read the Team Roster from the spreadsheet.
 * @returns {Object[]} Array of {name, team, manager, email, startDate}
 */
function getRosterData() {
  var SPREADSHEET_ID = '165d0fwpVxn_xSP0xRyDt9zrVBHEFoGWm_hMmyMUQQSQ'; // from your copy's URL
  var ss = SpreadsheetApp.openById(SPREADSHEET_ID);
  var sheet = ss.getSheetByName('Team Roster');
  var data = sheet.getDataRange().getValues();

  var headers = data[0];
  var roster = [];
  for (var i = 1; i < data.length; i++) {
    var entry = {};
    for (var j = 0; j < headers.length; j++) {
      entry[headers[j]] = data[i][j];
    }
    roster.push(entry);
  }
  return roster;
}
```

**Test it:**

```bash
clasp push
```

**Option A — agent CLI:** Ask your AI tool: *"Run the `getRosterData` function"*. It will call `clasp run` and show the output in the terminal.

**Option B — browser editor:** Run `clasp open`, select `getRosterData` from the function dropdown, click **▶ Run**, and check the **Execution log** panel at the bottom.

Either way, confirm the output shows a list of names from your roster.
</details>

---

## Step 4 — Populate the Template Deck

Now for the fun part. Ask your AI tool to write a function that:
1. Calls your roster function to get the data
2. **Copies** the branded template presentation (using `DriveApp.getFileById().makeCopy()`)
3. Opens the copy and finds the example person slide (the "Kermit" slide)
4. For each person in the roster, duplicates that slide and fills in their details
5. Removes the original example slide
6. Logs the URL of the finished deck

<details>
<summary>💡 Hint: Sample prompt</summary>

> *"Write an Apps Script function called `createDeck` that: (1) calls `getRosterData()`, (2) copies the template presentation `[paste your template ID here]` using `DriveApp.getFileById(id).makeCopy('Fireside Deck - ' + new Date().toLocaleDateString())`, (3) opens the copy with `SlidesApp.openById()`, (4) finds the person-template slide (slide index 3 — the one with 'Kermit'), (5) for each person in the roster duplicates that slide and replaces the placeholder text with the person's name and team info, (6) removes the original template slide, and (7) logs the URL."*

</details>

<details>
<summary>📝 Reference implementation</summary>

```javascript
/**
 * Copy the branded template and populate one slide per person.
 */
function createDeck() {
  var TEMPLATE_ID = '1EQRvjebRDN5f-oc6ln2jN-WTaLHpHw33mhl9fcvyBLo'; // from the template presentation URL
  var roster = getRosterData();
  Logger.log('Found ' + roster.length + ' people in the roster.');

  // Copy the template presentation
  var copyFile = DriveApp.getFileById(TEMPLATE_ID)
    .makeCopy('Fireside Deck - ' + new Date().toLocaleDateString());
  var pres = SlidesApp.openById(copyFile.getId());
  Logger.log('Created copy: ' + pres.getUrl());

  // The person-template slide is at index 3 (the "Kermit" example)
  var templateSlide = pres.getSlides()[3];

  // Create one slide per person by duplicating the template
  roster.forEach(function(person) {
    var newSlide = templateSlide.duplicate();

    // Replace placeholder text on all shapes in the slide
    newSlide.getShapes().forEach(function(shape) {
      shape.getText().replaceAllText('Kermit the Frog', person['Name']);
      shape.getText().replaceAllText(
        'Kermit is joining the leapfrog team',
        person['Name'] + ' is joining the ' + person['Team'] + ' team'
      );
      shape.getText().replaceAllText(
        'Before Kermit joined our team he was running a show with his friends',
        'Manager: ' + person['Manager']
      );
      shape.getText().replaceAllText(
        'Fun Fact: Kermit likes waving his arms really fast and drinking tea. Doing both at the same time is not recommended.',
        'Email: ' + person['Email']
      );
    });
  });

  // Remove the original template slide (Kermit)
  templateSlide.remove();

  Logger.log('Done! ' + roster.length + ' slides created.');
  Logger.log('Open your deck: ' + pres.getUrl());
}
```
</details>

---

## Step 5 — Push and Run

Push your code to Google, then run it. There are two ways — use whichever feels most natural.

### Option A — Let your IDE + AI agent run it (recommended)

After pushing, ask your AI tool to run the script for you:

> *"Run the `createDeck` function"*

Your agent will call `clasp run createDeck` on your behalf and show you the output in the terminal. When it finishes, it will log a URL — that's your generated Google Slides deck, already waiting in your Drive.

> **⚠️ First-time only:** `clasp run` requires the Apps Script API to be enabled on your Google account. If the agent hits an error about the API not being enabled, go to [script.google.com/home/usersettings](https://script.google.com/home/usersettings) and toggle it on, then try again.

### Option B — Run it from the browser editor

If you prefer a more hands-on experience, you can run it directly in the [script.google.com](https://script.google.com/home) editor:

```bash
clasp push
clasp open
```

Then in the editor:
- Select `createDeck` from the function dropdown at the top
- Click **▶ Run**
- If a permissions prompt appears, review the requested access and click **Allow**
- Check the **Execution log** panel at the bottom to see the output URL

### Viewing your output

Either way, when the script finishes, your generated slide deck will appear in your **Google Drive**. The Execution log (or terminal output) will include a direct link — click it to open the deck immediately.

Open the URL — you should see a copy of the branded Fireside deck with one slide per person from the roster, fully populated. 🎉

---

## Step 6 — Stretch Goals

Finished early? Ask your AI tool to help you try these enhancements:

### 🎨 Add Formatting
Add a colored background to each slide based on the person's team.

### 📅 Add Start Date
Show each person's start date on their slide, formatted as "Joined: Month Year."

### 🏆 New Joiners Section
Add a section header slide that says "New Joiners" before listing people who started this month.

### 📊 Anniversary Highlights
Add a final slide summarizing work anniversaries — people whose start date month matches the current month.

### 🖼️ Update the Title Slide
Change the title slide text to include the current month and year — so each generated deck is dated automatically.

---

## What You Just Did

You built a real automation that:

- ✅ Reads live data from a Google Sheet
- ✅ Copies a branded slide deck template
- ✅ Populates one slide per person — no copy-paste needed
- ✅ Runs in seconds instead of hours

This is the same pattern behind Martin's monthly all-hands deck generator, event programs, onboarding decks, and dozens of other Workspace automations.

> **🚀 What's next?** Think about what repetitive Workspace tasks you do every week. Chances are, an Apps Script + AI assistant can automate it.
