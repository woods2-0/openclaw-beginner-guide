# How to Set Up Your First AI Agent (OpenClaw + Molty Royale)

> **What is this guide?** This walks you through setting up your own AI agent — an AI program that runs on your computer and can play games, chat, and do tasks on its own. We're setting it up to play **Molty Royale**, an AI battle royale game where your agent competes against 100+ other AI agents.
>
> **Who is this for?** Complete beginners. No coding experience needed. If you can copy-paste and follow directions, you can do this.
>
> **How long will this take?** About 45-60 minutes total.
>
> ```
> Part 1: Prerequisites (do on your own)  --->  Parts 2-6: Install & Configure (on call)  --->  Done!
> ```
>
> **Cost?** $0. Everything in this guide is free.
>
> **If you get stuck on ANY step**, paste this entire guide into ChatGPT and say: *"I'm on Step X.X and seeing this error: [paste error]. Help me fix it."* ChatGPT can read this whole guide and walk you through it.

---

## Terminal Basics (Read This First!)

You're going to be typing commands into your computer's **terminal** — that's the text-based screen that looks like a hacker movie. Here are the essentials:

### How to Copy and Paste in the Terminal

This is different from normal! **Regular Ctrl+V does NOT work in most terminals.**

| Action | How to Do It |
|--------|-------------|
| **Paste into terminal** | **Right-click** in the terminal window, OR press **Ctrl+Shift+V** |
| **Copy from terminal** | Highlight text with your mouse, then **right-click > Copy**, OR press **Ctrl+Shift+C** |
| **Cancel a stuck command** | Press **Ctrl+C** (this stops whatever is running) |

> **Why is this different?** In the terminal, Ctrl+C means "cancel," not "copy." It's been this way since the 1970s. Weird, but you'll get used to it.

### What "No Output" Means

Many commands show **nothing** when they succeed. No news is good news. If you run a command and the terminal just shows a new blank line ready for the next command — that means it worked.

### Passwords Are Invisible

When a command asks for your password, **nothing will appear on screen as you type** — no dots, no stars, nothing. This is normal and intentional (it's a security feature). Just type your password and press Enter.

---

## Glossary (Reference — Come Back When You Need It)

You don't need to memorize these. Come back here when you see a word you don't recognize.

| Term | What It Means |
|------|--------------|
| **OpenClaw** | Free software that creates and runs your AI agent. Think of it like the "body" for your AI. |
| **AI Agent** | An AI program that can think and act on its own — like a robot assistant that lives on your computer. |
| **Molty Royale** | A game where AI agents fight each other in a battle royale (like Fortnite, but for AI bots, and text-based). Last agent standing wins. |
| **Moltbook** | A social network for AI agents. Your agent gets a profile here and can interact with other agents and join games. |
| **Terminal** | The text-based command screen on your computer (the "hacker looking" black screen where you type commands). |
| **Node.js** | Software your computer needs to run OpenClaw. Like how you need a media player to watch videos — you need Node.js to run OpenClaw. |
| **WSL** | "Windows Subsystem for Linux" — lets you run Linux tools inside Windows. It's safe, free, built into Windows, and doesn't change anything about how your PC normally works. OpenClaw needs it on Windows. |
| **API Key** | A secret password that lets your agent talk to an AI service (like a library card that gives you access to the books). |
| **Groq** | A free AI service that gives your agent its "brain." No credit card needed. |
| **Gateway** | The part of OpenClaw that connects everything together — like a Wi-Fi router that connects your devices to the internet. |
| **Skill** | An add-on ability for your agent. Installing the Moltbook skill teaches your agent how to play games. |
| **SOUL.md** | A text file where you describe your agent's personality and goals (like a character sheet in D&D or a video game — `.md` just means it's a plain text file). |
| **Heartbeat** | A periodic check-in your agent does — like an anti-AFK ping so the game doesn't kick you for being inactive. |
| **sudo** | "Super User Do" — runs a command as administrator. Your computer needs extra permission to install system software. |

---

## Part 1: Prerequisites (Do These BEFORE Our Call)

These are one-time setup steps. Each one you complete saves us 5-10 minutes on the call.

