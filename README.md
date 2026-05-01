# Berlin Trust Index

**Map → [berlintrustindex.com](https://berlintrustindex.com)**

---

## Can you trust Google Maps?

Google publishes a notice on German business listings disclosing how many customer reviews have been removed following defamation complaints. The notice gives a count in bands: 2–5, 6–10, 11–20, 21–50, 51–100, 101–150, 151–200, 201–250, or 250+.

This project collects those disclosures across Berlin and presents them on a map.

## Current dataset

Live numbers in [`meta.json`](./meta.json). At time of writing: ~11,300 venues checked, ~1,400 with at least one disclosed removal, ~45,000 reviews removed across Berlin. 42 venues sit at the 250+ disclosure cap; their actual totals are not disclosed by Google and are unknown.

## What this repo contains

| File | |
|---|---|
| `index.html` | Map (Leaflet + OSM tiles) |
| `results.json` | Venues with at least one disclosed removal |
| `checked.json` | All checked venues, used for site search |
| `meta.json` | Summary statistics |
| `methodology.md` | How the data was collected |

No scraper code or raw database is included in this repository.

## What the data shows — and what it does not

The data shows which Berlin venues have had Google reviews removed following defamation complaints, at what volume, as disclosed by Google itself.

It does not show whether removed reviews were legitimate, whether complaints were justified, or whether any venue acted wrongfully. A high removal count means defamation complaints were filed and Google processed them. It is not a finding of fault.

A venue may equally have been the target of fake or coordinated negative reviews and legitimately sought removal. The data shows volume only.

## What the project does not do

- We do not name reviewers, complainants, or law firms acting on individual cases.
- We do not reproduce the content of removed reviews.
- We do not collect or display data Google has not itself made public.

## Corrections and removal requests

If a venue believes its data is incorrectly represented, please contact us via the site. Verifiable corrections are made promptly. Removal requests are reviewed against Google's current disclosure for the listing.

## Credits

Scraping approach informed by [mb4umi/maps-deleted-reviews](https://github.com/mb4umi/maps-deleted-reviews).

## Legal

All data on this site originates from public disclosures made by Google on its own Maps platform. This project arranges that public data geographically. No private data is collected, processed, or shown.
