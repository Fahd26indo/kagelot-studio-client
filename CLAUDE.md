---
tags: [kagelot, client, root, orchestrator]
---

# KAGELOT — Studio Client
*影 — You are the Kage. The shinobi squad hands you the plan. You run the shot.*
*This file auto-loads every session. Do not delete.*

---

## WHAT THIS IS

This is your local command post for **KAGELOT** — an AI film studio's brain, reached from your terminal.

KAGELOT gives you **direction and prompts, not renders.** You describe a clip in plain language; KAGELOT's hidden agents (its skills + knowledge) turn it into a finished, paste-ready prompt package — camera direction, image prompts, and the Seedance prompt — delivered as a **markdown file**. You then run those prompts in **your own** generation tools (Seedance, Midjourney, Google Flow, etc.). KAGELOT does the thinking; you push the buttons; you own the result.

> **The golden rule of KAGELOT:** *Direct in raw language. KAGELOT translates it into cinematic prompts.* You get the prompts as a `.md` file. Generation happens in your accounts, on your compute. KAGELOT never runs image or video generation for you.

**Why it works this way:** the value is the *craft of directing and prompt-writing* — the studio's method, honed over hundreds of films. That method stays on the KAGELOT server and never touches this machine. You receive its output (the prompts), not its formulas.

---

## YOU ARE CONNECTED TO THE KAGELOT MCP SERVER

This project ships a `.mcp.json` that connects Claude Code to the KAGELOT MCP server. When it's live, these tools appear (namespaced `mcp__kagelot__*`):

| Tool | What it does | Returns |
|---|---|---|
| `mcp__kagelot__direct_clip` | Turn a plain-language clip direction into a full prompt package (direction + camera + image prompts + Seedance prompt) | markdown prompt text |
| `mcp__kagelot__write_screenplay` | Draft a screenplay from a brief | markdown screenplay |
| `mcp__kagelot__list_styles` | List available visual styles (names only) | style list |

**No generators.** There is deliberately no `generate_image` / `generate_video` tool. KAGELOT's product here is the **prompts and knowledge**, not the media. Everything KAGELOT returns is text you save as markdown.

**First time here?** Launch the guide: it checks your connection and walks you through setup.
→ Ask: *"kage guide, get me started"* (or run `/direct` once the connection is verified).

---

## THE WORKFLOW LOOP

Teach and follow this order:

1. **Screenplay / concept** — optional: `mcp__kagelot__write_screenplay` from a brief → save to `screenplay/`.
2. **Lock a style** — `mcp__kagelot__list_styles`, pick one, use its name in later directions.
3. **Direct clip-by-clip** — describe the clip in your own words → `mcp__kagelot__direct_clip` → save the returned prompt package to `clips/CLIP-NN-*/CLIP-NN-prompts.md`.
4. **Generate — yourself, in your own tools** — copy the image prompts into Midjourney/Flow, the Seedance prompt into Seedance. KAGELOT does not do this step.
5. **Log your results** — paste the links/filenames of what you generated into `clips/CLIP-NN-*/CLIP-NN-results.md` so the project stays tracked.
6. **Review & move on** — keep what works, re-direct the clip if the prompt needs adjusting, then next clip.

**The assistant proposes prompts; you generate and judge — always.**

---

## MEMORY PROTOCOL — MANDATORY (two tiers, like a real studio)

1. **`MEMORY.md`** (repo root) — the **director's** standing preferences across all films. One line per fact, pointing to `memory/<slug>.md`. (e.g. "always vertical 9:16", "prefers slow push-ins", "no dutch angles").
2. **`projects/<film>/memory.md`** — **each project has its own memory file** — that film's state: logline, locked style, characters, which clips are done, next step, and any decision that affects future clips. Update it as you work so the next session picks up cleanly.

Rules:
- Session start → read `MEMORY.md` and the active project's `memory.md`.
- When the director states a preference or a project decision → write it to the right tier.
- Global MEMORY.md = the director. Project memory.md = the film.
- **Never save the studio's craft** — you don't have it, and it isn't yours to store. Memory here is the director's taste and each project's state, nothing more.

---

## FILE STRUCTURE

```
kagelot-studio-client/
├── CLAUDE.md              ← this file (auto-loads)
├── MEMORY.md             ← director's standing preferences (index)
├── PROJECT_STRUCTURE.md  ← folder conventions
├── .mcp.json             ← KAGELOT MCP connection (key via env)
├── .env.example          ← copy to .env, add your KAGELOT_API_KEY
├── memory/               ← one director-preference per file
└── projects/             ← your films
    └── _TEMPLATE/        ← copy this folder to start a new film
        ├── screenplay/
        ├── clips/        ← CLIP-NN-<slug>/  (prompts + your result links)
        └── memory.md     ← THIS film's memory (state, style, next step)
```

Every prompt package saves as markdown into its project's clip folder. Name by role, never by client name — see `PROJECT_STRUCTURE.md`.

---

## DEFAULT BEHAVIOUR

- Simple direction works because the studio's context is rich — the director doesn't need to over-explain.
- One clear question at a time, not five.
- After producing a prompt package, state the exact file path where it was saved.
- The director is human-in-the-loop and runs all generation themselves.
- If the MCP tools aren't available, don't fake prompt-craft from memory — say the connection is down and route to the **kage-guide** agent.

---

*KAGELOT. The shadow studio. The squad hands you the shot — you run it.*
