# papers-wordcloud (GitHub Pages package)

This is a ready-to-push package for an **interactive word cloud** that auto-loads up to **20 papers** from `papers.json`.
- Click a word in the cloud → the right panel lists all matching papers (with PDF/Link buttons).
- Works great when hosted on **GitHub Pages** and embedded into **Google Sites** via *Embed → By URL*.

## Folder structure
```
papers-wordcloud/
├─ index.html                  # main page (loads papers.json)
├─ papers.json                 # list of up to 20 papers (edit this)
├─ vendor/
│  └─ pdfjs/
│     ├─ pdf.min.js           # (add these two files locally, recommended)
│     └─ pdf.worker.min.js
└─ pdf/
   ├─ your-paper-1.pdf
   └─ your-paper-2.pdf
```

> **Tip:** Add an empty file named `.nojekyll` at repo root so GitHub Pages serves the `vendor/` path as-is. (Already included in the ZIP.)

## Step-by-step

1) **Add pdf.js locally** (recommended)
   - Get from npm `pdfjs-dist` (files under `build/`) or download manually:
     - `vendor/pdfjs/pdf.min.js`
     - `vendor/pdfjs/pdf.worker.min.js`
   - The `index.html` prefers these local files. If missing, it falls back to CDN.

2) **Put your PDFs** in the `pdf/` folder and update `papers.json`.
   - Use **relative paths** in `papers.json`, e.g. `"pdf": "./pdf/paper01.pdf"`.
   - If a PDF is hosted on another domain (and fails due to CORS), add a `"text"` field (abstract/fulltext) so the app can skip fetching that PDF.

3) **Commit & push to GitHub** (repo name example: `papers-wordcloud`).

4) **Enable GitHub Pages**
   - Repo → Settings → Pages → Source: *Deploy from a branch* (main, `/`).
   - Your site appears at `https://<your-username>.github.io/papers-wordcloud/`.

5) **Embed in Google Sites**
   - Sites → Insert → Embed → *By URL* → paste your GitHub Pages URL.
   - Resize iframe (height ~1000–1200 px).

## Updating the list
Just edit `papers.json` and push again. No need to touch `index.html`.

### papers.json format
Each entry supports:
```jsonc
{
  "title": "Paper title",
  "url": "https://publisher-or-lab-page",
  "pdf": "./pdf/paper-file.pdf",
  "text": "Optional pre-extracted text to skip fetching the PDF"
}
```
- If `text` is present and reasonably long, the app uses it directly.
- Otherwise it will try to fetch and extract text from `pdf` using pdf.js.

## Troubleshooting
- **pdf.js failed to load**: Add local files in `vendor/pdfjs/`, or check network/CDN restrictions.
- **CORS error when fetching PDFs**: Host PDFs under the same GitHub Pages origin (e.g., `./pdf/...`) or use `text` field.
- **Mixed content blocked**: Only use **https** links.
- **Nothing shows**: Open DevTools (F12) → Console. Check errors and `Network` tab to confirm `papers.json` is loading.

Enjoy!
