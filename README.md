# Wong–Roa Wedding Seating Chart

Mobile-friendly seating chart for the Wong–Roa wedding — Emerald Ballroom, Crystal Springs Resort, November 1, 2026.

Tap a table on the floor plan to see who's seated and add guests from the master list. Everything is a single `index.html` — no build step, no backend.

## Features

- **Floor plan** — 16 round tables plus fixtures (band/DJ, dance floor, sweetheart table, cake, gifts, bar). A gold ring around each table shows how full it is; a table turns solid emerald when full.
- **Guest picker** — bottom sheet grouped by family group, searchable, only shows unseated guests.
- **Guest list** — full roster with bride/groom/mutual color dots, Maybe/Unlikely tags, search, and a "hide unlikely" filter. Tap a guest's table badge to unseat them.
- **Table capacity** — 10 seats by default, adjustable per table up to 14.
- **Autosave** — every change is saved to the browser's `localStorage` (key `wongroa-seating-v1`).
- **Export / Import JSON** — buttons on the Guest List tab. `localStorage` doesn't sync between devices, so use export/import to move the plan between phones/browsers. Exports store guests by name, so they survive edits to the guest list order.
- **Clear all assignments** — with a confirmation prompt.

## ⚠️ Guest data is SAMPLE data

The guest list currently in `index.html` is **placeholder names only**. To load the real list, edit the `RAW` constant near the top of the `<script>` block. One guest per line:

```
First,Last,Family Group,Side,Status
```

- **Side:** `B` = Bride · `G` = Groom · `M` = Mutual
- **Status:** `D` = Definite · `M` = Maybe · `U` = Unlikely

**Privacy note:** a public repo (and its GitHub Pages site) is visible to anyone with the link. Keep home addresses and other contact info out of this file — names only. If even names feel like too much, make the repo private (Pages on private repos requires a paid GitHub plan) or keep the file local.

## Deploying to GitHub Pages

1. Merge this branch into `main`.
2. In the repo: **Settings → Pages → Source: Deploy from a branch → Branch: `main`, folder: `/ (root)`** → Save.
3. The site will be live at `https://<username>.github.io/CrystalSpringsSeating/` after a minute or two.

## Files

- `index.html` — the entire app (vanilla HTML/CSS/JS, fonts loaded from Google Fonts).
