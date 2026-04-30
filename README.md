# Berlin Trust Index

**Live map → [berlintracker.github.io/berlin.defamation.tracker](https://berlintracker.github.io/berlin.defamation.tracker/)**

---

In early 2026, Google Maps began displaying a public notice on German business listings showing how many customer reviews had been removed following defamation complaints. The notice appears as a banner on the reviews tab, showing a count in ranges: *2–5, 6–10, 11–20, 21–50, 51–100, 101–150, 151–200, 201–250, 250+*.

This project systematically collects that disclosure data across venues in Berlin and publishes the results as an interactive map.

## Current dataset (as of April 2026)

- **11,338 venues checked** across Berlin's inner districts
- **1,384 venues** with confirmed removals (~12% hit rate)
- **44,988+ reviews removed** citywide (42 venues at the 250+ disclosure cap — actual totals unknown)

Numbers update with each data collection run. The live map reflects the most recent exported dataset.

## What the data shows

The data shows that defamation complaints were filed and Google processed them. It does not imply the complaints were justified or unjustified. Many venues on this map are well-regarded places that used a legal system available to anyone. The data shows volume only.

## This repository

This repo contains only the published outputs — no scraper code, no raw database.

| File | Description |
|------|-------------|
| `index.html` | Interactive map (Leaflet + OpenStreetMap tiles) |
| `results.json` | Hits-only export — venues with confirmed removals |
| `meta.json` | Summary stats (total checked, hit count, etc.) |
| `checked.json` | All checked venues with zero removals (for search) |
| `methodology.md` | How the data was collected |

## Methodology

See [methodology.md](methodology.md) for full details on how venues were identified, how removal counts were read, and what the data does and doesn't represent.

## Credits

Scraping approach informed by [mb4umi/maps-deleted-reviews](https://github.com/mb4umi/maps-deleted-reviews).

## Legal

All data is publicly disclosed by Google on their Maps platform. This project surfaces existing public disclosures. Framing is factual and explicitly non-accusatory throughout. No complainant names, law firm names, or case details are captured or published.
