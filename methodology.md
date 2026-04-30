# Methodology — Berlin Trust Index

## What we measured

In April 2026, Google Maps began displaying a public notice on German business listings stating how many customer reviews had been removed following defamation complaints. The notice appears on the reviews tab of affected listings and shows a count in one of nine bands: 2–5, 6–10, 11–20, 21–50, 51–100, 101–150, 151–200, 201–250, or 250+.

We collected this disclosure data across central Berlin.

## Collection

**Scope.** All venue types returned by Google Maps search within Charlottenburg, Friedrichshain, Gesundbrunnen, Kreuzberg, Mitte, Moabit, Neukölln, Prenzlauer Berg, Schöneberg, Tempelhof, Wedding, and Weissensee — broadly the area within and immediately adjacent to the S-Bahn Ringbahn.

**Method.** Google Maps searches using a grid of category queries (restaurant, bar, café, döner, sushi, vietnamese, etc.) combined with Berlin postcodes. Each unique place returned was visited individually. For each, we recorded: place name, Google Maps place ID, current star rating, total visible review count, removal band (min and max), removal rate, and date checked.

Live counts (venues checked, hits, total removals) are published in `meta.json` and update with each collection run.

**Locale.** Google Maps served in German throughout. Parsing of removal text, tab labels, and review counts was implemented for German-language output.

## Calculations

**What "total reviews" means.** Google's displayed review count includes only reviews currently visible. Reviews removed following a defamation complaint are excluded from that count, per Google's own documentation. A venue showing 196 reviews with a banner indicating 101–150 removals therefore had 297–346 reviews ever submitted and has 196 visible today.

**Removal rate.** removed ÷ (visible + removed) — the proportion of all reviews ever submitted that were removed. The denominator is the estimated total ever submitted.

**Which figure we display.** Citywide totals use the lower bound of each band. Per-venue figures show the band itself ("101–150 removed"). Where a single number is required for sorting or threshold logic, we use the median of the band.

**Floor venues (250+).** Google caps disclosed counts at "over 250" without an exact figure. For these venues we treat removed_min = 250. All derived figures involving floor venues are minimums; the true counts may be substantially higher.

**"N removed per visible rating."** Where removed_min exceeds the visible review count, we display removed_min ÷ visible (e.g. 1.5 removed per visible rating). This conveys that the shadow of removed reviews is larger than what is currently visible on the listing.

Thresholds for indicators, rankings, and rate-based comparisons are provisional and will be revisited as the dataset stabilises.

## Social pressure index (MSS)

Each venue is spatially joined to Berlin's Monitoring Soziale Stadtentwicklung (MSS) 2023 dataset — a publicly available index covering ~540 Planungsraum zones. The MSS assigns each zone a status index (1 = vulnerable, 2 = medium, 3 = stable) and a dynamic indicator (positive, stable, negative).

We use it as a spatial proxy to test whether removal activity concentrates by social pressure band. MSS is a residential and social indicator, not a direct measure of commercial rents. Correlation does not imply causation.

Source: Senatsverwaltung für Stadtentwicklung, Bauen und Wohnen — MSS 2023, open licence.

## Limitations

**Search visibility bias.** The sample is drawn from Google Maps search results, which rank by prominence. Visible businesses skew toward higher review volumes and active online presence — the same population most likely to manage their reputation. The hit rate is not generalisable to all Berlin businesses; it reflects the commercially visible subset.

**Disclosure scope.** The Google notice specifies removals "aufgrund von Beschwerden wegen Diffamierung" — defamation complaints. This is distinct from spam or policy-violation removals, which use different language. The disclosure indicates that a complaint was filed and processed; it does not indicate whether the complaint was legally justified.

**The 250+ ceiling.** For floor venues, counts and derived rates are minimums only.

**Snapshot.** Counts change as complaints are filed and as Google's 365-day disclosure window rolls forward. Data is timestamped per venue.

## What the data does and does not show

The data shows which venues have had reviews removed following defamation complaints, at what scale, as disclosed by Google.

It does not show whether removed reviews were legitimate, whether complaints were justified, or whether any venue acted wrongfully. A high removal count means complaints were filed and Google processed them. It is not a finding of guilt.

The caveat applies in both directions: a venue may have been the target of a coordinated negative-review campaign and legitimately sought removal. The data shows volume.

## Reproduction

Published at `berlintrustindex.com`. The repository contains:

- `results.json` — hits only (venues with at least one disclosed removal)
- `checked.json` — all checked venues, used for search
- `meta.json` — summary statistics

The raw database, including venues with no removals, is available to researchers and journalists on request.

Scraping approach informed by [mb4umi/maps-deleted-reviews](https://github.com/mb4umi/maps-deleted-reviews).
