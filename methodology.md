# Methodology — Berlin Trust Index

## What we measured

In April 2026, Google Maps began displaying a public notice on business listings in Germany indicating how many customer reviews had been removed following defamation complaints. The notice appears as a banner on the reviews tab of affected listings, showing a count in one of nine ranges: 2–5, 6–10, 11–20, 21–50, 51–100, 101–150, 151–200, 201–250, or 250+. This data is publicly visible to any Maps user.

We systematically collected this disclosure data across venues in central Berlin — restaurants, bars, cafés, hotels, gyms, hair salons, clubs, and other business types.

## Data collection

**Scope:** All venue types returned by Google Maps search within the following Berlin neighbourhoods: Charlottenburg, Friedrichshain, Gesundbrunnen, Kreuzberg, Mitte, Moabit, Neukölln, Prenzlauer Berg, Schöneberg, Tempelhof, Wedding, and Weissensee — broadly corresponding to the area within and immediately adjacent to the S-Bahn Ringbahn.

**Method:** We conducted Google Maps searches using a grid of food type queries (restaurant, bar, café, döner, sushi, vietnamese, etc.) combined with Berlin postcodes, collecting the URLs of all place listings returned. Each unique place was then visited individually to record:

- Place name and Google Maps place ID
- Current star rating
- Total review count
- Removal count (as a range: min and max)
- Removal rate (removed_max ÷ total_reviews)
- Date checked

**Current dataset:** 11,338 unique venues checked across the S-Bahn Ringbahn area, with 1,384 confirmed hits and 44,988+ reviews removed citywide (42 venues at the 250+ cap). Numbers update with each collection run.

## Known limitations and biases

**Search visibility bias.** Our sample is drawn from Google Maps search results, which rank by relevance and prominence. Businesses that appear in search results are disproportionately those with higher review volumes and greater online presence — the same population most likely to actively manage their online reputation. This means our hit rate is not generalisable to all Berlin businesses; it reflects the commercially visible subset.

**The disclosure is specific but limited.** The Google Maps disclosure explicitly states reviews were removed "aufgrund von Beschwerden wegen Diffamierung" — due to complaints regarding defamation. This is distinct from spam removal or policy violations, which use different language. The disclosure does not indicate whether any individual complaint was legally justified or successful in court — only that a complaint was filed and Google processed it.

**The 250+ ceiling.** Google caps disclosed removal counts at "over 250" without providing an exact figure. For venues at this ceiling, removal counts and any derived rates are floors only — the true figures may be substantially higher. Thresholds, indicators, and comparative rankings involving these venues should be interpreted with caution.

**Snapshot data.** This is a point-in-time snapshot. Removal counts change as new complaints are filed and as the annual disclosure window rolls forward. Data is timestamped per venue.

**German locale.** Google Maps served in German (due to Berlin IP geolocation) throughout. All parsing of removal text, tab labels, and review counts was implemented for German-language output.

## How we calculate

**What "total reviews" means.** Google's displayed review count reflects only reviews that are currently visible — reviews removed following a defamation complaint are excluded from that count. This is confirmed by Google's own help documentation: a removed review disappears from the listing and the count decreases accordingly. See: [Add, edit, or delete Google Maps reviews](https://support.google.com/maps/answer/6230175) and [Defamation Removal Notices in Germany](https://support.google.com/contributionpolicy/answer/16997273).

In practice this means: if a venue shows 196 reviews and a banner saying 101–150 were removed, there were originally 297–346 reviews ever submitted, and 196 remain visible today.

**Removal rate.** Removal rate = removed_min ÷ visible_reviews

Where removed_min is the lower bound of the disclosed range (e.g. 101 for "101–150"), and visible_reviews is Google's current displayed count. Using removed_min gives a conservative lower bound — the true rate is somewhere between removed_min/visible and removed_max/visible.

For venues at the 250+ ceiling, removed_min = 250 and the true figure is unknown — rates for these venues are marked as minimums.

**"N removed per visible rating."** For venues where removed_min exceeds the visible count (i.e. more reviews have been removed than currently exist), we express the rate as: removed_min ÷ visible, rounded to one decimal place. This phrasing — e.g. "1.5 removed per visible rating" — conveys that the shadow of removed reviews is larger than what a reader can actually see.

Note: thresholds for indicators, leaderboard rankings, and rate-based comparisons are provisional. We are gathering data first and will determine appropriate cutoffs once the full dataset distribution is understood.

## Social pressure index (MSS)

To test whether removal activity correlates with commercial and social pressure, each venue has been spatially joined to Berlin's Monitoring Soziale Stadtentwicklung (MSS) 2023 dataset — a publicly available index of ~540 Planungsraum zones covering the entire city. The MSS assigns each zone a status index (si_n: 1 = low/vulnerable, 2 = medium, 3 = high/stable) and a dynamic indicator (positive, stable, negative).

This allows grouping of removal data by social pressure band. The MSS is a residential and social indicator, not a direct measure of commercial rents — it is used here as a spatial proxy. Correlation with MSS status does not imply causation.

Data source: [Senatsverwaltung für Stadtentwicklung, Bauen und Wohnen — MSS 2023](https://gdi.berlin.de/services/wfs/mss_2023), open licence.

## Map interface — stat card

The map includes a stat card that updates as you pan. It shows two types of information: data-driven stats calculated from the venues in your current view, and editorial context explaining the legal and commercial mechanisms behind the data.

**Data stats** (shown when enough venues are in view) include: hit rate versus city average, which venue dominates removals in the area, rating gap estimates, clusters of 250+ filers, whether removal activity concentrates in one venue type, and how MSS social-pressure bands compare. These are calculated live from the current viewport and most fire at most once per session.

**Editorial context** cycles in every fourth pan, weighted by how much explanatory work each atom does:

- High priority (shown most often): how Germany's anti-hate-speech law (NetzDG) is used to remove restaurant reviews; that this dataset is legal claims not spam moderation; the zero-text one-star removal; the appeal dead end.
- Medium priority: the cash payment trap (no receipt = no defence); the anonymous complainant problem.
- Lower priority: the commercial review-removal industry; the 250+ disclosure ceiling.

These weightings reflect editorial judgement about what a first-time reader most needs to understand. They can be adjusted as the project develops.

## What the data does and does not show

**Does show:** Which venues have had reviews removed following defamation complaints, and at what scale, as disclosed by Google.

**Does not show:** Whether removed reviews were legitimate, whether the complaints were justified, or whether any specific venue acted wrongfully. A high removal count indicates that defamation complaints were filed and Google processed them — it does not constitute a finding of guilt or bad faith on the part of the venue.

The caveat applies in both directions: a business may have been the victim of a coordinated negative review campaign and legitimately sought removal. The data indicates volume only.

## Reproduction

The results dataset is available at [berlintracker.github.io/berlin.defamation.tracker](https://berlintracker.github.io/berlin.defamation.tracker). The published repository includes `results.json` (hits only), `checked.json` (all checked venues, used for search), and `meta.json` (summary stats). Results are updated on each data collection run. The raw database (including all venues with no removals) is available for researchers and journalists on request.

## Credits

Scraping approach informed by [mb4umi/maps-deleted-reviews](https://github.com/mb4umi/maps-deleted-reviews).
