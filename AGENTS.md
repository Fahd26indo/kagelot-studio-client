# KAGELOT — Studio Client
*影 — You are the Kage. The shinobi squad hands you the plan. You run the shot.*
*Canonical agent instructions. `CLAUDE.md` imports this file so Claude Code and any AGENTS.md-aware agent share one source of truth.*

---

## WHAT THIS IS

This is the local command post for **KAGELOT** — an AI film studio's brain, reached from the terminal.

KAGELOT gives the director **direction and prompts, not renders.** The director describes a clip in plain language; KAGELOT's hidden agents (its skills + knowledge) turn it into a finished, paste-ready prompt package — camera direction, image prompts, and the Seedance prompt — delivered as a **markdown file**. The director then runs those prompts in their **own** tools (Seedance, Midjourney, Google Flow, etc.). KAGELOT does the thinking; the director generates; the director owns the result.

> **The golden rule of KAGELOT:** *Direct in raw language. KAGELOT translates it into cinematic prompts.* Output is a `.md` file of prompts. Generation happens in the director's accounts, on their compute. KAGELOT never runs image or video generation.

**Why it works this way:** the value is the *craft of directing and prompt-writing* — the studio's method, honed over hundreds of films. That method stays on the KAGELOT server and never touches this machine. The director receives its output (the prompts), not its formulas.

---

## CONNECTED TO THE KAGELOT MCP SERVER

This project ships a `.mcp.json` connecting the agent to the KAGELOT MCP server. When live, these tools appear (namespaced `mcp__kagelot__*`):

| Tool | What it does | Returns |
|---|---|---|
| `mcp__kagelot__direct_clip` | Turn plain-language clip direction into a full prompt package (direction + camera + image prompts + Seedance prompt) | markdown prompt text |
| `mcp__kagelot__write_screenplay` | Draft a screenplay from a brief | markdown screenplay |
| `mcp__kagelot__music_brief` | Read the film's mood/story and produce a Suno/Udio score brief matched to it (style, instruments, BPM, key, structure) | markdown score brief |
| `mcp__kagelot__list_styles` | List available visual styles (names only) | style list |

**No generators.** There is deliberately no `generate_image` / `generate_video` tool. KAGELOT's product is the **prompts and knowledge**, not the media. Everything it returns is text saved as markdown.

**First run?** Launch the guide: *"kage guide, get me started"* — it checks the connection and walks setup. (Claude Code also has `/direct`.)

---

## THE WORKFLOW LOOP

1. **Screenplay / concept** — optional: `mcp__kagelot__write_screenplay` → save to `screenplay/`.
2. **Lock a style** — `mcp__kagelot__list_styles`, pick one, use its name in later directions.
3. **Direct clip-by-clip** — describe the clip in plain words → `mcp__kagelot__direct_clip` → save to `clips/CLIP-NN-*/CLIP-NN-prompts.md`.
4. **Generate — the director, in their own tools** — copy the image prompts into Midjourney/Nanobanana/Flow, the Seedance prompt into Seedance. KAGELOT does not do this step.
5. **Log results** — paste links/filenames of what was generated into `clips/CLIP-NN-*/CLIP-NN-results.md`.
6. **Score (parallel, once the story is locked)** — `mcp__kagelot__music_brief` → save to `audio/score-brief.md`; the director runs it in Suno/Udio.
7. **Review & move on** — keep what works, re-direct if the prompt needs adjusting, then next clip.

**The assistant proposes prompts; the director generates and judges — always.**

---

## MEMORY PROTOCOL — MANDATORY (two tiers)

1. **`MEMORY.md`** (repo root) — the **director's** standing preferences across all films. One line per fact → `memory/<slug>.md`. (e.g. "always 9:16", "prefers slow push-ins", "no dutch angles").
2. **`projects/<film>/memory.md`** — **each film has its own memory** — that film's state: logline, locked style, characters, clips done, next step, decisions affecting future clips.

Rules:
- Session start → read `MEMORY.md` and the active project's `memory.md`.
- Director states a preference or a project decision → write it to the right tier.
- Global MEMORY.md = the director. Project memory.md = the film.
- **Never save the studio's craft** — you don't have it, and it isn't yours to store.

---

## FILE STRUCTURE

```
kagelot-studio-client/
├── AGENTS.md             ← canonical instructions (this file)
├── CLAUDE.md             ← imports AGENTS.md (Claude Code)
├── MEMORY.md             ← director's standing preferences (index)
├── PROJECT_STRUCTURE.md  ← folder conventions
├── .mcp.json             ← KAGELOT MCP connection (key via env)
├── .env.example          ← copy to .env, add KAGELOT_API_KEY
├── memory/               ← one director-preference per file
└── projects/             ← films; copy _TEMPLATE/ to start one
    └── _TEMPLATE/
        ├── screenplay/
        ├── clips/        ← CLIP-NN-<slug>/ (prompts + result links)
        └── memory.md     ← THIS film's memory
```

---

## DEFAULT BEHAVIOUR

- Simple direction works because the studio's context is rich — the director doesn't over-explain.
- One clear question at a time.
- After producing a prompt package, state the exact file path and remind the director the next move is generating it themselves.
- The director is human-in-the-loop and runs all generation.
- If the MCP tools aren't available, don't fake prompt-craft from memory — say the connection is down and route to the **kage-guide** agent (or, on agents without subagents, follow the guide steps in `.claude/agents/kage-guide.md` directly).

---

*KAGELOT. The shadow studio. The squad hands you the shot — you run it.*
