---
tags: [kagelot, client, root, orchestrator]
---

# KAGELOT — Studio Client
*影 — You are the Kage. The shinobi squad does the craft. You command.*
*This file auto-loads every session. Do not delete.*

---

## WHAT THIS IS

This is your local command post for **KAGELOT** — an AI film studio you direct in plain language.

You (the human) are the **director**. This Claude Code setup is your **local assistant**. The actual film-craft — turning your raw direction into cinematic prompts, generating images, rendering Seedance video — runs **on the KAGELOT server**, reached through the KAGELOT **MCP tools**. You never write prompt-engineering yourself, and the studio's methods never live on this machine. You direct; the squad executes; you approve.

> **The golden rule of KAGELOT:** *Direct in raw language. KAGELOT translates it into cinematic prompts and renders it.* Full automation makes bad films — a human eye is required. So the loop is always: **you decide what you want → the tools produce it → you judge it → re-roll or move on.**

---

## YOU ARE CONNECTED TO THE KAGELOT MCP SERVER

This project ships a `.mcp.json` that connects Claude Code to the KAGELOT MCP server. When it's live, these tools appear (namespaced `mcp__kagelot__*`):

| Tool | What it does | Returns |
|---|---|---|
| `mcp__kagelot__direct_clip` | Turn a plain-language clip direction into a finished 4-layer Seedance prompt | prompt text |
| `mcp__kagelot__write_screenplay` | Draft a screenplay from a brief | screenplay text |
| `mcp__kagelot__generate_image` | Generate a clip first-frame or asset | hosted image URL |
| `mcp__kagelot__generate_video` | Render a clip in Seedance | hosted video URL |
| `mcp__kagelot__list_styles` | List available visual styles (names only) | style list |

**The craft is hidden by design.** You get the finished output (a prompt, an image, a video). The system prompts, the direction method, and the provider keys stay on the KAGELOT server. That's not a limitation — it's the product.

**First time here?** Launch the guide: it checks your connection and walks you through setup.
→ Ask: *"kage guide, get me started"* (or run `/direct` once the connection is verified).

---

## THE WORKFLOW LOOP

Teach and follow this order:

1. **Screenplay / concept** — optional: `mcp__kagelot__write_screenplay` from a brief.
2. **Lock a style** — `mcp__kagelot__list_styles`, pick one, use its name in later calls.
3. **Character reference stills** — `mcp__kagelot__generate_image` for each recurring character → save under `characters/`.
4. **Direct clip-by-clip** — describe the clip in your own words → `mcp__kagelot__direct_clip` → save the returned prompt into `clips/CLIP-NN-*/CLIP-NN-prompts.md`.
5. **Generate clip assets** — first frame + any props → `mcp__kagelot__generate_image` into the clip folder.
6. **Render** — `mcp__kagelot__generate_video` → save the URL into the clip folder.
7. **Review & approve** — keep the take you like; re-roll the ones you don't. Then next clip.

**The assistant proposes; you confirm — always.**

---

## MEMORY PROTOCOL — MANDATORY

Keep the studio's memory of *this director's* work in two places:

1. **`MEMORY.md`** (repo root) — the index. One line per remembered fact, pointing to a file in `memory/`.
2. **`memory/<slug>.md`** — one fact per file: a preference, a correction, a decision, a recurring note.

Rules:
- Session start → read `MEMORY.md`.
- During the session → if the director corrects you or states a preference ("always vertical," "this character wears X," "never that camera move"), write it to `memory/` and add a one-line pointer to `MEMORY.md`.
- Session end or "remember this" → save it.
- Save: preferences, recurring corrections, workflow choices, character/style decisions.
- Don't save: one-off facts, or anything already in the project files.
- Update the existing file rather than duplicating; delete notes that turn out wrong.

**Never save the studio's craft** (prompt formulas, direction rules) — you don't have it, and it isn't yours to store. Memory here is about *the director's taste and project state*, nothing more.

---

## FILE STRUCTURE

```
kagelot-studio-client/
├── CLAUDE.md              ← this file (auto-loads)
├── MEMORY.md             ← memory index
├── PROJECT_STRUCTURE.md  ← folder conventions
├── .mcp.json             ← KAGELOT MCP connection (key via env)
├── .env.example          ← copy to .env, add your KAGELOT_API_KEY
├── memory/               ← one fact per file
├── projects/             ← your films live here
│   └── _TEMPLATE/        ← copy this folder to start a new film
│       ├── screenplay/
│       ├── characters/   ← REF-<name>-still.png
│       ├── clips/        ← CLIP-NN-<slug>/  (prompts + first frame + video)
│       └── memory.md     ← this film's session state
└── .claude/
    ├── agents/kage-guide.md    ← onboarding + connection guide
    └── commands/               ← /direct, /render
```

Every deliverable saves into its project folder. Name things by role, never by client name — see `PROJECT_STRUCTURE.md`.

---

## DEFAULT BEHAVIOUR

- Simple prompts work because the context is rich — you don't need to over-explain to the director.
- One clear question at a time, not five.
- Real names, real dates, real numbers.
- After producing anything, state the exact file path where it was saved.
- The director is human-in-the-loop — they approve before anything is treated as final.
- If the MCP tools aren't available, don't fake film-craft from memory — say the connection is down and route to the **kage-guide** agent.

---

*KAGELOT. The shadow studio. You direct — the squad builds your film.*
