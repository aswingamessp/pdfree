# PDFree — every PDF tool, completely free

**One file. No install. No accounts. No uploads. No premium.**

`pdfree.html` is a complete, self-contained PDF productivity platform in a single HTML file
(~6 MB — all engines bundled). Open it in any modern browser (Chrome, Edge, Firefox, Safari)
and all **57 tools** work immediately — even offline.

## Offline behavior (verified)

The app is tested with **all network requests blocked** (fetch/XHR interception, `blob:`/`data:` allowed — they never touch the network). Results:

- ✅ **All 57 tools' core processing runs offline** — verified battery includes rendering standard-font PDFs, merge/split/organize, all editors, Word/Excel/PowerPoint → PDF, PDF → JPG/PNG/TXT/HTML/Markdown/DOCX/XLSX/PPTX, compress, repair, PDF/A, **AES-256 protect & unlock (qpdf WASM is embedded in the file)**, compare, redaction, summarizer, chat/QA, extractors, image & text input.
- ⚠️ Needs network (always disclosed on the tool page):
  - **OCR language packs** — downloaded once per language (~10–15 MB), then browser-cached; OCR fails offline with a clear message.
  - **Translation** — paragraph text goes to MyMemory / your LibreTranslate.
  - **Handwriting fonts** — fetched from Google Fonts; offline it falls back to a system cursive font.
  - **Rare CJK-encoding PDFs** — PDF.js needs its cMap files for a few old CJK-encoded fonts; most PDFs (including all standard-font documents) render fine offline because `useSystemFonts` is enabled.

## Current status (November 25, 2026)

- **Live site:** https://aswingamessp.github.io/pdfree/ (GitHub Pages, HTTPS automatic)
- **Source repo:** https://github.com/aswingamessp/pdfree — push to `main` and Pages republishes automatically
- **New in this build:** "Edit PDF Text" tool (genuine in-place text editing, content streams rewritten with pdf-lib, scanned/password/signature detection) · OCR PDF now exports an editable **Word file** in which detected tables become real Word tables (ruled-grid + position-clustering detection) · PDF to Word rebuilds tables as Word tables for text PDFs too.
- **Fixes (round 2):** OCR now **pre-erases table ruling lines** before recognition (Tesseract otherwise skips ruled tables as line-art — this was the cause of blank table sections); vertical rulings are erased only along their true extent so crossing text is never clipped; table clustering runs in PDF-point space with quality gating (a weak detection degrades to paragraphs — text is never swallowed); Word output preserves **alignment, per-paragraph sizes, headings and reading-order paragraphs**; the text editor now **identifies the real embedded font** (BaseFont + weight/style from the content stream) and prefills family/size/bold/italic; redaction covers are computed from the **actual ink bounding box** on the rendered page (no half-glyph residue); removal produces a **clean blank background** (pixel-verified).
- **Ads are LIVE** — four Adsterra units wired in (placements below), `enabled: true`. A diagnostic page `ad-test.html` is deployed beside the app: it loads two units directly and tells you whether the network is serving, blocked, or pending approval. The Adsterra API key works for read-only reports (stats/domains) via `api3.adsterratools.com/publisher`; unit creation stays dashboard-only.

## Earning from the site (optional advertising)

The app contains a built-in, switched-off ad system. Three non-intrusive banner slots are reserved:

| Slot | Banner size | Where it appears |
| --- | --- | --- |
| `home` | Native banner | Homepage, below Popular tools — visible to every visitor |
| `footer` | 728×90 | Above the footer, desktop (≥861 px) |
| `footerMobile` | 320×50 | Above the footer, phones and tablets (≤860 px) |
| `result` | 300×250 | Above the download list after a tool completes |

To turn ads on: host the file publicly (Netlify Drop / GitHub Pages / Cloudflare Pages), sign up at an ad network (Adsterra or Monetag for a quick start; AdSense for higher rates later), create **banner** units in those sizes, then open `pdfree.html`, find the `ADVERTISEMENTS — EDIT HERE` block near the top, paste the codes into the matching `html: ''` fields, set `enabled: true`, save and re-upload.

