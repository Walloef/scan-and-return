# Scan & Return

A tiny, dependency-free proof-of-concept checkout ledger. Create QR codes for
**users** and **items**, then scan a user followed by an item to check it out —
scan the item again to return it. All activity is recorded with timestamps.

No build step and no runtime libraries except one vendored MIT QR encoder
(`qrcode.min.js`). Scanning uses the browser-native `BarcodeDetector` API and
data is stored in `localStorage`.

## Run locally

The camera needs a secure context, so serve it (don't open the file directly):

```
python3 -m http.server 8000
```

Then open <http://localhost:8000> in Chrome, Edge, or Safari 17+.

## Hosting

Deployed as static files on GitHub Pages, which serves over HTTPS — that lets a
phone's camera work too. Three tabs: **Scan**, **Setup**, **Ledger**.

## Known limitations (PoC)

- No backend: data lives per-browser in `localStorage` and is not shared across devices.
- `BarcodeDetector` is not available in Firefox.