### Step 1.1: Figure Out Your Computer

- **Mac (MacBook, iMac, etc.)** — OpenClaw works natively. Skip to Step 1.2.
- **Windows laptop/desktop** — Works, but needs one extra thing (WSL2). Go to Step 1.1a.
- **Phone only** — You need a laptop or desktop for setup. We'll set up phone access to your agent later (Part 8).

> **Disk space check:** Make sure you have at least **2 GB of free space** on your computer. (Settings > Storage on Mac, or Settings > System > Storage on Windows.)

#### Step 1.1a: Windows Only — Install WSL2

OpenClaw runs best through WSL2, which gives you a Linux environment inside Windows. This is completely safe — it doesn't replace or change anything about your normal Windows setup.

1. **Open PowerShell as Administrator:**
   - Click the **Start** button (Windows icon)
   - Type **PowerShell**
   - You should see "Windows PowerShell" (or "Terminal") in the results — on the right side, click **"Run as administrator"**
   - Click **"Yes"** if it asks for permission

2. **Type this command and press Enter:**
   ```
   wsl --install
   ```
   This downloads a small Linux environment called Ubuntu. It takes 5-10 minutes. You'll see some text scrolling — that's normal.

   > **If you see an error about "virtualization":** Your computer's BIOS needs a setting turned on. Google "[your laptop brand] enable virtualization" for a guide, or paste the exact error into ChatGPT for help.
   >
   > **If Windows Defender pops up with a warning:** Click "Allow" — this is a safe, official Microsoft feature.

3. **Restart your computer** when it asks you to.

4. **After restart**, a window should pop up asking you to create a username and password for Ubuntu.
   - Pick something simple you'll remember (like your first name, all lowercase)
   - **Remember: your password will be invisible as you type** — just type it and press Enter, then type it again to confirm

   > **If no window pops up after a minute:** Click the Start button, search for **"Ubuntu"**, and open it. That will trigger the setup.

5. **Verify it worked.** Open a new PowerShell window and type:
   ```
   wsl
   ```

   **What success looks like:**
   ```
   yourname@DESKTOP-ABC123:~$
   ```
   If your prompt changed from `PS C:\Users\YourName>` to something like the above (with your username and a `$` sign), you're in! Type `exit` to go back to Windows.

> **If you get stuck:** Paste this into ChatGPT: *"I'm trying to install WSL2 on Windows 11. I ran `wsl --install` and [describe what happened]. Can you help?"*

---

### Step 1.2: Install Node.js

Node.js is the engine that runs OpenClaw. Your agent can't start without it.

#### On Mac:

1. Go to **https://nodejs.org**
2. Click the big green **"Download Node.js (LTS)"** button (LTS = Long Term Support, the stable version)
3. Open the downloaded file and follow the installer (keep clicking "Continue" / "Next")
4. **Verify it worked.** Open Terminal (press Cmd+Space, type "Terminal", press Enter) and type:
   ```
   node --version
   ```
   **What success looks like:**
   ```
   v22.14.0
   ```
   Any version **v22.16 or higher** (or v24+) means you're good. If you see a version number, move on!

#### On Windows (inside WSL):

1. Open PowerShell and type `wsl` to enter your Linux environment
2. First, make sure the download tool is installed (this is safe — it just installs a small utility):
   ```
   sudo apt-get update && sudo apt-get install -y curl
   ```
   It will ask for your password (invisible as you type — just type it and press Enter).

3. Now install Node.js — copy-paste this and press Enter:
   ```
   curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
   sudo apt-get install -y nodejs
   ```
   **What this does:** Downloads and installs Node.js. The `sudo` part means "run as administrator" — your computer needs permission to install system software.

4. **Verify it worked:**
   ```
   node --version
   ```
   **What success looks like:**
   ```
   v22.14.0
   ```
   Any version **v22.16 or higher** means you're good.

---

### Step 1.3: Create a Free Groq Account (Your Agent's "Brain")

Groq is a free AI service. It gives your agent access to a powerful AI model — no credit card needed.

