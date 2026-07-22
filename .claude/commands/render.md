---
description: Render a directed clip in Seedance via KAGELOT.
---

# /render — Render a clip

Render a clip that already has a prompts file (and ideally a first frame + assets) in its folder.

## Steps
1. Identify the target clip folder (`clips/CLIP-<NN>-*`). Confirm it has a `-prompts.md`. If it doesn't, run `/direct` first.
2. Confirm render settings with the director if unsure — model (default: the fast/cheap Seedance tier), duration, aspect ratio. **Every render costs credits**, so don't upgrade model or count without being asked.
3. Call `mcp__kagelot__generate_video` with the clip number and its prompt. KAGELOT attaches the clip's reference images itself — you do not pass image URLs.
4. Save the returned video URL into the clip folder (e.g. `clips/CLIP-<NN>-*/CLIP-<NN>-video.md` with the URL, or note it in the clip's index). Renders don't overwrite — add a new entry for each take.
5. Tell the director the URL and ask them to review. Keep the take they approve; re-roll the ones they reject (a re-roll is a fresh call — Seedance has no seed control, so each is a true re-roll).

## Notes
- Renders take a few minutes — don't block; report when the URL lands.
- If a render fails on a content-moderation error, note it and suggest a stylized/cleaner reference image rather than retrying blindly. Never attempt to evade filters.
- Insufficient-credit error → tell the director to top up with the KAGELOT team; don't loop.
- Tools unavailable → route to **kage-guide**.