- Full walkthrough with verified payout facts: **PDFree_Advertising_Guide.docx / .pdf** (in this folder).
- A ready `privacy-policy.html` ships beside the app — edit its marked placeholders and host it alongside (AdSense requires it).
- Ad banners render in isolated iframes (one per unit) so each unit's scripts stay separate from the others. Adsterra requires non-sandboxed frames to serve — a diagnostic page, `ad-test.html`, is deployed beside the app to verify serving anytime.
- With `enabled: false` (the default) nothing changes: no slots, no requests, offline behavior identical.

## Quick start

1. Open `pdfree.html` (double-click, or serve it anywhere).
2. Drop a file on the homepage or pick a tool.
3. Process and download. Nothing ever leaves your device.

## The privacy model

All processing runs **locally** via WebAssembly / JavaScript engines bundled inside the file:

| Engine | Role |
| --- | --- |
| PDF.js 3.11 | rendering, thumbnails, text extraction, search |
| pdf-lib 1.17 | merge, split, rotate, stamps, forms, crop, resize |
| qpdf (WASM) | AES-256 / AES-128 / RC4 encryption & decryption |
| Tesseract.js 5 | OCR (engine bundled; language pack downloads once, then caches) |
| jsPDF + AutoTable | text typesetting, tables |
| SheetJS | XLSX reading/writing |
| PptxGenJS | PPTX writing |
| JSZip | ZIP outputs |
| html2canvas | HTML → PDF rendering |

The only network use, always disclosed on the tool page:
**OCR language packs** (downloaded once per language, then cached) and **translation**
(paragraph text sent to MyMemory free API or your own LibreTranslate). Optional AI features
can use a **local Ollama** server; without one, PDFree's built-in extractive algorithms are used.

## Feature status (honest inventory)

All 52 tools from the master inventory are implemented and tested (24 internal diagnostics +
45 end-to-end tests with real documents), plus the extra tools. Where a browser engine cannot
match desktop software, the limitation is stated on the tool page and below.

### Organize (8/8)
✅ Merge · ✅ Split (ranges / single pages / fixed groups / half) · ✅ Organize (drag-reorder, rotate,
delete, blank pages, insert pages from other PDFs) · ✅ Extract pages · ✅ Remove pages ·
✅ Reorder · ✅ Rotate (90/180/270, all or range) · ✅ Scan to PDF (camera capture, auto-enhance,
photo import; perspective correction not included)

### Edit & Complete (13/13)
✅ **Edit PDF Text** (real in-place text editing: content-stream text removal with background-redaction fallback, original position/format/colour preserved, multi-page + undo/redo, scanned/encrypted/signed detection, `_edited.pdf` export) ·
✅ Edit PDF (text, images, shapes, arrows, freehand, undo/redo, move/resize/rotate) ·
✅ Add text · ✅ Add images · ✅ Annotate (highlight, draw, shapes, text notes) · ✅ Crop
(visual, per page or all) · ✅ Resize (A3/A4/A5/Letter/Legal/custom, fit/fill/stretch) ·
✅ Page numbers (positions, formats incl. custom pattern, range, skip-first) · ✅ Watermark
(text/image, positions, tiling, opacity) · ✅ Sign (draw / type / upload, saved locally) ·
✅ Fill forms (AcroForm text/checkbox/radio/dropdown) · ✅ Flatten (form fields) ·
✅ Redact (auto-locate terms, boxes, rasterization, metadata strip, post-verification)

⚠️ Note: pages you edit/annotate/sign are re-embedded as high-resolution images; unedited
pages keep full original quality. (True in-place vector editing of existing PDF text is not
feasible with open browser engines.)