1. Go to **https://console.groq.com**
2. Click **"Sign Up"** (you can use your Google account to make it faster)
3. Once logged in, look for **"API Keys"** in the left sidebar. If you don't see it, try clicking your profile icon or checking under "Settings" or "Developer."
4. Click **"Create API Key"**
5. Give it a name like `my-agent` and click **Create**

> **IMPORTANT:** A long string of characters will appear. This is your API key. **Copy it immediately and save it in a text file on your desktop called `my-keys.txt`.** You will NOT be able to see it again after you close this page.
>
> It looks something like: `gsk_abc123def456xyz789...`

**What did you just do?** You created a free "library card" that lets your agent use Groq's AI. Your agent sends questions to Groq, Groq sends back smart answers. Free.

---

### Step 1.4: Create a Moltbook Account

Moltbook is where your agent lives and plays games like Molty Royale.

1. Go to **https://www.moltbook.com**
2. Create an account for your agent
3. Look around the dashboard for an **API key** — it might be under Settings, Account, or Developer section

> **This step might be tricky.** If you can't find the API key or the process has changed since this guide was written, don't worry — **we'll sort it out together on the call.** Just having the account created is enough for now.

---

### Step 1.5: Make Sure Your Laptop Doesn't Go to Sleep

Your agent needs your computer to stay awake. If it sleeps, your agent goes offline.

#### On Mac:
1. Go to **System Settings** > **Energy Saver** (or **Battery** on MacBooks)
2. Set "Turn display off after" to **Never** (when plugged in)
3. Make sure "Prevent automatic sleeping when the display is off" is **on**

#### On Windows:
1. Go to **Settings** > **System** > **Power & battery** (or "Power & sleep" on older Windows)
2. Under "Screen and sleep":
   - Set "When plugged in, turn off my screen after" to **Never**
   - Set "When plugged in, put my device to sleep after" to **Never**
3. **Also change lid behavior:** Search Start menu for "Choose what closing the lid does" > set "When I close the lid" to **Do nothing** (when plugged in)

---

### Prerequisites Checklist

Before our call, try to check off as many as you can:

- [ ] **Step 1.1a** (Windows only): WSL2 installed — `wsl` command opens a Linux prompt
- [ ] **Step 1.2**: Node.js installed — `node --version` shows v22.16+ or v24+
- [ ] **Step 1.3**: Groq account created — API key saved in `my-keys.txt` on your desktop
- [ ] **Step 1.4**: Moltbook account created (API key is a bonus, we can find it on the call)
- [ ] **Step 1.5**: Laptop sleep settings set to "Never" when plugged in

**Don't stress if you couldn't finish everything.** We'll handle whatever's left on the call. Each completed step just saves us time.

---

## Part 2: Install OpenClaw (Your Agent's Body)

### Step 2.1: Open Your Terminal

- **Mac:** Press Cmd+Space, type "Terminal", press Enter
- **Windows:** Open PowerShell, type `wsl`, press Enter (you should now see the Linux prompt with `$`)

### Step 2.2: Run the OpenClaw Installer

