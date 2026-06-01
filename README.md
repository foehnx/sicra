# [The Better ICRA Paper Schedule](https://foehnx.github.io/sicra)

> ⚠️ **Heads up:** this site may be taken offline at any point after ICRA 2026. If you've starred a bunch of papers, **Export** your favorites before the conference wraps up — the JSON file works forever and can be re-imported into any future copy of the page.

Live at https://foehnx.github.io/sicra

A single-page paper explorer for ICRA 2026. The official program viewer at [ras.papercept.net](https://ras.papercept.net/conferences/conferences/ICRA26/program/) makes it hard to scan a few thousand papers, so this is a nicer frontend on top of the same data.

By [Philipp Foehn](https://www.linkedin.com/in/foehn/) from [Skydio](https://www.skydio.com/careers).

## Run it

Any static file server works — the whole thing is `index.html` + `data.json.gz`.

```bash
python3 -m http.server 8765
# open http://localhost:8765/index.html
```

Or just drop the two files anywhere that serves static content (GitHub Pages, Cloudflare Pages, S3, etc.).

## What's in it

- **Fast list of all 2,951 papers** — virtualized so it stays smooth on mobile.
- **Search** across title, authors, topics, room, session, and university. Toggle "Search abstracts" to also search the abstract text. Multi-word queries are AND-token substring matches (`deep rein` finds papers with both `deep` and `rein` somewhere).
- **Autocomplete** in the search box: focus the empty input to browse every keyword in the conference, ordered by frequency; start typing to filter both keywords and author names. Pick one with arrow keys + Enter (or click), it replaces just the last token.
- **Day filter chips** — Tue / Wed / Thu.
- **Expandable rows** with the full title, full author list with affiliations, all topics, abstract, and PDF link when one is published.
- **Favorites** — star anything to keep it. Stored in your browser (`localStorage`); nothing leaves your device unless you choose to share.
- **Favorites view** groups your starred papers by day with sticky day headers, color-coded, and on first open it scrolls to today in `Europe/Vienna` time.
- **Import / Export** favorites as a small JSON file. Import is additive (union with what you already have), not destructive.
- **Share link** — in favorites mode, copy a URL that embeds your favorites in the hash. Open it on another device or send it to a colleague and the favorites get merged in.
- **Deep links**: `#favorites` opens favorites mode, `#day=Tuesday` preselects a day, `#paper=<id>` scrolls to and expands a specific paper.
- **Dark / light mode** follows your OS.
- **Keyboard**: `/` focuses search, `Esc` clears search or collapses an expanded row.

## Data

The paper data is **scraped once** from the public papercept program pages (the `ContentListWeb_*.html` pages, the author index, and the keyword index) into `data.json.gz`. The page does **not** keep hitting papercept — it just loads that single static file. The scraper (`scrape.py`) is included if you ever want to refresh it manually, but day-to-day use is fully self-contained.

This means: if the conference organizers update the program after the initial scrape, you won't see those changes until someone re-runs the scraper and redeploys.

## Caveats

This is a quick weekend-conference hack. Bugs are expected and might not get fixed. There's no support, no warranty, no roadmap. If something is broken on your device, sorry — try a different browser or open the official program. If something is really broken, feel free to file an issue but treat it as a lottery ticket.

PDF links are mostly empty right now because the conference hasn't happened yet and the papers haven't been published. The button only shows when there's actually a link to open.

## Built with Claude

The whole thing — scraper, frontend, virtualization, autocomplete, the lot — was vibe-coded in Cursor with Claude doing the heavy lifting. Treat it accordingly: code style is whatever felt right at the moment, comments are sparse, and the architecture is "single HTML file with inline everything." Works for the use case.
