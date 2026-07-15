# Wong–Roa Wedding Seating Chart

Mobile-friendly seating chart for the Wong–Roa wedding — Emerald Ballroom, Crystal Springs Resort, November 1, 2026.

Tap a table on the floor plan to see who's seated and add guests from the master list. Everything is a single `index.html` — no build step, no backend.

## Features

- **Floor plan** — 16 round tables laid out to match the Emerald Ballroom's real floor plan (a staggered 8-table wing plus a block of 8 in the main room). A gold ring around each table shows how full it is; a table turns solid emerald when full. A "View original design" button pops up the venue's floor-plan drawing (`floorplan.png`) for reference.
- **Guest picker** — bottom sheet grouped by family group, searchable, only shows unseated guests.
- **Guest list** — full roster with bride/groom/mutual color dots, Maybe/Unlikely tags, search, and a "hide unlikely" filter. Tap a guest's table badge to unseat them.
- **Table capacity** — 10 seats by default, adjustable per table up to 14.
- **Autosave** — every change is saved to the browser's `localStorage` (key `wongroa-seating-v1`).
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
- `floorplan.png` — the venue's original Emerald Ballroom floor-plan drawing, shown in the "View original design" popup.