### Convert (16/16)
✅ PDF→Word (structure-rebuilt DOCX: headings by font size, paragraphs, page breaks — not a
pixel-perfect clone) · ✅ PDF→Excel (positional table detection → XLSX) · ✅ PDF→PowerPoint
(high-res slide images) · ✅ PDF→JPG / PNG (DPI/quality/range, ZIP) · ✅ PDF→TXT / HTML /
Markdown (tables as pipe tables) · ✅ PDF→PDF/A (image-based PDF/A-2b with XMP; self-declared —
validate with veraPDF for certification) · ✅ Word→PDF (headings, bold/italic, lists, tables,
images) · ✅ Excel→PDF (landscape, per-sheet tables) · ✅ PowerPoint→PDF (images + text boxes
placed from slide geometry; themes/animations not rendered) · ✅ JPG→PDF / PNG→PDF (batch,
fit/full/fill layouts) · ✅ HTML→PDF (browser rendering, paginated) · ✅ TXT→PDF (Unicode via
canvas fallback)

### Optimize & Recover (4/4 + 2 OCR variants)
✅ Compress (lossless repack + extreme/recommended/low/custom image modes, before/after stats,
honest "cannot shrink" report) · ✅ OCR (searchable PDF with invisible text layer + TXT export,
30 languages, page limits) · ✅ Repair (strategy ladder: tolerant rebuild → visual recovery,
recovery log, honest failure report) · ✅ PDF to PDF/A · ✅ PDF→Word with OCR · ✅ PDF→Excel
with OCR

### Security (4/4)
✅ Protect (AES-256/AES-128/RC4 via qpdf WASM, permissions for print/modify/copy, verified) ·
✅ Unlock (correct password required — never cracks; qpdf primary, visual fallback) ·
✅ Compare (page-by-page LCS text diff, colored report, side-by-side preview, HTML export) ·
✅ Secure Redaction (term sweep + boxes, rasterization, metadata strip, full-document
verification with PASS/FAIL)

### Intelligence (8/8)
✅ Summarizer (short/detailed/key points/chapter-wise with page references, TXT+DOCX export,
optional Ollama) · ✅ Translate (MyMemory or your LibreTranslate, side-by-side output, 28
languages) · ✅ Chat with PDF (cited extractive answers, follow-ups, optional local Ollama) ·
✅ Extract text (TXT+DOCX) · ✅ Extract tables (preview + XLSX + CSVs) · ✅ Extract images
(previews, individual or ZIP) · ✅ Question answering (citations, study-oriented) ·
✅ PDF to handwriting (6 Google handwriting fonts, ruled/grid/plain/yellow paper, ink color,
jitter)

### Extra tools (7)
✅ Copy PDF (+metadata strip) · ✅ Metadata viewer & editor · ✅ Bookmarks viewer + TOC page
generator · ✅ Accessibility checker (text layer, /Lang, tagging, title, bookmarks, encryption;
scored report) · ✅ Workflow builder (chain local tools step by step) · ✅ "Use result in
another tool" chaining on every result screen · ✅ Recent files (local IndexedDB, clearable) ·
✅ Shared viewer (zoom, fit, thumbnails, text selection, in-document search, rotate,
full-screen, keyboard) · ✅ Dark/light/auto themes · ✅ Keyboard shortcuts · ✅ Hidden
`#/selftest` diagnostics page

### Not implemented (by design, with reasons)
- **Perspective correction** in Scan to PDF (needs an OpenCV-class engine; capture + enhance +
  combine are included).
- **veraPDF validation** for PDF/A (Java engine; output is self-declared PDF/A-2b).
- **Pixel-perfect PDF→Word/PPTX** (rebuild approach documented on the tool pages).
- **Password cracking** in Unlock PDF (never — authorization required).

## Resource limits (technical, not monetization)

There are no quotas, credits, watermarks or locked features. The only limits are your
device's memory/CPU. Very large documents (500+ pages rasterized) may be slow — the progress
bar shows per-page status and every operation is cancellable.

## Keyboard shortcuts

`/` search tools · `d` toggle dark mode · `g h` home · `g t` all tools · `?` help ·
in the editor: `Ctrl+Z` / `Ctrl+Y` undo-redo, `Del` delete, arrows nudge, `Shift+arrows` nudge ×5.

## Rebuilding / developing

Source lives in `scripts/pdfree/src/` with `node scripts/pdfree/build.js` producing
`download/pdfree.html` (vendor libraries are bundled from `scripts/pdfree/vendor/`).
Test documents: `scripts/pdfree/tests/` (`make_tests.py` regenerates them).
