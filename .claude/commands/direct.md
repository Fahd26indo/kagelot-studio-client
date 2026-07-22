---
description: Direct a clip in plain language — KAGELOT returns a full prompt package (markdown). You generate it yourself.
---

# /direct — Direct a clip

The director describes a clip in their own words. You send that raw direction to KAGELOT and save the returned **prompt package** into the clip folder. **You do not write the prompt-craft yourself, and you do not generate anything — KAGELOT writes the prompts; the director runs them in their own tools.**

## Steps
1. If the director hasn't described the clip yet, ask in one line: *"Describe the clip — what happens, and the feeling you want."* Confirm the **style** (from `mcp__kagelot__list_styles`) and the **clip number**.
2. Call `mcp__kagelot__direct_clip` with:
   - `clip` — the clip number (e.g. `05`)
   - `raw_direction` — the director's plain-language description, verbatim (don't polish it into "prompt language" yourself — that's KAGELOT's job)
   - `style` — the chosen style name
3. Save the returned markdown (direction + camera + image prompts + Seedance prompt) to `clips/CLIP-<NN>-<slug>/CLIP-<NN>-prompts.md` in the active project. Create the folder if needed.
4. Tell the director the exact file path, and the next move: **copy the image prompts into Midjourney/Flow and the Seedance prompt into Seedance — in their own accounts.** Then log the results in `CLIP-<NN>-results.md`.
5. Update the active project's `memory.md` (mark the clip directed, set the next step).

## Notes
- One clip per call. Don't batch multiple clips into one direction.
- KAGELOT returns text only — never treat `/direct` as generating an image or video.
- If the director corrects the result, save the correction as a memory so it carries forward (director-wide → `memory/` + `MEMORY.md`; this film only → the project `memory.md`).
- If the KAGELOT tools aren't available, stop and route to the **kage-guide** agent — do not invent a prompt from memory.
