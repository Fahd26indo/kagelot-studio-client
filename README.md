# KAGELOT — Studio Client 影

**Your local command post for KAGELOT — the AI film studio you direct in plain language.**

You are the *Kage* (the shadow commander). This kit connects [Claude Code](https://claude.com/claude-code) to the **KAGELOT MCP server**, so you can direct films from your terminal: describe a clip in your own words, and KAGELOT turns it into cinematic prompts, generates the images, and renders the video — the craft runs on the server, you keep the taste.

---

## What's in here

An advanced Claude Code setup, ready to use:

- **`CLAUDE.md`** — auto-loads every session: the workflow, the memory protocol, and the KAGELOT tools.
- **`.claude/agents/kage-guide.md`** — an onboarding agent that checks your connection and walks you through setup.
- **`.claude/commands/`** — `/direct` (direct a clip) and `/render` (render a clip).
- **Memory system** — `MEMORY.md` + `memory/` so the assistant remembers your preferences and project state across sessions.
- **Project scaffold** — `projects/_TEMPLATE/` you copy for each new film.
- **`.mcp.json`** — the KAGELOT MCP connection (your key stays in `.env`, never committed).

You never see or store the studio's prompt-craft. You get finished outputs — prompts, images, videos.

---

## Setup (5 minutes)

**1. Install Claude Code** (if you haven't):
```bash
npm install -g @anthropic-ai/claude-code
```

**2. Get your KAGELOT key.** Ask the KAGELOT team for your API key (it's tied to your account + credit balance).

**3. Add your key:**
```bash
cp .env.example .env
# open .env and paste your key into KAGELOT_API_KEY
```

**4. Open the project in Claude Code and start:**
```bash
claude
```
Then say: **"kage guide, get me started"** — the guide agent verifies the connection and takes it from there.

---

## The workflow

```
concept → lock a style → character stills → direct clip-by-clip → generate assets → render → approve → next clip
```

You describe each clip in plain language. KAGELOT does the prompt engineering and rendering. You judge the result and keep the takes you like.

Full details load automatically from `CLAUDE.md` when you open the project.

---

## What stays private

The studio's system prompts, direction method, style formulas, and provider keys **live on the KAGELOT server and never touch this machine.** This kit only knows how to *ask* for outputs and where to save them. That's the deal: you get the studio's power without holding its secrets.

---

*KAGELOT — the shadow studio. Direct your film; the squad builds it.*
