# Berlin Trust Index

**Live map → [berlintrustindex.com](https://berlintrustindex.com)**

---

In early 2026, Google Maps began displaying a public notice on German business listings showing how many customer reviews had been removed following defamation complaints. The notice gives a count in bands: 2–5, 6–10, 11–20, 21–50, 51–100, 101–150, 151–200, 201–250, 250+.

This project collects that data across Berlin and publishes it as an interactive map.

## Current dataset

Live numbers in [`meta.json`](./meta.json). At time of writing: ~11,300 venues checked, ~1,400 with confirmed removals, ~45,000 reviews removed citywide. 42 venues sit at the 250+ disclosure cap — their actual totals are unknown.

## Repo contents

| File | |
|---|---|
| `index.html` | Map (Leaflet + OSM tiles) |
| `results.json` | Venues with confirmed removals |
| `checked.json` | All checked venues, used for search |
| `meta.json` | Summary stats |
| `methodology.md` | How the data was collected |

No scraper code or raw database is published here.

## What the data shows

That defamation complaints were filed and Google processed them. Not whether the complaints were justified. Many venues on the map are well-regarded places using a legal route available to anyone. The data shows volume.

## Credits

Scraping approach informed by [mb4umi/maps-deleted-reviews](https://github.com/mb4umi/maps-deleted-reviews).

## Legal

All data is publicly disclosed by Google on Maps. This project surfaces existing public disclosures. No complainant names, law firm names, or case details are captured or published.
