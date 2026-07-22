# Project Structure — KAGELOT films

Every film is a folder under `projects/`. Copy `projects/_TEMPLATE/` to start a new one. Name things by **role**, never by client or personal name — so references stay clean.

KAGELOT returns **prompts as markdown**. It does not generate or host any media. The director generates in their own tools and keeps their own files; this repo stores the **prompt packages** and **links to what the director generated**.

```
projects/<film-name>/
├── memory.md                   ← THIS film's memory: logline, style, characters, progress, next step
├── screenplay/                 ← markdown screenplays / outlines
└── clips/
    ├── _index.md               ← the timeline: one row per clip
    └── CLIP-<NN>-<slug>/        ← one folder per clip
        ├── CLIP-<NN>-prompts.md    ← KAGELOT's prompt package (direction + camera + image prompts + Seedance prompt)
        └── CLIP-<NN>-results.md    ← the director's own generated results: links/filenames + which take was kept
```

## Naming rules
- **Clips:** `CLIP-<NN>-<slug>` with a zero-padded number (`CLIP-01-...`). The slug is a short kebab-case description.
- **Prompts vs results:** `-prompts.md` is what KAGELOT wrote. `-results.md` is what the director generated from it (in Midjourney/Seedance/Flow) and where those files live.
- **Per-project memory:** every film folder has its own `memory.md` — the studio's working memory of that film.

## Where things come from
- `screenplay/` ← `mcp__kagelot__write_screenplay` (optional)
- clip `-prompts.md` ← `mcp__kagelot__direct_clip`
- clip `-results.md` ← the **director**, after generating the prompts in their own tools

KAGELOT never touches the media. It hands you the plan; you shoot it.
