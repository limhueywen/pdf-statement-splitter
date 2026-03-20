# PDF Statement Splitter

A browser-based tool that splits a combined PDF statement into individual files — one per account code. No installation, no server, no data upload.

**Created by [Lim Huey Wen](https://github.com/limhueywen)**

---

## What it does

Accounts receivable teams often receive a single bulk PDF containing statements for every customer. This tool reads that file, detects each account automatically, and produces a separate downloadable PDF per account.

**Example:** A 12-page PDF with accounts `102001`, `102002`, `108004` becomes three individual files:
- `102001.pdf`
- `102002.pdf`
- `108004.pdf`

---

## How to use

1. Open `pdf-splitter.html` in any modern browser — no setup required
2. Drop your combined PDF onto the upload area
3. Click **Scan & Detect Accounts** — the tool reads every page and finds account codes automatically
4. Review the detected account list to confirm it looks correct
5. Click **Split into Separate PDFs**
6. Download files individually by clicking each card, or click **Download ZIP** for everything at once

---

## Features

- **Auto-detection** — tries a comprehensive list of known label patterns (`Account No :`, `Acc No:`, `Customer ID:`, etc.) and falls back to a heuristic scan if none match
- **Manual override** — if auto-detection misses, use the Edit Pattern field to enter the exact label text and character format
- **Multi-page accounts** — pages belonging to the same account are automatically grouped into a single output file
- **Fully local** — all processing happens in the browser using PDF.js and pdf-lib; no data is sent to any server
- **ZIP download** — download all split files in one archive

---

## Compatibility

Works in all modern browsers (Chrome, Edge, Firefox, Safari). No installation or internet connection required after the page loads.

| Dependency | Version | Purpose |
|---|---|---|
| [PDF.js](https://mozilla.github.io/pdf.js/) | 3.11.174 | Extract text from PDF pages |
| [pdf-lib](https://pdf-lib.js.org/) | 1.17.1 | Create and write output PDF files |
| [JSZip](https://stuk.github.io/jszip/) | 3.10.1 | Package all files into a ZIP archive |

All loaded via CDN — no build step needed.

---

## Pattern detection

The tool tries these label patterns in order, picking the one that matches the most pages:

```
Account No :    Account No:    Account No.    Account No
Acc No :        Acc No:        Account Number:
Customer No:    Customer ID:   Cust No:       Invoice No:
```

If none match, a heuristic scan looks for any `LABEL : NUMBER` pattern and picks the most frequent one.

**Manual override:** On the Review screen, click **Edit pattern** and enter:
- **Label** — the exact text before the code, e.g. `Account No :`
- **Code characters** — `0-9` for numbers only, `A-Za-z0-9` for alphanumeric, `A-Z0-9\-` for codes with dashes

---

## File structure

```
pdf-splitter.html    # The entire application — single self-contained file
README.md
```

---

## License

MIT — free to use, modify, and distribute.

---

*PDF Statement Splitter — Lim Huey Wen — https://github.com/limhueywen*
