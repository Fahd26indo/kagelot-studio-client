# KAGELOT — Studio Client 影

**Your local command post for KAGELOT — the AI film studio you direct in plain language.**

You are the *Kage* (the shadow commander). This kit connects [Claude Code](https://claude.com/claude-code) to the **KAGELOT MCP server**, so you can direct films from your terminal: describe a clip in your own words, and KAGELOT hands you a finished **prompt package** — camera direction, image prompts, and the Seedance prompt — as a markdown file. You then run those prompts in your **own** tools (Seedance, Midjourney, Flow). KAGELOT does the thinking; you do the generating; you own the result.

---

## What's in here

An advanced Claude Code setup, ready to use:

- **`CLAUDE.md`** — auto-loads every session: the workflow, the memory protocol, and the KAGELOT tools.
- **`.claude/agents/kage-guide.md`** — an onboarding agent that checks your connection and walks you through setup.
- **`.claude/commands/`** — `/direct` (direct a clip) and `/render` (render a clip).
- **Memory system** — `MEMORY.md` + `memory/` for your standing preferences, plus a **`memory.md` inside every project** for that film's state.
- **Project scaffold** — `projects/_TEMPLATE/` you copy for each new film.
- **`.mcp.json`** — the KAGELOT MCP connection (your key stays in `.env`, never committed).

KAGELOT returns **prompts, not renders.** You never see or store the studio's prompt-craft — you get finished prompt packages as markdown and generate them yourself.

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
concept → lock a style → direct clip-by-clip → KAGELOT returns a prompt .md → you generate it in your own tools → log results → next clip
```

You describe each clip in plain language. KAGELOT does the direction and prompt engineering and hands you a markdown file. You run those prompts in Seedance/Midjourney/Flow yourself, keep the takes you like, and note them in the clip's `-results.md`.

Full details load automatically from `CLAUDE.md` when you open the project.

---

## What stays private

The studio's system prompts, direction method, and style formulas **live on the KAGELOT server and never touch this machine.** This kit only knows how to *ask* for prompt packages and where to save them. That's the deal: you get the studio's directing brain without holding its secrets — and you run generation on your own compute, in your own accounts.

---

*KAGELOT — the shadow studio. Direct your film; the squad builds it.*