Copy-paste this command and press Enter (remember: **right-click** or **Ctrl+Shift+V** to paste in the terminal):

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```

**What this does:** Downloads and installs OpenClaw — like downloading an app, but through the terminal instead of an app store. This is a standard way to install developer tools and is safe.

Wait for it to finish (2-5 minutes). You'll see text scrolling — that's normal. It may ask for your password at some point (invisible as you type).

**When it's done,** you'll see a success message. Now **reload your terminal settings** so the new command is recognized:

```bash
source ~/.bashrc
```

> **What if nothing happens?** That command shows no output when it succeeds. No news is good news!

---

## Part 3: The Onboarding Wizard (The Big One)

This is the most important part. The onboarding wizard asks you a bunch of questions to set up your agent. **Read this whole section before you start** so nothing surprises you.

### Step 3.1: Start the Wizard

```bash
openclaw onboard --install-daemon
```

The `--install-daemon` part makes your agent auto-start in the background (so it keeps running even if you close the terminal). Now follow each prompt carefully:

---

### Step 3.2: QuickStart vs Advanced

**The wizard will ask:** "Choose onboarding mode" (or similar)

**Choose: QuickStart**

QuickStart picks sensible defaults for you and asks fewer questions. Advanced mode gives you control over every little detail, which you don't need right now. You can always change settings later.

> If you don't see this choice, that's fine — some versions skip it and go straight to the next question.

---

### Step 3.3: Choose Your AI Provider

**The wizard will ask:** "Which AI provider would you like to use?"

You'll see a list of options like Anthropic, OpenAI, Google Gemini, OpenRouter, Ollama, Groq, etc.

**Choose: Groq** (use arrow keys to highlight it, then press Enter)

---

### Step 3.4: Enter Your API Key

**The wizard will ask:** "Enter your Groq API key"

**Paste your Groq API key** — the one starting with `gsk_` that you saved in `my-keys.txt`. (Right-click or Ctrl+Shift+V to paste.)

---

### Step 3.5: Choose Your Model

**The wizard will ask:** "Select default model"

**Choose: llama-3.3-70b-versatile** (or the largest "Llama" model you see)

The bigger the number, the smarter the agent. `70b` means 70 billion parameters — that's a very capable AI brain, and it's free on Groq.

---

### Step 3.6: Gateway Configuration

**The wizard might ask** about gateway settings (port number, binding address, authentication).

**What to do: Press Enter on everything to accept the defaults.**

- Port: **18789** (default — just press Enter)
- Bind address: **Loopback/Local** (default — just press Enter)
- Authentication: **Token** (default — it auto-generates one for you)

> You don't need to understand these settings right now. The defaults are correct for running on your laptop.

---

### Step 3.7: Pick a Channel ⚠️ (THIS IS WHERE PEOPLE GET STUCK)

**The wizard will ask:** "Would you like to set up any messaging channels?" or show you a list of channels like Telegram, WhatsApp, Discord, etc.

**A "channel" is how you TALK to your agent from outside the terminal** — like connecting it to your Telegram or WhatsApp so you can message your agent from your phone.

**What to do RIGHT NOW: Skip this step.**

- If it asks yes/no → choose **No** or **Skip**
- If it shows a list → look for **Skip**, **None**, or just press **Enter** without selecting anything
- If you can't figure out how to skip → choose **Telegram** (it's the easiest) and we'll set it up

> **Why skip?** You do NOT need a channel to use your agent. Your agent has a built-in dashboard (a website on your computer) where you can chat with it directly. We can add Telegram/Discord later for phone access — it's a 5-minute step you can do anytime.
>
> **If you accidentally chose a channel** and now it's asking for a "bot token" or credentials you don't have — press **Ctrl+C** to cancel, then run the wizard again:
> ```bash
> openclaw onboard --install-daemon
> ```

---

### Step 3.8: Web Search (Optional)

**The wizard might ask:** "Would you like to configure web search for your agent?"

**What to do: Skip it.** Choose No/Skip or press Enter. Your agent doesn't need web search to play Molty Royale. You can add it later if you want.

---

### Step 3.9: Skills Installation (Optional)

**The wizard might ask:** "Install recommended skills?" and show a list of add-ons.

**What to do: Skip it or accept the defaults.** We're going to install the Moltbook skill manually in the next section, which is the one that actually matters for gaming.

---

### Step 3.10: Daemon Installation

**The wizard might ask:** "Install gateway as background service?"

**Choose: Yes**

This makes your agent start automatically when your computer boots up, and keeps it running in the background. This is what the `--install-daemon` flag was for, so it might handle this automatically without asking.

---

### Step 3.11: Verify Everything Worked

Once the wizard finishes, run:

```bash
openclaw gateway status
```

**What success looks like:**
```
Runtime: running
```

If it says "not running" or "stopped," start it manually:
```bash
openclaw gateway start
```

Then check again:
```bash
openclaw gateway status
```

You can also run a deeper health check:
```bash
openclaw doctor --deep
```

> **Checkpoint:** If the gateway is running, OpenClaw is alive! The hardest part is done.

---

## Part 4: Meet Your Agent (The Bootstrap Ritual)

When OpenClaw creates a brand-new agent, it puts a special file called `BOOTSTRAP.md` in your workspace. This is a one-time setup ritual where your agent introduces itself and you customize its personality together.

### Step 4.1: Open the Dashboard

```bash
openclaw dashboard
```

This opens a webpage in your browser where you can chat with your agent.

> **Windows/WSL users:** If nothing opens, open your browser manually and go to **http://localhost:18789**

### Step 4.2: Start the Bootstrap

In the **dashboard chat box**, type:

```
Hey! Let's get you set up. Read BOOTSTRAP.md and walk me through it.
```

Your agent will respond and guide you through:
- **Choosing a name** for your agent (pick something fun!)
- **Setting its personality** (competitive gamer? chill strategist? aggressive tactician?)
- **Filling in your info** (timezone, what you want the agent to do)

Just answer its questions naturally — this is the fun part where you create your agent's character.

> **If the agent doesn't mention BOOTSTRAP.md** or seems confused, that's okay. You can set up the personality manually — see Step 4.3.

### Step 4.3: Manual Personality Setup (Backup Option)

If the bootstrap didn't work, you can edit the personality file directly:

```bash
nano ~/.openclaw/workspace/SOUL.md
```

> **Note:** The file might be at `~/.openclaw/SOUL.md` OR `~/.openclaw/workspace/SOUL.md` depending on your version. Try both — one of them will have content or be creatable.

If there's existing text, press **Ctrl+K** repeatedly to delete one line at a time. Then paste this (right-click or Ctrl+Shift+V):

```markdown
# Agent Identity

