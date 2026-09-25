# KAGELOT — Studio Client 影

**An expert AI film-direction brain for your coding agent. It writes the prompts; you make the film.**

KAGELOT plugs into Claude Code, Kimi, or any MCP-capable agent and turns plain-language direction into **paste-ready prompts** — for Seedance video, for storyboards and shot diagrams, and for any image generator (Nanobanana, Midjourney, Google Flow). You describe the shot in your own words; KAGELOT hands back a finished prompt package as a markdown file. You run those prompts in your own tools. The studio's method stays on the KAGELOT server — you get its output, not its formulas.

> **KAGELOT returns prompts, not renders.** No image or video generation runs here. That's the point: you get the directing and prompt-writing expertise, and you generate on your own compute, in your own accounts.

---

## What it's expert at

- 🎬 **Seedance video prompts** — describe a clip, get a full multi-layer prompt: story direction, camera angles, and the paste-ready Seedance prompt, tuned the way a real director would build it.
- 🎞️ **Storyboards & shot diagrams** — get the storyboard-grid and director's-blueprint prompts that lock composition and camera before you generate — the single biggest lever on render quality.
- 🖼️ **Image-generator prompts** — first-frame and asset prompts for **Nanobanana, Midjourney, Google Flow, or any image model** you use, style-locked and character-consistent.
- 🎵 **Music & score prompts** — reads the film's mood and story and returns a **Suno/Udio-ready score brief** (style, instruments, BPM, key, structure) matched to the scene — it understands what the film actually needs, not a generic "epic music" tag.
- 📝 **Screenplays** — draft a screenplay from a one-line brief.

All output is markdown you save into your project. You copy it into your generation tools and shoot.

---

## Works with any MCP agent

KAGELOT is an [MCP](https://modelcontextprotocol.io) server, so it connects to whatever agent you already use:

**Claude Code · Kimi · Cursor · Cline · Windsurf · Continue · Gemini CLI · Zed** — and more.

Same server, same key. Only the config file differs per tool (below).

---

## Install

### 1. Prerequisites
- An MCP-capable agent (e.g. [Claude Code](https://claude.com/claude-code): `npm install -g @anthropic-ai/claude-code`).
- Your **KAGELOT API key** — ask the KAGELOT team (it's tied to your account).

### 2. Get the kit
```bash
git clone https://github.com/Fahd26indo/kagelot-studio-client.git
cd kagelot-studio-client
```

### 3. Add your key (the step everyone gets wrong)

`.mcp.json` contains `"Authorization": "Bearer ${KAGELOT_API_KEY}"` — that `${...}` reads a **real OS environment variable**, nothing else. Two ways to make it resolve — pick ONE:

**A. Simplest — paste the key into `.mcp.json` directly:**
```json
"Authorization": "Bearer kgl_your_real_key_here"
```
⚠️ After this, **never commit `.mcp.json`** — it now holds your secret.

**B. Clean — set a real environment variable:**
- **Windows (PowerShell):** `setx KAGELOT_API_KEY "kgl_your_real_key"` → must print `SUCCESS` → **close ALL terminal windows** (setx only affects windows opened after it runs).
- **macOS/Linux:** add `export KAGELOT_API_KEY="kgl_your_real_key"` to `~/.zshrc` → open a new shell.

**Do NOT:**
- ❌ paste the key into `.env.example` — it's a template, **nothing ever reads it**.
- ❌ rely on a `.env` file — most MCP agents (incl. Claude Code) do **not** auto-load `.env` for `.mcp.json` interpolation.
- ❌ paste the key inside the braces (`${kgl_...}`) — that makes it look up a variable *named* your key, which doesn't exist.

### 4. Connect your agent to KAGELOT

**Claude Code** — the included `.mcp.json` already wires it up. **Restart the agent after adding your key** (MCP servers connect at startup only), then approve the `kagelot` server when prompted:
```bash
claude
```
Verify with `/mcp` — `kagelot` should show **connected**.
Or add it explicitly (uses your OS env var):
```bash
claude mcp add --transport http kagelot https://kagelot.com/api/mcp \
  --header "Authorization: Bearer $KAGELOT_API_KEY"
```

**Kimi** — add the same server in Kimi's MCP config (an HTTP MCP server), using the URL `https://kagelot.com/api/mcp` and header `Authorization: Bearer <your-key>`.

**Any other MCP agent** — point it at `https://kagelot.com/api/mcp` with your key in the `Authorization: Bearer` header. Cursor uses `.cursor/mcp.json`, Cline/Windsurf each have their own MCP settings — the server details are identical.

### 5. Start directing
Open the project in your agent and say:
> **"kage guide, get me started"**

The built-in guide checks your connection and walks you through your first clip.

---

## The workflow

```
lock a style → direct a clip in plain words → KAGELOT returns a prompt .md → you generate it in your own tools → next clip
```

Each film lives in `projects/<name>/`, with its own `memory.md` tracking style, progress, and next step. Full details load automatically from `CLAUDE.md` (Claude Code) / `AGENTS.md` (other agents) when you open the project.

---

## What stays private

The studio's system prompts, direction method, and style formulas **live on the KAGELOT server and never touch your machine.** This kit only knows how to *ask* for prompt packages and where to save them. You get the directing brain; KAGELOT keeps its secrets; and every render runs on your own accounts.

---

*KAGELOT — the shadow studio. Direct in plain language; the squad writes the prompts.*
