# Wedding Planning Seating Chart

Mobile-friendly wedding seating planner for the Emerald Ballroom at Crystal Springs Resort.

Tap a table on the floor plan to see who's seated and add guests from the master list. Everything is a single `index.html` — no build step, no backend.

## Features

- **Floor plan** — 16 round tables arranged to match the supplied ballroom plan, plus fixtures (band/DJ, dance floor, sweetheart table, cake, gifts, bar). A gold ring around each table shows how full it is; a table turns solid burgundy when full.
- **Original plan viewer** — opens the supplied ballroom image inside the app, with a link to view it full size.
- **Guest picker** — bottom sheet grouped by family group, searchable, and limited to unseated guests matching the selected status filters.
- **Guest list** — full roster with bride/groom/mutual color dots, Maybe/Unlikely tags, search, and independent Definite/Maybe/Unlikely filters. Only Definite guests are shown by default. Tap a guest's table badge to unseat them.
- **Table capacity** — 10 seats by default, adjustable per table up to 14.
- **Autosave** — every change is saved to the browser's `localStorage` (key `wongroa-seating-v1`).
- **Save / load code** — prominent controls under the Guest List filters generate a compact code for the current arrangement or restore one pasted later. Codes contain guest indexes rather than names and are validated against the current guest list.
- **Export / Import JSON** — buttons on the Guest List tab. `localStorage` doesn't sync between devices, so use export/import to move the plan between phones/browsers. Exports store guests by name, so they survive edits to the guest list order.
- **Clear all assignments** — with a confirmation prompt.
- **Passphrase gate** — the page asks for a passphrase before showing anything. Once entered correctly it's remembered on that device (`localStorage` key `wongroa-pass-v1`), so you only type it once per browser.

## Guest data & privacy

The real guest list is embedded in `index.html`, but **encrypted** (AES-256-GCM, key derived from the passphrase), so the names are not readable in the page source or the repo. Entering the passphrase decrypts the list in the browser; nothing is ever sent to a server.

Only what the app needs is stored: first name, last name, family group, side, and RSVP status. **No addresses or contact info are in this repo — keep it that way.**

To update the guest list, the encrypted blob (`ENC` constant in the `<script>` block) has to be regenerated: decrypt with the passphrase, edit the CSV (`First,Last,Family Group,Side,Status` per line; Side `B`/`G`/`M` = Bride/Groom/Mutual; Status `D`/`M`/`U` = Definite/Maybe/Unlikely), re-encrypt with the same passphrase (SHA-256 of the lowercased passphrase as the AES key, 12-byte IV prepended, base64). Easiest is to just ask Claude to do it.

This is a convenience lock, not bank-grade security: it keeps bots and casual visitors out, but anyone you give the passphrase to can see the full list.

## Deploying to GitHub Pages

1. Merge this branch into `main`.
2. In the repo: **Settings → Pages → Source: Deploy from a branch → Branch: `main`, folder: `/ (root)`** → Save.
3. The site will be live at `https://<username>.github.io/CrystalSpringsSeating/` after a minute or two.

## Files

- `index.html` — the entire app (vanilla HTML/CSS/JS, fonts loaded from Google Fonts).
- `floor-plan.png` — the supplied original ballroom floor plan shown by the reference viewer.