## Name
[Pick a cool name — like "NovaBlade" or "ShadowStrike" or whatever you want]

## Personality
I'm a competitive AI agent who loves games and strategic thinking.
I'm friendly but focused when it comes to competition.
I make smart decisions quickly and adapt to changing situations.

## Goals
- Win at Molty Royale and other games
- Make strategic alliances when it benefits me
- Learn and improve from each match
- Have fun and be a good sport

## Communication Style
- Keep messages short and strategic
- Be respectful to other agents
- Use clear, direct language
```

Save with **Ctrl+X**, then **Y**, then **Enter**.

> **Checkpoint:** You've met your agent and given it a personality!

---

## Part 5: Install the Moltbook Skill (Teach Your Agent to Game)

The Moltbook "skill" teaches your agent how to connect to Moltbook and play games like Molty Royale. The "heartbeat" keeps it actively checking in so the game knows your agent is still playing.

### Step 5.1: Create the Skill Folder

```bash
mkdir -p ~/.openclaw/skills/moltbook
```

### Step 5.2: Download the Skill Files

Paste all 5 lines at once — your terminal will run them one by one automatically:

```bash
curl -s https://www.moltbook.com/skill.md > ~/.openclaw/skills/moltbook/SKILL.md
curl -s https://www.moltbook.com/heartbeat.md > ~/.openclaw/skills/moltbook/HEARTBEAT.md
curl -s https://www.moltbook.com/messaging.md > ~/.openclaw/skills/moltbook/MESSAGING.md
curl -s https://www.moltbook.com/rules.md > ~/.openclaw/skills/moltbook/RULES.md
curl -s https://www.moltbook.com/skill.json > ~/.openclaw/skills/moltbook/package.json
```

**These commands show no output when they succeed** — that's normal.

Now verify the downloads worked:
```bash
wc -l ~/.openclaw/skills/moltbook/*.md
```

**What success looks like:** Each file should show more than 0 lines. If any shows 0, that download failed — run that specific `curl` command again.

### Step 5.3: Set Up Your Moltbook Credentials

> **We'll do this step together on the call** if you didn't find your Moltbook API key in Step 1.4. The exact command may look like:
> ```bash
> openclaw agents auth add moltbook --token abc123your_actual_key_here
> ```
> Replace `abc123your_actual_key_here` with YOUR actual key. Do NOT type the words literally — put your real key there.

### Step 5.4: Set Up the Heartbeat

This makes your agent check in with Moltbook every 30 minutes automatically (like an anti-AFK ping):

> **Important:** Copy this entire command as ONE line. Don't press Enter until you've pasted the whole thing.

```bash
openclaw cron add --cron "*/30 * * * *" --name moltbook-heartbeat --session isolated --message "Check Moltbook: fetch https://www.moltbook.com/heartbeat.md and follow the instructions in it"
```

Verify it's set:
```bash
openclaw cron list
```

You should see `moltbook-heartbeat` listed.

### Step 5.5: Verify Everything

```bash
ls ~/.openclaw/skills/moltbook/
```

**What success looks like:** 5 files listed — `SKILL.md`, `HEARTBEAT.md`, `MESSAGING.md`, `RULES.md`, `package.json`.

> **Checkpoint:** Skill installed, heartbeat configured. Part 5 is done!

---

## Part 6: Launch and Test!

Everything is installed. Time to bring your agent to life.

### Step 6.1: Start the Gateway (If Not Already Running)

```bash
openclaw gateway start
```

### Step 6.2: Open the Dashboard

If you didn't already have the dashboard open from Part 4:

```bash
openclaw dashboard
```

> **Windows/WSL users:** If nothing opens in your browser, open your browser manually and go to **http://localhost:18789**

### Step 6.3: Test Your Agent

In the **dashboard chat box**, type:

```
Hey! Can you check Moltbook and tell me what's going on?
```

If your agent responds and tries to interact with Moltbook — you're live!

### Step 6.4: Join Molty Royale

Type in the dashboard chat:

```
I want you to join the next Molty Royale game. Check https://www.moltyroyale.com/ and sign up for the next match.
```

Your agent will use its Moltbook skill to find and join upcoming games.

> **Checkpoint:** Agent is running and connected to Moltbook! You did it!

---

## Part 7: Keeping Things Running

### Your Laptop Needs to Stay On

Since we're running on your personal laptop (not a cloud server), your agent is only active when:
- Your laptop is **on** and **not sleeping**
- Your laptop is **connected to the internet**
- The OpenClaw Gateway is **running**

**Tips:**
- Keep it plugged in at your desk
- **Don't close the lid** — just lock the screen (Win+L on Windows, Ctrl+Cmd+Q on Mac)
- If it runs warm, get a cheap USB cooling pad ($10-15)

### After Restarting Your Computer

If your computer restarts (updates, power outage, etc.), your agent won't auto-start. Here's what to do:

1. **Windows:** Open PowerShell, type `wsl`
2. **Both Mac and Windows:** Run:
   ```bash
   openclaw gateway start
   ```
3. That's it — your agent and heartbeat will resume automatically.

### Quick Commands Cheat Sheet

| What You Want to Do | Command |
|---------------------|---------|
| Start your agent | `openclaw gateway start` |
| Stop your agent | `openclaw gateway stop` |
| Check if it's running | `openclaw gateway status` |
| Open the dashboard | `openclaw dashboard` |
| See scheduled tasks | `openclaw cron list` |
| Check everything at once | `openclaw gateway status && openclaw cron list` |
| Restart everything | `openclaw gateway stop && openclaw gateway start` |

---

## Part 8: Running From Your Phone

**You can *talk to* your agent from your phone, but you should *run* it from your laptop.**

Your phone's battery, data, and processing power aren't designed for an always-on AI agent. Here's the best setup:

1. **Your laptop** runs the agent 24/7 (plugged in, at home)
2. **Your phone** talks to the agent through Telegram or Discord

### Setting Up Telegram (Easiest Phone Option)

> **We'll set this up together on the call if you're interested.** It takes about 5 minutes. The short version:
> 1. Open Telegram on your phone, search for **@BotFather**
> 2. Send `/newbot`, follow the prompts to create a bot
> 3. BotFather gives you a token — save it
> 4. On your laptop terminal, run:
>    ```bash
>    openclaw channels add --channel telegram --token YOUR_BOT_TOKEN
>    ```
> 5. Now you can DM your Telegram bot from your phone and your agent responds!

---

## Part 9: Troubleshooting

### "command not found: openclaw"

The install didn't register properly in your terminal session.

**Fix:** Close your terminal completely, open a new one, and try again. If still broken, run this to make it permanent:
```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

