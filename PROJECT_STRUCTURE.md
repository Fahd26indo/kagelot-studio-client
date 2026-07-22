# Project Structure — KAGELOT films

Every film is a folder under `projects/`. Copy `projects/_TEMPLATE/` to start a new one. Name things by **role**, never by client or personal name — so variables and references stay clean.

```
projects/<film-name>/
├── screenplay/                 ← markdown screenplays / outlines
├── characters/                 ← REF-<name>-still.png   (approved character reference stills)
├── clips/
│   ├── _index.md               ← the timeline: one row per clip
│   └── CLIP-<NN>-<slug>/       ← one folder per clip
│       ├── CLIP-<NN>-prompts.md      ← the 4-layer prompt KAGELOT returned
│       ├── CLIP-<NN>-first-frame.png ← the clip's anchor frame
│       ├── CLIP-<NN>-asset-*.png     ← props / extra assets for this clip
│       └── CLIP-<NN>-video.md        ← rendered take URLs (one entry per take)
└── memory.md                   ← this film's session state / next step
```

## Naming rules
- **Characters:** `REF-<name>-still.png` (e.g. `REF-kael-still.png`). Character reference is a full still, not a crop.
- **Clips:** `CLIP-<NN>-<slug>` with a zero-padded number (`CLIP-01-...`, `CLIP-02-...`). The slug is a short kebab-case description.
- **Clip first frame ≠ character reference.** A clip's anchor frame lives *inside that clip folder*, not in `characters/`.
- **Renders never overwrite.** Each take is a new entry (`-video`, `-video-2`, ...). Seedance has no seed control, so every re-roll is a genuine new take.

## Where things come from
- `screenplay/` ← `mcp__kagelot__write_screenplay` (optional)
- `characters/`, clip frames, assets ← `mcp__kagelot__generate_image`
- clip `-prompts.md` ← `mcp__kagelot__direct_clip`
- clip videos ← `mcp__kagelot__generate_video`

KAGELOT hosts the actual image/video files on its CDN; this repo stores the **URLs and prompts**, not heavy media (see `.gitignore`).
