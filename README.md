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

## Known limitations (PoC)

- No backend: data lives per-browser in `localStorage` and is not shared across devices.
