# PDFree — Free Online PDF Toolkit

A complete, professional PDF toolkit in **one self-contained HTML file**: merge, split, compress, convert, edit, organize, secure, analyze. Every tool runs **locally in your browser** — files are never uploaded anywhere.

**Live site:** https://aswingamessp.github.io/pdfree/

## Highlights

- 100% client-side: merge, split, extract, delete, rotate, reorder pages; compress; PDF ↔ Word/Excel/PowerPoint/JPG; images → PDF; watermark, page numbers, headers/footers; AES-256 encrypt/decrypt; metadata editor; OCR; PDF viewer; text extraction; repair
- Works offline for the core tools — hosting only adds the ability for others to use it online
- No accounts, no watermarks, no server processing

## Repository contents

| File | Purpose |
| --- | --- |
| `index.html` | The entire application (single file) |
| `privacy-policy.html` | Privacy policy page (edit the marked placeholders before serious use) |
| `docs/PDFree_Advertising_Guide.pdf` | Step-by-step monetization guide (also provided as `.docx`) |

## Updating the site

Edit or replace `index.html`, then push to `main` — GitHub Pages republishes automatically (check the **Actions** tab; first publish takes a minute or two).

## Earning from the site (advertising)

The app contains a built-in, switched-off ad system with three non-intrusive banner slots:

| Slot | Banner size | Where it appears |
| --- | --- | --- |
| `sidebar` | 160×600 | Fixed right edge, wide desktop screens only (≥1700 px) |
| `footer` | 728×90 | Above the footer, every page |
| `result` | 300×250 | Above the download list after a tool completes |

**Remaining steps to turn ads on:**

1. In the **Adsterra dashboard → Websites**, add `https://aswingamessp.github.io/pdfree/` and wait for approval (usually quick).
2. Under **Ad Units**, create **Banner** units in the three sizes above (never popup/popunder/social-bar formats — they disturb visitors).
3. Copy each unit's HTML code and either paste it to your assistant in chat ("add these ads") or edit `index.html` yourself: find `ADVERTISEMENTS — EDIT HERE` near the top, paste each code into the matching `html: ''` field, set `enabled: true`, commit.
4. Check the live site, then watch earnings in the Adsterra dashboard; payouts start at $5 depending on method and are sent automatically twice a month.

The banners render in sandboxed iframes — ad scripts cannot read the site or the files visitors process. With `enabled: false` (the current default) nothing changes: no slots, no requests, offline behavior identical.

> Security note: never put an Adsterra **API key** into `index.html` — it is a secret; only the public banner code belongs in the page. Ad networks' own ad code is safe to embed.
