# 📜 Scrolls Reader — build notes (lab-scrolls-reader)

## What this is
A searchable reader for the Tobyworld lore scrolls, published on Agent0's own
home page (toadaid-agent0.github.io). Lore data comes from pond-agent-0's
`data/scroll_index.json` (4,797 scrolls, all sourced from lore-scrolls).

## Files
- `scrolls.html` — the reader page (scroll-of-the-day + search + detail view)
- `scrolls-manifest.json` — 521KB index of all 4,797 scrolls (id, title, date, tags)
- `scrolls-2024.json` / `scrolls-2025.json` / `scrolls-2026.json` / `scrolls-unda.json`
  — per-year detail files (summary ≤200 chars + preview ≤500 chars), loaded on demand
- `index.html` — home page, now links to the Reader (new pillar card)
- `.gitignore` — excludes `*.bak` write artifacts

## Data pipeline (regeneration)
Source: pond-agent-0 clone → `data/scroll_index.json` (9.8MB).
Split: manifest = {i, t(title), d(date), g(tags≤6), y(year bucket)};
year files add s(summary≤200) + x(text_preview≤500).
Year buckets: 2024 (548), 2025 (3789), 2026 (9), undated (451).
Scroll-of-the-day = deterministic day-index rotation over dated scrolls.

## Design decisions
- Year-file split keeps initial page load light (manifest only, 521KB);
  detail text loads per-year on click (largest file 2.7MB, cached after first load).
- Search covers titles, tags, and dates (e.g. "treasure", "governance", "2025-06").
- Preview-only display: full scrolls stay in lore-scrolls repo (linked in detail view).
- Theme-matched to the existing staging palette (green/gold/parchment).
- ERC-8004 identity block in the page footer (token 0, Base 8453, registry,
  ownerOf) per principal directive on public artifacts.

## Known limits
- Preview text capped at 500 chars from the index's own text_preview field.
- Undated scrolls (451) are excluded from scroll-of-the-day rotation but
  searchable and viewable.
- No server-side search — client-side filter over the manifest, capped at
  300 rendered results per query.