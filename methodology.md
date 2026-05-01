# Methodology — Berlin Trust Index

## What we measured

Google Maps displays a public notice on German business listings stating how many customer reviews have been removed following defamation complaints. The notice appears on the reviews tab of affected listings and shows a count in one of nine bands:

2–5, 6–10, 11–20, 21–50, 51–100, 101–150, 151–200, 201–250, or 250+.

We collect this data across central Berlin. We do not collect, store, or reproduce the content of any removed review. We do not collect or publish the names of reviewers, complainants, or law firms acting on individual cases.

## Collection

**Scope.** All venue types returned by Google Maps search within Charlottenburg, Friedrichshain, Gesundbrunnen, Kreuzberg, Mitte, Moabit, Neukölln, Prenzlauer Berg, Schöneberg, Tempelhof, Wedding, and Weissensee — broadly the area within and immediately adjacent to the S-Bahn Ringbahn.

**Method.** Google Maps searches using a grid of category queries (restaurant, bar, café, döner, sushi, vietnamese, etc.) combined with Berlin postcodes. Each unique place returned was visited individually. For each listing we recorded: place name, Google Maps place ID, current visible star rating, total visible review count, the band shown on Google's removal notice (if any), and the date the listing was checked.

Live counts (venues checked, hits, total removals) are in `meta.json` and update with each collection run.

**Locale.** Google Maps was served in German throughout. Parsing of removal text, tab labels, and review counts was implemented for German-language output.

## Calculations

**What "total reviews" means.** Google's displayed review count includes only reviews currently visible. Reviews removed following a defamation complaint are excluded from that count, per Google's own documentation. A venue showing 196 reviews with a banner indicating 101–150 removals therefore had 297–346 reviews ever submitted and has 196 visible today.

**Removal rate.** removed ÷ (visible + removed). The proportion of all reviews ever submitted that have been removed. The denominator is the estimated total ever submitted.

**Which figure we display.** Citywide totals, per-venue figures, and all sorting or threshold logic use the median of each band. Per-venue displays show the band itself ("101–150 removed") alongside the median, so the disclosed range is always visible to the reader.

**Floor venues (250+).** Google caps disclosed counts at "over 250" without an exact figure. For these venues we treat the lower bound as 250. All derived figures involving floor venues are minimums; the true counts are not disclosed and may be substantially higher.

**"N removed per visible rating."** Where the disclosed lower bound exceeds the visible review count, we display lower_bound ÷ visible (e.g. 1.5 removed per visible rating). This expresses that more reviews have been removed than currently appear on the listing.

Thresholds for indicators, rankings, and rate-based comparisons are provisional and may be revised as the dataset stabilises.

## Social pressure index (MSS)

Each venue is spatially joined to Berlin's Monitoring Soziale Stadtentwicklung (MSS) 2023 dataset — a public index covering ~540 Planungsraum zones. The MSS assigns each zone a status index (1 = vulnerable, 2 = medium, 3 = stable) and a dynamic indicator (positive, stable, negative).

We use it as a spatial proxy to test whether removal activity concentrates by social pressure band. MSS is a residential and social indicator, not a direct measure of commercial rents. Correlation does not imply causation.

Source: Senatsverwaltung für Stadtentwicklung, Bauen und Wohnen — MSS 2023, open licence.

## Limitations

**Search visibility bias.** The sample is drawn from Google Maps search results, which rank by prominence. Visible businesses skew toward higher review volumes and active online presence. The hit rate is not generalisable to all Berlin businesses; it reflects the commercially visible subset.

**Disclosure scope.** Google's notice specifies removals "aufgrund von Beschwerden wegen Diffamierung" — defamation complaints. This is distinct from spam or policy-violation removals, which Google labels separately. The disclosure indicates only that a complaint was filed and processed by Google; it does not indicate whether the complaint was legally tested or judicially upheld.

**The 250+ ceiling.** For floor venues, all counts and derived figures are minimums only.

**Snapshot.** Counts change as complaints are filed and as Google's 365-day disclosure window rolls forward. Each record is timestamped.

## What the data does and does not show

The data shows which Berlin venues have had reviews removed following defamation complaints, at what volume, as disclosed by Google.

It does not show whether removed reviews were legitimate, whether complaints were justified, or whether any venue acted wrongfully. A high removal count means complaints were filed and Google processed them. It is not a finding of fault on the part of any venue.

The same caveat applies in reverse: a venue may have been the target of fake or coordinated negative reviews and legitimately sought removal. The data shows volume only.

## Source attribution

Every figure on this site originates from public disclosures made by Google on its own Maps platform. We arrange that data geographically. No private data is collected, stored, or displayed. No information is derived from sources other than Google's own disclosures and the public MSS dataset described above.

## Corrections and right of reply

We aim to represent Google's disclosures accurately. If a venue, individual, or other party believes their data is incorrectly represented, contact us via the site. Verifiable corrections are made promptly.

## Reproducibility

The site is hosted at `berlintrustindex.com`. The repository contains:

- `results.json` — venues with at least one disclosed removal
- `checked.json` — all checked venues, used for search
- `meta.json` — summary statistics

The raw database, including venues with no removals, is available to researchers and journalists on request.

Scraping approach informed by [mb4umi/maps-deleted-reviews](https://github.com/mb4umi/maps-deleted-reviews).
