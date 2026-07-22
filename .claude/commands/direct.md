---
description: Direct a clip in plain language — KAGELOT turns it into a finished 4-layer Seedance prompt.
---

# /direct — Direct a clip

The director describes a clip in their own words. You send that raw direction to KAGELOT and save the finished prompt into the clip folder. **You do not write the prompt-craft yourself — KAGELOT does.**

## Steps
1. If the director hasn't already described the clip in this message, ask for it in one line: *"Describe the clip — what happens, and the feeling you want."* Also confirm which **style** to use (from `mcp__kagelot__list_styles`) and the **clip number**.
2. Call `mcp__kagelot__direct_clip` with:
   - `clip` — the clip number (e.g. `05`)
   - `raw_direction` — the director's plain-language description, verbatim (don't polish it into "prompt language" yourself — that's KAGELOT's job)
   - `style` — the chosen style name
3. Save the returned prompt text to `clips/CLIP-<NN>-<slug>/CLIP-<NN>-prompts.md` inside the active project. Create the folder if needed.
4. Tell the director the exact file path, and offer the next step: generate the first frame (`/direct`'s sibling — `mcp__kagelot__generate_image`) or render (`/render`).

## Notes
- One clip per call. Don't batch multiple clips into one direction.
- If the director corrects the result, capture the correction as a memory (`memory/` + `MEMORY.md`) so it carries forward.
- If the KAGELOT tools aren't available, stop and route to the **kage-guide** agent — do not invent a prompt from memory.
