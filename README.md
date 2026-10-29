# Scan & Return

A tiny, dependency-free proof-of-concept checkout ledger. Create QR codes for
**users** and **items**, then scan a user followed by an item to check it out —
scan the item again to return it. All activity is recorded with timestamps.

No build step and no runtime CDNs — just two vendored MIT single-file libraries:
`qrcode.min.js` (generates codes) and `jsQR.js` (decodes camera frames). Data is
stored in `localStorage`.

## Run locally

The camera needs a secure context, so serve it (don't open the file directly):

```
python3 -m http.server 8000
```

Then open <http://localhost:8000> in any modern browser.

## Hosting

Deployed as static files on GitHub Pages, which serves over HTTPS — that lets a
phone's camera work too. Three tabs: **Scan**, **Setup**, **Ledger**.

## Shared sync (optional)

Open the **Sync** tab to share the catalog and ledger across devices via a free
[jsonbin.io](https://jsonbin.io) bin. One-time: sign up, copy your Master Key, press
**Create new bin** on the first device, then **Connect** on others with the same key +
Bin ID. When connected, jsonbin is the source of truth (read-modify-write on each change,
with a 5s poll on the Ledger tab); otherwise everything stays in `localStorage`.

Keys are stored only in each browser's `localStorage` — they are never committed to this
repo. Anyone you give the key + Bin ID to can read and change the data, so treat it as a
demo-grade store.

## Known limitations (PoC)

- Without sync configured, data lives per-browser in `localStorage` and is not shared.
- Sync uses whole-document last-write-wins; simultaneous edits on two devices can race.
