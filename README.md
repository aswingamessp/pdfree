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

The app ships with a built-in ad system — four non-intrusive slots, currently **live with Adsterra**:

| Slot | Banner size | Where it appears |
| --- | --- | --- |
| `home` | Native banner | Homepage, below Popular tools — visible to every visitor |
| `footer` | 728×90 | Above the footer, desktop (≥861 px) |
| `footerMobile` | 320×50 | Above the footer, phones and tablets (≤860 px) |
| `result` | 300×250 | Above the download list after a tool completes |

**Ads are live (Nov 25, 2026).** The four Adsterra unit codes are wired into `index.html`
(`AD_CONFIG`, `enabled: true`) and deployed to the live site. To swap or add a unit later:
create it in the Adsterra dashboard, replace the matching `html` string in `AD_CONFIG`,
commit — GitHub Pages republishes automatically. Keep banner/native formats only (never
popup/popunder/social-bar — they disturb visitors and hurt the site).

The banners render in sandboxed iframes — ad scripts cannot read the site or the files visitors process. With `enabled: false` (the current default) nothing changes: no slots, no requests, offline behavior identical.

> Security note: never put an Adsterra **API key** into `index.html` — it is a secret; only the public banner code belongs in the page. Ad networks' own ad code is safe to embed.
