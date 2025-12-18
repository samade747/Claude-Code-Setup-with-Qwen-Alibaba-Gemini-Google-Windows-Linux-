# Claude-Code-Setup-with-Qwen-Alibaba-Gemini-Google-Windows-Linux-
Claude Code Setup with Qwen (Alibaba)  + Gemini (Google)  Windows &amp; Linux — Complete Beginner Guide
# CLOUDE.md
Claude Code Setup with Gemini (Google) + Qwen (Alibaba)
Windows & Linux — Complete Beginner Guide

This document explains, step by step, how to set up Claude Code using:
- Google Gemini models
- Alibaba Qwen models
- Claude Code Router
- Automatic model switching (Gemini + Qwen)

You can use Gemini only, Qwen only, or BOTH together.

![Profile Views](https://komarev.com/ghpvc/?username=samade747&style=flat-square)

![GitHub Followers](https://img.shields.io/github/followers/samade747?label=Followers&style=social)  

![GitHub Stars](https://img.shields.io/github/stars/samade747?label=Stars&style=social)

==================================================
TABLE OF CONTENTS
==================================================
1. What is Claude Code + Router
2. Prerequisites
3. Node.js Version Check
4. Install Claude Code & Router
5. (Optional) Install Qwen CLI
6. Environment Variables (Windows & Linux)
7. Router Configuration (Auto-Switching)
8. Start & Test Claude Code
9. How to Get API Keys / Tokens
10. Common Errors & Fixes
11. Recommended Usage Flow
12. Quick Checklist

==================================================
1. WHAT IS CLAUDE CODE + ROUTER
==================================================

Claude Code is a local AI coding interface.
Claude Code Router allows Claude Code to use:
- Gemini
- Qwen
- (and other providers)

The router decides which model to use automatically.

==================================================
2. PREREQUISITES
==================================================

Required for BOTH Windows & Linux:
- Node.js v18 or higher
- npm (comes with Node.js)
- Internet connection
- Port 3456 must be free

==================================================
3. NODE.JS VERSION CHECK
==================================================

Windows (PowerShell):
node --version

Linux (Terminal):
node --version

If version is below v18:
Download from https://nodejs.org (LTS recommended)

==================================================
4. INSTALL CLAUDE CODE & ROUTER
==================================================

Windows (PowerShell):
npm install -g @anthropic-ai/claude-code @musistudio/claude-code-router

Linux (Terminal):
npm install -g @anthropic-ai/claude-code @musistudio/claude-code-router

Verify installation:
ccr --version
ccr --help

==================================================
5. INSTALL QWEN CLI (OPTIONAL – REQUIRED FOR QWEN)
==================================================

Windows / Linux:
npm install -g @qwen-code/qwen-code@latest

Check:
qwen --version

==================================================
6. ENVIRONMENT VARIABLES (SAFE METHOD)
==================================================

DO NOT hardcode keys unless testing.
Environment variables are recommended.

---------------- WINDOWS (PowerShell) ----------------

Google Gemini API Key:
[System.Environment]::SetEnvironmentVariable(
  'GOOGLE_API_KEY',
  'PASTE_YOUR_GOOGLE_API_KEY_HERE',
  'User'
)

Qwen Access Token:
[System.Environment]::SetEnvironmentVariable(
  'QWEN_API_KEY',
  'PASTE_YOUR_QWEN_ACCESS_TOKEN_HERE',
  'User'
)

Restart PowerShell after setting variables.

---------------- LINUX (bash / zsh) ----------------

Edit ~/.bashrc or ~/.zshrc and add:

export GOOGLE_API_KEY="PASTE_YOUR_GOOGLE_API_KEY_HERE"
export QWEN_API_KEY="PASTE_YOUR_QWEN_ACCESS_TOKEN_HERE"

Reload:
source ~/.bashrc

==================================================
7. ROUTER CONFIGURATION (AUTO-SWITCHING)
==================================================

Config file location:

Windows:
C:\Users\YOUR_USERNAME\.claude-code-router\config.json

Linux:
~/.claude-code-router/config.json

Create folder if missing:

Windows:
mkdir %USERPROFILE%\.claude-code-router

Linux:
mkdir -p ~/.claude-code-router

Paste the following EXACT config.json:

--------------------------------------------------
config.json
--------------------------------------------------

{
  "LOG": true,
  "LOG_LEVEL": "info",
  "HOST": "127.0.0.1",
  "PORT": 3456,
  "API_TIMEOUT_MS": 600000,

  "Providers": [
    {
      "name": "gemini",
      "api_base_url": "https://generativelanguage.googleapis.com/v1beta/models/",
      "api_key": "$GOOGLE_API_KEY",
      "models": [
        "gemini-2.5-flash",
        "gemini-2.0-flash"
      ],
      "transformer": {
        "use": ["gemini"]
      }
    },
    {
      "name": "qwen",
      "api_base_url": "https://portal.qwen.ai/v1/chat/completions",
      "api_key": "$QWEN_API_KEY",
      "models": [
        "qwen3-coder-plus",
        "qwen3-coder-max",
        "qwen3-coder-turbo"
      ]
    }
  ],

  "Router": {
    "default": "gemini,gemini-2.5-flash",
    "background": "qwen,qwen3-coder-plus",
    "think": "qwen,qwen3-coder-plus",
    "longContext": "qwen,qwen3-coder-plus",
    "longContextThreshold": 60000,
    "webSearch": "gemini,gemini-2.5-flash"
  }
}

--------------------------------------------------

AUTO-SWITCH LOGIC:
- Gemini → fast chat, summaries, web search
- Qwen → deep thinking, coding, large repos

==================================================
8. START & TEST CLAUDE CODE
==================================================

Start or restart router:
ccr restart

Expected message:
Service started successfully

Open Claude Code:
ccr code

Type:
hi

If Claude replies → SETUP SUCCESS 🎉

==================================================
9. HOW TO GET API KEYS / TOKENS
==================================================

---------------- GOOGLE GEMINI ----------------
1. Visit https://aistudio.google.com
2. Sign in with Google
3. Create / select project
4. Generate API key
5. Copy key (starts with AIza...)
6. Set GOOGLE_API_KEY

---------------- QWEN ----------------
1. Run:
qwen
2. Browser opens → login
3. Token stored in:
   Windows: C:\Users\YOU\.qwen\oauth_creds.json
   Linux: ~/.qwen/oauth_creds.json
4. Open file and copy access_token
5. Set QWEN_API_KEY

IMPORTANT:
If token errors occur:
- Delete the .qwen folder
- Run qwen again
- Copy new token

==================================================
10. COMMON ERRORS & FIXES
==================================================

ccr command not found:
- Restart terminal
- Reinstall packages
- Check Node version

Router not starting:
- Port 3456 already in use
- Change PORT in config.json

401 / API errors:
- Invalid or expired API key
- Recheck environment variables

Qwen suddenly stops:
- Token refreshed
- Update QWEN_API_KEY again

==================================================
11. RECOMMENDED USAGE FLOW
==================================================

Start work:
ccr restart
ccr code

Use normally:
- "Explain this code" → Gemini
- "Refactor whole repo" → Qwen
- "Think step by step" → Qwen
- "Search docs" → Gemini

You NEVER need to switch models manually.

==================================================
12. QUICK CHECKLIST
==================================================

[ ] node --version shows v18+
[ ] Claude Code installed
[ ] Router installed
[ ] Qwen CLI installed (if using Qwen)
[ ] Environment variables set
[ ] config.json exists
[ ] ccr restart successful
[ ] ccr code responds

==================================================
END OF FILE

![Profile Views](https://komarev.com/ghpvc/?username=samade747&style=flat-square)

![GitHub Followers](https://img.shields.io/github/followers/samade747?label=Followers&style=social)  

![GitHub Stars](https://img.shields.io/github/stars/samade747?label=Stars&style=social)

## 📬 **Let's Connect!**  

🌐 **Portfolio**: [My Portfolio](https://5th-class-assignment-7th-october-my-portfolio-website-v9j2.vercel.app/)  
💼 **LinkedIn**: [Abdul Samad](https://www.linkedin.com/in/samaddeveloper-aiagents-developer/)  
📩 **Email**: [samad.e747@gmail.com](mailto:samad.e747@gmail.com)  
📱 **WhatsApp**: [WhatsApp +923328222026](https://api.whatsapp.com/send/?phone=03328222026&text&type=phone_number&app_absent=0)  






✅ 1️⃣ Claude Fallback Model (Gemini → Qwen → Claude)
🎯 Goal

If:

Gemini fails ❌

Qwen rate-limits ❌

➡️ Claude automatically becomes the fallback


==================================================

Fallback Priority (Best Practice)

{
  "LOG": true,
  "LOG_LEVEL": "info",
  "HOST": "127.0.0.1",
  "PORT": 3456,
  "API_TIMEOUT_MS": 900000,

  "Providers": [
    {
      "name": "gemini",
      "api_base_url": "https://generativelanguage.googleapis.com/v1beta/models/",
      "api_key": "$GOOGLE_API_KEY",
      "models": ["gemini-2.5-flash"],
      "transformer": { "use": ["gemini"] }
    },
    {
      "name": "qwen",
      "api_base_url": "https://portal.qwen.ai/v1/chat/completions",
      "api_key": "$QWEN_API_KEY",
      "models": ["qwen3-coder-plus"]
    },
    {
      "name": "claude",
      "api_key": "$ANTHROPIC_API_KEY",
      "models": ["claude-3-5-sonnet-20241022"]
    }
  ],

  "Router": {
    "default": [
      "gemini,gemini-2.5-flash",
      "claude,claude-3-5-sonnet-20241022"
    ],
    "think": [
      "qwen,qwen3-coder-plus",
      "claude,claude-3-5-sonnet-20241022"
    ],
    "longContext": [
      "qwen,qwen3-coder-plus",
      "claude,claude-3-5-sonnet-20241022"
    ],
    "longContextThreshold": 100000,
    "webSearch": [
      "gemini,gemini-2.5-flash",
      "claude,claude-3-5-sonnet-20241022"
    ]
  }
}


🔐 Add Claude Key (Optional but Recommended)

Windows

[System.Environment]::SetEnvironmentVariable(
  'ANTHROPIC_API_KEY',
  'PASTE_CLAUDE_KEY',
  'User'
)


Linux

export ANTHROPIC_API_KEY="PASTE_CLAUDE_KEY"

✅ 2️⃣ Optimized for Huge Monorepos (100k+ Tokens)
🏗 Best Practices for Large Repos

✔ Increased timeout
✔ Larger context threshold
✔ Qwen primary, Claude backup
✔ Stable long operations

🔧 Key Optimizations Already Applied
"API_TIMEOUT_MS": 900000,
"longContextThreshold": 100000

💡 Usage Tips

Always start with:

ccr restart


Ask Claude Code:

“Scan entire repo and summarize architecture”

Avoid running qwen CLI again (token refresh issue)

✅ 3️⃣ Team Onboarding Version (FOR JUNIORS)
👩‍💻 New Team Member Setup (10 Minutes)
# 1. Install Node.js (v18+)
node --version

# 2. Install tools
npm install -g @anthropic-ai/claude-code @musistudio/claude-code-router

# 3. (Optional) Qwen
npm install -g @qwen-code/qwen-code@latest

# 4. Set environment variables
# (team lead provides keys)

# 5. Start
ccr restart
ccr code

📘 Team Rules

❌ Do NOT commit API keys

❌ Do NOT run qwen unless token expires

✅ Use Claude Code only via ccr code

✅ Restart router if errors appear

✅ 4️⃣ GitHub-Ready README.md

Copy this as README.md in your repo 👇

# Claude Code – Gemini + Qwen + Claude

Production-ready Claude Code setup with:
- Google Gemini
- Alibaba Qwen
- Anthropic Claude (fallback)
- Automatic model routing

## Features
- Auto model switching
- Huge monorepo support
- Safe environment variables
- Windows & Linux support

## Requirements
- Node.js v18+
- npm
- Internet access

## Install
```bash
npm install -g @anthropic-ai/claude-code @musistudio/claude-code-router
npm install -g @qwen-code/qwen-code@latest

Configuration

Place config.json in:

Windows: C:\Users\YOU\.claude-code-router\

Linux: ~/.claude-code-router/

Set environment variables:

GOOGLE_API_KEY

QWEN_API_KEY

ANTHROPIC_API_KEY (optional)

Run
ccr restart
ccr code

Usage

Chat & search → Gemini

Coding & deep reasoning → Qwen

Fallback reliability → Claude

Security

❌ Never commit API keys
✅ Use environment variables

License

MIT


---

# 🎉 YOU NOW HAVE AN ENTERPRISE-GRADE SETUP

✔ Auto-switching  
✔ Multi-provider fallback  
✔ Monorepo optimized  
✔ Team onboarding ready  
✔ GitHub clean & professional  

---

## 🚀 Want the FINAL polish?
I can:
- Create **`.env.example`**
- Add **pre-commit security checks**
- Generate **architecture diagram**
- Tune **cost-optimized routing**

Just say **YES + option number** 💪

![Profile Views](https://komarev.com/ghpvc/?username=samade747&style=flat-square)

![GitHub Followers](https://img.shields.io/github/followers/samade747?label=Followers&style=social)  

![GitHub Stars](https://img.shields.io/github/stars/samade747?label=Stars&style=social)

## 📬 **Let's Connect!**  

🌐 **Portfolio**: [My Portfolio](https://5th-class-assignment-7th-october-my-portfolio-website-v9j2.vercel.app/)  
💼 **LinkedIn**: [Abdul Samad](https://www.linkedin.com/in/samaddeveloper-aiagents-developer/)  
📩 **Email**: [samad.e747@gmail.com](mailto:samad.e747@gmail.com)  
📱 **WhatsApp**: [WhatsApp +923328222026](https://api.whatsapp.com/send/?phone=03328222026&text&type=phone_number&app_absent=0)  



# CLOUDE.md — Windows Beginner Friendly

**Claude Code + Gemini (Google) + Qwen (Alibaba)**

Complete, copy‑and‑paste, Windows-focused guide. Includes: step-by-step Claude Code setup, Gemini and Qwen configuration, multiple fallback options, monorepo optimizations, team onboarding, GitHub README, .env.example, and troubleshooting.

> This single file is written for **Windows (PowerShell)** users. Adapt the few Linux notes if you need to run on macOS/Linux.

---

## Table of Contents

1. Overview
2. Prerequisites (Windows)
3. Quick checks
4. Global installs (Claude Code, Router, Qwen CLI)
5. Environment variables (PowerShell commands)
6. Config file locations and how to create them
7. Example configs
   - Minimal Gemini-only
   - Minimal Qwen-only
   - Combined (Gemini + Qwen)
   - Multi-fallback (Gemini → Qwen → Claude)
   - Monorepo-optimized
8. Qwen login flow & token management
9. Claude (Anthropic) API key notes
10. Start, test, and typical commands
11. Multiple fallback strategies (how to choose)
12. Team onboarding quickstart
13. GitHub-ready README excerpt
14. .env.example and PowerShell helper
15. Troubleshooting (common errors & fixes)
16. Quick checklist
17. Next steps & optional extras

---

## 1) Overview

This document helps you run Claude Code locally on Windows and connect it to multiple model providers. It focuses on a safe, beginner-friendly setup that uses environment variables (no secrets in files) and sets up multiple fallbacks so your workflow keeps working when a provider is down or rate-limited.

Supported providers in the file:
- Google Gemini (via API key)
- Alibaba Qwen (via Qwen CLI OAuth token)
- Anthropic Claude (optional fallback via API key)

Router port default: **3456** (changeable in config)

---

## 2) Prerequisites (Windows)

- Windows 10/11
- PowerShell (built-in)
- Node.js v18 or newer (LTS recommended)
- npm (installed with Node)
- Web browser for OAuth (Qwen login)
- Free local port (default 3456)

Install Node.js from:
https://nodejs.org

---

## 3) Quick checks (PowerShell)

Run these and confirm versions:

```powershell
node --version
npm --version
```

`node --version` must start with `v18` or higher.

---

## 4) Global installs (PowerShell)

Open PowerShell (normal user) and run:

```powershell
npm install -g @anthropic-ai/claude-code @musistudio/claude-code-router
# Optional (required for Qwen):
npm install -g @qwen-code/qwen-code@latest
```

Verify:

```powershell
ccr --version
ccr --help
# (if installed) qwen --version
```

If `ccr` or `qwen` is not found, close and reopen PowerShell so your PATH refreshes.

---

## 5) Environment variables (PowerShell)

**Do not paste secrets to public chat.** Use these PowerShell commands to set user-level env vars.

Replace `PASTE_...` with your keys. These persist for the current user.

```powershell
# Google Gemini API key
[System.Environment]::SetEnvironmentVariable('GOOGLE_API_KEY', 'PASTE_YOUR_GOOGLE_API_KEY_HERE', 'User')

# Qwen token (you will extract this during login flow)
[System.Environment]::SetEnvironmentVariable('QWEN_API_KEY', 'PASTE_YOUR_QWEN_TOKEN_HERE', 'User')

# (Optional) Anthropic Claude key for fallback
[System.Environment]::SetEnvironmentVariable('ANTHROPIC_API_KEY', 'PASTE_YOUR_ANTHROPIC_API_KEY_HERE', 'User')
```

After running these, **restart PowerShell** for new terminals to pick up the variables.

---

## 6) Config file locations and how to create them

Router expects a JSON config in:

```
%USERPROFILE%\.claude-code-router\config.json
```

Create folder and open file in Notepad (PowerShell):

```powershell
New-Item -ItemType Directory -Path "$env:USERPROFILE\.claude-code-router" -Force
notepad "$env:USERPROFILE\.claude-code-router\config.json"
```

Paste one of the example configs below and save.

---

## 7) Example configs

> All examples avoid hardcoding secrets by referencing environment variable placeholders like `$GOOGLE_API_KEY`. If your router doesn't expand `$ENVVAR` strings, replace those with actual token strings for testing (not recommended for production).

### A) Minimal Gemini-only

```json
{
  "LOG": true,
  "LOG_LEVEL": "info",
  "HOST": "127.0.0.1",
  "PORT": 3456,
  "API_TIMEOUT_MS": 600000,
  "Providers": [
    {
      "name": "gemini",
      "api_base_url": "https://generativelanguage.googleapis.com/v1beta/models/",
      "api_key": "$GOOGLE_API_KEY",
      "models": ["gemini-2.5-flash", "gemini-2.0-flash"],
      "transformer": { "use": ["gemini"] }
    }
  ],
  "Router": { "default": "gemini,gemini-2.5-flash", "webSearch": "gemini,gemini-2.5-flash" }
}
```

### B) Minimal Qwen-only

```json
{
  "LOG": true,
  "LOG_LEVEL": "info",
  "HOST": "127.0.0.1",
  "PORT": 3456,
  "API_TIMEOUT_MS": 600000,
  "Providers": [
    {
      "name": "qwen",
      "api_base_url": "https://portal.qwen.ai/v1/chat/completions",
      "api_key": "$QWEN_API_KEY",
      "models": ["qwen3-coder-plus", "qwen3-coder-max"]
    }
  ],
  "Router": { "default": "qwen,qwen3-coder-plus" }
}
```

### C) Combined: Gemini + Qwen (safe, env vars)

```json
{
  "LOG": true,
  "LOG_LEVEL": "info",
  "HOST": "127.0.0.1",
  "PORT": 3456,
  "API_TIMEOUT_MS": 600000,
  "Providers": [
    { "name": "gemini", "api_base_url": "https://generativelanguage.googleapis.com/v1beta/models/", "api_key": "$GOOGLE_API_KEY", "models": ["gemini-2.5-flash"] },
    { "name": "qwen", "api_base_url": "https://portal.qwen.ai/v1/chat/completions", "api_key": "$QWEN_API_KEY", "models": ["qwen3-coder-plus"] }
  ],
  "Router": {
    "default": "gemini,gemini-2.5-flash",
    "background": "qwen,qwen3-coder-plus",
    "think": "qwen,qwen3-coder-plus",
    "longContext": "qwen,qwen3-coder-plus",
    "longContextThreshold": 60000,
    "webSearch": "gemini,gemini-2.5-flash"
  }
}
```

### D) Multi-fallback: Gemini → Qwen → Claude (Recommended production-safe)

```json
{
  "LOG": true,
  "LOG_LEVEL": "info",
  "HOST": "127.0.0.1",
  "PORT": 3456,
  "API_TIMEOUT_MS": 900000,
  "Providers": [
    { "name": "gemini", "api_base_url": "https://generativelanguage.googleapis.com/v1beta/models/", "api_key": "$GOOGLE_API_KEY", "models": ["gemini-2.5-flash"] },
    { "name": "qwen", "api_base_url": "https://portal.qwen.ai/v1/chat/completions", "api_key": "$QWEN_API_KEY", "models": ["qwen3-coder-plus"] },
    { "name": "claude", "api_base_url": "https://api.anthropic.com/v1/", "api_key": "$ANTHROPIC_API_KEY", "models": ["claude-3-5-sonnet-20241022"] }
  ],
  "Router": {
    "default": ["gemini,gemini-2.5-flash", "qwen,qwen3-coder-plus", "claude,claude-3-5-sonnet-20241022"],
    "think": ["qwen,qwen3-coder-plus", "claude,claude-3-5-sonnet-20241022"],
    "longContext": ["qwen,qwen3-coder-plus", "claude,claude-3-5-sonnet-20241022"],
    "longContextThreshold": 100000,
    "webSearch": ["gemini,gemini-2.5-flash", "claude,claude-3-5-sonnet-20241022"]
  }
}
```

> Note: If your router implementation does not accept arrays for routing keys, flatten them to comma-separated strings in the order of preference.

### E) Monorepo-optimized (for very large repos)

This config raises timeouts and context threshold for large repo scanning / summarization tasks.

```json
{
  "LOG": true,
  "LOG_LEVEL": "info",
  "HOST": "127.0.0.1",
  "PORT": 3456,
  "API_TIMEOUT_MS": 1200000,
  "Providers": [
    { "name": "qwen", "api_base_url": "https://portal.qwen.ai/v1/chat/completions", "api_key": "$QWEN_API_KEY", "models": ["qwen3-coder-max"] },
    { "name": "claude", "api_base_url": "https://api.anthropic.com/v1/", "api_key": "$ANTHROPIC_API_KEY", "models": ["claude-3-5-sonnet-20241022"] }
  ],
  "Router": {
    "default": "qwen,qwen3-coder-max",
    "think": "qwen,qwen3-coder-max",
    "longContext": "qwen,qwen3-coder-max",
    "longContextThreshold": 200000,
    "API_TIMEOUT_MS": 1200000
  }
}
```

---

## 8) Qwen login flow & token management (Windows)

1. Install Qwen CLI: `npm install -g @qwen-code/qwen-code@latest`
2. Run `qwen` in PowerShell. A browser tab will open prompting you to login.
3. Complete the login flow in your browser. Keep PowerShell open until it finishes.
4. After successful login, Qwen CLI stores credentials in:

```
%USERPROFILE%\.qwen\oauth_creds.json
```

5. Open this JSON and copy the `access_token` value. Use it to set `QWEN_API_KEY` (see Section 5), or paste into `config.json` (not recommended).

6. **If token issues appear**: delete `%USERPROFILE%\.qwen` and repeat login.

**Important**: Do not run `qwen` in random directories or multiple times — it may refresh tokens and cause mismatch between running router and stored token.

---

## 9) Anthropic Claude API key notes (fallback)

If you want Anthropic as a fallback, request an API key from Anthropic (account required). Set it as `ANTHROPIC_API_KEY` using PowerShell as shown in Section 5. Add provider entry in config (see Multi-fallback example).

---

## 10) Start, test, and typical commands (PowerShell)

```powershell
# Restart router (service provided by package)
ccr restart

# Open Claude Code interface
ccr code

# If UI opens, type 'hi' and press Enter to test response.
```

If you see `Service started successfully`, the router is running. If `ccr code` fails to connect, run `ccr restart` again and check logs printed in the same terminal.

---

## 11) Multiple fallback strategies (how to choose)

**Fallback strategies you can choose and why**:

### Strategy A — Gemini primary, Qwen secondary, Claude tertiary
- Use when you want cheap, fast chat + web search as default, deep tasks handled by Qwen, and robust fallback to Claude.
- Router order: `gemini -> qwen -> claude`

### Strategy B — Qwen primary for code, Gemini for chat
- Use when development/coding is primary. Qwen is tuned for coding tasks; Gemini handles light chat.
- Router: `think,longContext` → Qwen; `default,webSearch` → Gemini

### Strategy C — Claude as automatic fallback for all
- Use when Anthropic is your reliable fallback provider. Keep Claude in `default` after Gemini/Qwen.

**How to implement in config**: specify the provider order in your `Router` entries as shown in the Multi-fallback example.

---

## 12) Team onboarding quickstart (for juniors / teammates)

Copy this block into a team onboarding doc or share as a pinned message.

### Steps for teammates (10 minutes)

1. Install Node.js v18+ from nodejs.org
2. Open PowerShell, run:
   ```powershell
   npm install -g @anthropic-ai/claude-code @musistudio/claude-code-router
   npm install -g @qwen-code/qwen-code@latest  # if using Qwen
   ```
3. Set environment variables (team lead provides values or use safe secrets manager):
   ```powershell
   [System.Environment]::SetEnvironmentVariable('GOOGLE_API_KEY', 'PASTE_GOOGLE_KEY', 'User')
   [System.Environment]::SetEnvironmentVariable('QWEN_API_KEY', 'PASTE_QWEN_TOKEN', 'User')
   [System.Environment]::SetEnvironmentVariable('ANTHROPIC_API_KEY', 'PASTE_ANTHROPIC_KEY', 'User')
   ```
4. Create `C:\Users\YOURNAME\.claude-code-router\config.json` and paste the agreed config.
5. Run:
   ```powershell
   ccr restart
   ccr code
   ```
6. Say `hi` to test. If it replies, you’re ready.

### Team rules
- Never commit API keys
- Use `.env` or secret management for production
- If Qwen token breaks, delete `%USERPROFILE%\.qwen` and run `qwen` again (and update `QWEN_API_KEY`)

---

## 13) GitHub-ready README excerpt (copy to your repo)

```markdown
# Claude Code – Gemini + Qwen + Claude (Windows)

This repo holds a recommended config for running Claude Code with multiple providers. It uses environment variables (no secrets checked into source).

## Requirements
- Node.js v18+
- npm
- PowerShell (Windows)

## Setup
1. Install CLI tools:
   ```powershell
   npm install -g @anthropic-ai/claude-code @musistudio/claude-code-router
   npm install -g @qwen-code/qwen-code@latest
   ```
2. Set environment variables for your user (PowerShell):
   ```powershell
   [System.Environment]::SetEnvironmentVariable('GOOGLE_API_KEY','...','User')
   [System.Environment]::SetEnvironmentVariable('QWEN_API_KEY','...','User')
   [System.Environment]::SetEnvironmentVariable('ANTHROPIC_API_KEY','...','User')
   ```
3. Add `config.json` to `C:\Users\YOU\.claude-code-router\`.
4. Start router and run:
   ```powershell
   ccr restart
   ccr code
   ```

## Security
- Never commit API keys.
- Keep `.qwen` folder secret.
```

---

## 14) .env.example and PowerShell helper script

**.env.example** (text to share with team)

```
# .env.example — DO NOT CHECK IN SECRETS
GOOGLE_API_KEY=
QWEN_API_KEY=
ANTHROPIC_API_KEY=
```

**PowerShell helper to load `.env` into user env (for convenience only)**

Create `load-env.ps1` and run `.\load-env.ps1` (do not commit this with secrets):

```powershell
# load-env.ps1 — Loads .env into current user environment (NON-PRODUCTION convenience)
$envPath = Join-Path $PWD ".env"
if (-Not (Test-Path $envPath)) { Write-Error ".env file not found"; exit 1 }
Get-Content $envPath | ForEach-Object {
  if ($_ -match "^\s*#") { return }
  if ($_ -match "^\s*$") { return }
  $pair = $_ -split "=", 2
  $key = $pair[0].Trim()
  $val = if ($pair.Length -ge 2) { $pair[1].Trim() } else { "" }
  [System.Environment]::SetEnvironmentVariable($key, $val, 'User')
  Write-Host "Set user env: $key"
}
Write-Host "Restart PowerShell to use new vars in new shells."
```

---

## 15) Troubleshooting (common errors & fixes)

**`ccr` or `qwen` command not found**
- Close & reopen PowerShell. Ensure npm global bin directory is in PATH.
- `npm bin -g` shows global bin location.

**Router doesn't start / port 3456 busy**
- Check what uses port: `netstat -ano | findstr 3456`
- Kill PID if necessary: `taskkill /PID <pid> /F` or change `PORT` in config.

**API key errors (401/403)**
- Re-check tokens. For Qwen, ensure `oauth_creds.json` contains the token you put in `QWEN_API_KEY`.

**Qwen token rotates (login done again)**
- Delete: `%USERPROFILE%\.qwen` then re-run `qwen` and copy new token to `QWEN_API_KEY`.

**`Service started successfully` not appearing**
- Look at the terminal where you ran `ccr restart` for errors; set `LOG_LEVEL` to `debug` in config for more info.

**Claude Code loads UI but does not respond**
- Check router logs in terminal and ensure providers show healthy connections.

---

## 16) Quick checklist (Windows copy/paste)

```powershell
# Check Node
node --version
# Install tools
npm install -g @anthropic-ai/claude-code @musistudio/claude-code-router
npm install -g @qwen-code/qwen-code@latest
# Set env placeholders (paste real keys)
[System.Environment]::SetEnvironmentVariable('GOOGLE_API_KEY', 'PASTE_GOOGLE', 'User')
[System.Environment]::SetEnvironmentVariable('QWEN_API_KEY', 'PASTE_QWEN', 'User')
[System.Environment]::SetEnvironmentVariable('ANTHROPIC_API_KEY', 'PASTE_CLAUDE', 'User')
# Create config folder & open file
New-Item -ItemType Directory -Path "$env:USERPROFILE\.claude-code-router" -Force
notepad "$env:USERPROFILE\.claude-code-router\config.json"
# Paste config and save, then:
ccr restart
ccr code
```

---

## 17) Next steps & optional extras

If you want, I can:

- Produce a **single downloadable CLOUDE.md** file (I can place it in the canvas or produce a ZIP). ✅ (I will deliver now if you want)
- Create a **`.env.example` + .gitignore`** and a secure team secrets guide
- Generate a **pre-commit hook** to detect accidental API key leaks
- Provide a **PowerShell script** to install everything automatically (interactive)

---

### End — Windows Beginner Friendly CLOUDE.md

Save this file as `CLOUDE.md` and follow the Windows sections. If you want a separate Linux/macOS version or a downloadable ZIP with config files included, tell me and I will create it.


![Profile Views](https://komarev.com/ghpvc/?username=samade747&style=flat-square)

![GitHub Followers](https://img.shields.io/github/followers/samade747?label=Followers&style=social)  

![GitHub Stars](https://img.shields.io/github/stars/samade747?label=Stars&style=social)

## 📬 **Let's Connect!**  

🌐 **Portfolio**: [My Portfolio](https://5th-class-assignment-7th-october-my-portfolio-website-v9j2.vercel.app/)  
💼 **LinkedIn**: [Abdul Samad](https://www.linkedin.com/in/samaddeveloper-aiagents-developer/)  
📩 **Email**: [samad.e747@gmail.com](mailto:samad.e747@gmail.com)  
📱 **WhatsApp**: [WhatsApp +923328222026](https://api.whatsapp.com/send/?phone=03328222026&text&type=phone_number&app_absent=0)  
