# ⚙️ Prerequisites

Complete these steps **before the workshop** so you're ready to code from minute one. Total time: ~10 minutes.

---

## 1. Install Your AI Developer Tool

This is your primary tool for the workshop. You'll use it to write code, run commands, and debug — all through natural language prompts. Your workshop organizer will tell you which tool to install.

Once installed, open it and ask it to tell you a joke — just to make sure it's working correctly.

> **Need help?** Ask the workshop organizer if you have any difficulty getting your AI tool set up.

---

## 2. Check if You Have Node.js

You don't need to open a terminal yourself. Just ask your AI tool:

> **Prompt to try:** *"Do I have Node.js installed? I need at least version 18."*

Your AI tool will check for you and tell you the result. If you already have Node.js v18+, **skip to Step 3**.

### If You Need to Install Node.js

Ask your AI tool:

> *"Please install Node.js LTS for me"*

Or install manually:

**macOS:**
```bash
# Download the installer from https://nodejs.org (LTS version)
# Or install via Homebrew:
brew install node
```

**Windows:**
```powershell
# Download the installer from https://nodejs.org (LTS version)
# Or install via winget:
winget install OpenJS.NodeJS.LTS
```

---

## 3. Install Clasp

[Clasp](https://github.com/google/clasp) (Command Line Apps Script Projects) lets you develop Google Apps Script projects locally in your editor instead of the browser-based script editor.

Ask your AI tool:

> *"Install clasp globally with npm: `npm install -g @google/clasp`"*

Or run it yourself in a terminal:

```bash
npm install -g @google/clasp
```

---

## 4. Enable the Apps Script API

1. Go to [script.google.com/home/usersettings](https://script.google.com/home/usersettings)
2. Turn **ON** the "Google Apps Script API"

> **⚠️ Important:** Without this step, `clasp push` and `clasp pull` will fail with a permissions error.

---

## 5. Log in to Clasp

Ask your AI tool:

> *"Run `clasp login` for me"*

Or run it yourself in a terminal:

```bash
clasp login
```

This opens a browser window to authenticate with your Google account. Once complete, Clasp stores credentials locally.

> **⚠️ Permissions prompt:** After signing in, Google will show a screen listing the permissions clasp is requesting — including access to your Drive files, Apps Script projects, deployments, and cloud services. **Click "Allow"** to proceed. These permissions are required for clasp to push and pull scripts on your behalf.

> **💡 Tip:** If you're using a corporate Google Workspace account, make sure your admin hasn't disabled Apps Script API access. If `clasp login` fails, try with a personal Google account first to verify your setup works.

---

## 6. Verify Everything Works

Ask your AI tool one final check:

> *"Verify my setup: check that I have Node.js v18+, clasp is installed, and I'm logged in to clasp."*

Or run these commands yourself:

```bash
node --version        # Should show v18.x or higher
clasp --version       # Should show 3.x
clasp login --status  # Should show "You are logged in as <your-email>"
```

If all three pass, you're ready for the workshop. 🎉

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| `clasp: command not found` | Run `npm install -g @google/clasp` again, or check that your npm global bin is in your `PATH` |
| `clasp login` opens browser but fails | Try a different browser, or use `clasp login --no-localhost` |
| Apps Script API error | Make sure you toggled it ON at [script.google.com/home/usersettings](https://script.google.com/home/usersettings) |
| Corporate account restrictions | Ask your Google Workspace admin about Apps Script API access, or use a personal account for the workshop |
| `npm` permission errors (macOS) | Use `sudo npm install -g @google/clasp` or fix npm permissions with `npm config set prefix ~/.npm-global` |

> **💡 Still stuck?** Ask your AI tool to help debug — paste the error message into the chat and it will walk you through the fix. If you're unsuccessful, ask your workshop organizers to help.
