# 💻 Module 1 — Build a Slide Deck Generator

In this module, you'll build a Google Apps Script that reads employee data from a spreadsheet and automatically creates a Google Slides presentation — one slide per person.

Your AI tool will do the heavy lifting. Describe what you want, and let it write the code for you.

> **⏱ Time:** ~35 minutes (with AI assistance)

---

## What You're Building

A script that:
1. Reads names, roles, and teams from a roster spreadsheet
2. Creates a brand-new Google Slides presentation
3. Adds one slide per person with their info
4. Gives you a link to the finished deck

This is a simplified version of the automation that Martin's team uses to generate their monthly all-hands deck.

### Learning Outcomes

By the end of this module, participants will be able to:

- **Set up a Clasp project** — Scaffold, push, and run an Apps Script project from the command line.
- **Read from Google Sheets** — Pull structured data from a spreadsheet using the Sheets API.
- **Generate Google Slides** — Create a presentation and populate slides programmatically.
- **Use an AI assistant to write Apps Script** — Describe intent in plain English and iterate on generated code.
- **Identify automation opportunities** — Recognize repetitive Workspace tasks that Clasp + Apps Script can eliminate.

---

## Step 0 — Copy the Roster Spreadsheet

Your workshop facilitator will share a link to a Google Sheets roster. Open the link and make your own copy:

**File → Make a copy**

This gives you your own version of the spreadsheet to work with. Keep the tab open — you'll need the spreadsheet URL in a later step.

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

Your script needs permission to read Google Sheets and create Slides. Ask your AI tool to update the project manifest (`appsscript.json`) with the correct OAuth scopes.

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
    "https://www.googleapis.com/auth/presentations"
  ]
}
```

> **⚠️ Heads up — `spreadsheets.readonly` won't work here.** Even though we're only reading data, `SpreadsheetApp.openById()` requires the full `spreadsheets` scope at runtime. The `readonly` variant only works for container-bound scripts (where the sheet is the script's parent file). Also note: you don't need the `drive` scope — `SlidesApp.create()` works with just `presentations`.
</details>

---

## Step 3 — Read Data from the Roster

Create a function that reads the "Team Roster" sheet from **your copy** of the spreadsheet (from Step 0) and returns an array of objects — one per person — with their Name, Team, Manager, Email, and Start Date.

Grab your spreadsheet ID from the URL — it's the long string between `/d/` and `/edit`:

```
https://docs.google.com/spreadsheets/d/YOUR_SPREADSHEET_ID_HERE/edit
```

Ask your AI to write this function. Give it your spreadsheet URL so it can extract the ID. Then push and run it to make sure it reads the data correctly.

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
  var SPREADSHEET_ID = 'YOUR_SPREADSHEET_ID_HERE'; // from your copy's URL
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

Then open the script editor (`clasp open`), select `getRosterData` from the function dropdown, click **▶ Run**, and check the **Execution log** panel to confirm it returned a list of names.
</details>

---

## Step 4 — Create the Slides Presentation

Now for the fun part. Ask your AI tool to write a function that:
1. Calls your roster function to get the data
2. Creates a brand-new Google Slides presentation
3. Sets up a title slide
4. Adds one slide per person showing their Name, Team, and Manager
5. Logs the URL of the finished presentation so you can open it

<details>
<summary>💡 Hint: Sample prompt</summary>

> *"Write an Apps Script function called `createDeck` that: (1) calls `getRosterData()`, (2) creates a new Google Slides presentation called 'Team Roster Deck', (3) adds a title slide with the text 'Team Roster', and (4) adds one slide per person showing their Name, Team, and Manager. Log the URL of the finished presentation."*

</details>

<details>
<summary>📝 Reference implementation</summary>

```javascript
/**
 * Create a slide deck from the roster data.
 */
function createDeck() {
  var roster = getRosterData();
  Logger.log('Found ' + roster.length + ' people in the roster.');

  // Create a new presentation
  var pres = SlidesApp.create('Team Roster Deck');
  Logger.log('Created presentation: ' + pres.getUrl());

  // The first slide is auto-created — use it as the title slide
  var titleSlide = pres.getSlides()[0];

  // Set the title text
  titleSlide.getPlaceholder(SlidesApp.PlaceholderType.TITLE)
    .asShape().getText().setText('Team Roster');
  titleSlide.getPlaceholder(SlidesApp.PlaceholderType.SUBTITLE)
    .asShape().getText().setText('Generated on ' + new Date().toLocaleDateString());

  // Add one slide per person
  roster.forEach(function(person) {
    var slide = pres.appendSlide(SlidesApp.PredefinedLayout.TITLE_AND_BODY);

    // Set the person's name as the slide title
    slide.getPlaceholder(SlidesApp.PlaceholderType.TITLE)
      .asShape().getText().setText(person['Name']);

    // Build the body text
    var body = '';
    body += '🏢 Team: ' + person['Team'] + '\n';
    body += '👤 Manager: ' + person['Manager'] + '\n';
    body += '📧 Email: ' + person['Email'];

    slide.getPlaceholder(SlidesApp.PlaceholderType.BODY)
      .asShape().getText().setText(body);
  });

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

Open the URL — you should see a slide deck with a title slide and one slide per person from the roster. 🎉

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

### 🖼️ Custom Layout
Instead of using the default title-and-body layout, create slides with the name as a large centered title and the details in a smaller text box below.

---

## What You Just Did

You built a real automation that:

- ✅ Reads live data from a Google Sheet
- ✅ Creates a Google Slides presentation from scratch
- ✅ Generates one slide per person — no copy-paste needed
- ✅ Runs in seconds instead of hours

This is the same pattern behind Martin's monthly all-hands deck generator, event programs, onboarding decks, and dozens of other Workspace automations.

> **🚀 What's next?** Think about what repetitive Workspace tasks you do every week. Chances are, an Apps Script + AI assistant can automate it.