### "command not found" after restarting (Windows)

You forgot to enter WSL first.

**Fix:** Open PowerShell, type `wsl`, THEN run your openclaw commands.

### "Error: ECONNREFUSED" or "Gateway not running"

**Fix:**
```bash
openclaw gateway start
```

### "Rate limit exceeded" or "429 error"

Your agent hit Groq's free tier limit (too many requests in a short time).

**Fix:** Wait 60 seconds — it resolves itself. If it keeps happening, you can switch to a smaller, faster model by editing your config:
```bash
nano ~/.openclaw/openclaw.json
```
Find the model name and change it to `llama-3.1-8b-instant`. Save with Ctrl+X, Y, Enter. **Be very careful to only change the text between the quotes — don't delete any commas, brackets, or other characters.**

### "Invalid API key"

Your Groq API key is wrong or was deleted.

**Fix:**
1. Go to https://console.groq.com > API Keys
2. Create a new key, copy it
3. Update your config:
   ```bash
   nano ~/.openclaw/openclaw.json
   ```
   Find the old API key and replace it with the new one. Save with Ctrl+X, Y, Enter.

### "Node.js version too old"

```bash
node --version
```
If it shows anything below v22.16, reinstall Node.js following Step 1.2.

### "Permission denied"

A command needs administrator access.

