
# iMessage Auto-Responder Setup Guide

## Prerequisites

### Step 1: macOS Requirements

You must be on macOS with the Messages.app signed in to iMessage.

### Step 2: Install imsg Tool

Install the imsg command-line tool by running:

```bash
brew install steipete/tap/imsg
```

### Step 3: Grant Permissions

You must grant Full Disk Access to your Terminal or iTerm application:

* Navigate to **System Settings → Privacy & Security → Full Disk Access**
* Add your Terminal/iTerm application
* You will also need to approve the Messages automation permission (macOS will prompt on first use)

---

## Installation

### Step 4: Get Gemini API Key

Get your free Gemini API key from:
[https://aistudio.google.com/apikey](https://aistudio.google.com/apikey)

### Step 5: Download the Skill

Install the skill from:
[https://clawhub.ai/Koba42Corp/autoresponder](https://clawhub.ai/Koba42Corp/autoresponder)

### Step 6: Extract Files

Extract the downloaded skill into:

```bash
/Users/[your user]/.openclaw/workspace/skills
```

#### Step 6a: Make sure to rename the folder to autoresponder

---

## Configuration

### Step 7: Set Up Gemini API Key

Add your Gemini API key to .zshrc:

```bash
echo 'export GEMINI_API_KEY="YOUR_KEY_HERE"' >> ~/.zshrc
source ~/.zshrc
```

Verify installation by checking these directories exist:

```
~/clawd
~/.openclaw
~/.openclaw/workspace/skills/autoresponder
```

---

### Step 7a: Update the watcher.js file

* Update generateResponse() to use GEMINI AI
* Update sendMessage() method to support both iMessage (iPhones) and SMS (non-iPhones)
* Add const { OpenAI } = require('openai'); at the top

Shortcut: Copy and paste the watcher.js file from this GitHub repo to replace your existing one.

---

### Step 7b: Install dependencies

```bash
cd ~/.openclaw/workspace/skills/autoresponder/scripts
npm install openai
```

---

### Step 7c: Make the launcher executable

```bash
chmod +x ~/.openclaw/workspace/skills/autoresponder/scripts/launcher.sh
```

---

## Running the Auto-Responder

### Step 8: Initial Startup

Start up Clawdbot and verify it's working properly. If you encounter any permission errors from Telegram, we'll troubleshoot them.

### Step 9: Stop Existing Gateway

```bash
openclaw gateway stop
```

### Step 10: Start Gateway in Verbose Mode

Important: Run this from the same terminal where you installed imsg:

```bash
openclaw gateway --verbose
```

---

### Step 10a: Start Auto-Responder

In Telegram, start the auto-responder:

```
/autorespond restart
```

### Step 11: Check Status

In Telegram, verify the auto-responder is running:

```
/autorespond status
```

### Step 12: Add Contacts

Add contacts to the watchlist using:

```
/autorespond_add +15551234567 "Best Friend" "Reply with sarcastic humor"
```

Example prompts:

```
"Reply casually like we're close friends"
"Be professional and brief"
"Reply affectionately, use 'love' and 'baby' occasionally"
```

---

You're all set! The auto-responder will now monitor and reply to messages from your added contacts.

---

## Troubleshooting

Permission errors: Make sure you ran `openclaw gateway --verbose` from the terminal where you installed imsg

Not responding: Check logs at

```
~/clawd/logs/imsg-autoresponder.log
```

API errors: Verify your Gemini API key with:

```bash
echo $GEMINI_API_KEY
```