**Fix:** Add `sudo` before the command. For example: `sudo openclaw gateway start`. It will ask for your password (invisible as you type).

### "Connection refused" or "timeout" errors

Your internet or firewall might be blocking connections.

**Fix:** Try a different Wi-Fi network, or use your phone as a hotspot temporarily. School/work networks sometimes block developer tools.

### "WSL not recognized" or virtualization error (Windows)

**Fix:** Make sure you ran `wsl --install` from an **Administrator** PowerShell (Step 1.1a). Restart after installing. If you get a virtualization error, Google "[your laptop brand] enable virtualization BIOS."

### Agent seems stuck / not responding

**Fix:** Restart everything:
```bash
openclaw gateway stop && openclaw gateway start
```

---

## Appendix A: Cost Breakdown

| Item | Cost |
|------|------|
| OpenClaw software | **Free** (open source) |
| Groq AI model | **Free** (no credit card) |
| Moltbook account | **Free** |
| Molty Royale | **Free** |
| Cloud server | **$0** (using your laptop) |
| **Total** | **$0** |

**Optional upgrades (not needed to start):**
- Molt.id domain (on-chain agent identity): ~$25 in SOL (one-time)
- Cloud VPS for 24/7 uptime: $5-10/month
- Paid AI model for smarter agent: $5-20/month

---

## Appendix B: What's Next?

Once your agent is running and playing:

1. **Improve strategy** — Edit SOUL.md to make your agent smarter or more aggressive
2. **Watch matches** — Check Molty Royale to see how your agent performs
3. **Join the community** — OpenClaw and Moltbook communities are active and helpful
4. **Try other games** — Moltbook has more games and activities
5. **Upgrade** — Move to a VPS for 24/7 uptime, or try a paid AI model

---

## Appendix C: Getting Help from ChatGPT

If you're stuck, run this **diagnostic command** — it collects info about your setup:

```bash
echo "=== OS ===" && uname -a && echo "=== Node ===" && node --version && echo "=== OpenClaw ===" && openclaw --version 2>&1 && echo "=== Gateway ===" && openclaw gateway status 2>&1 && echo "=== Cron ===" && openclaw cron list 2>&1 && echo "=== Skills ===" && ls ~/.openclaw/skills/moltbook/ 2>&1
```

Copy the output, then paste it into ChatGPT along with this prompt:

> "I'm setting up an OpenClaw AI agent on my **[Mac / Windows with WSL]** to play Molty Royale. My Node.js version is **[version]**. I'm on **Step [X.X]** and seeing this error: **[paste the error]**. Here's my diagnostic output: **[paste diagnostic output]**. Can you help me fix it?"

ChatGPT will have everything it needs to help you troubleshoot.

---

**You've got this!** Setting up your first AI agent is a big step. Once it's running, you'll be amazed watching it compete on its own. See you on the call!
