# Chicago 311 Pothole Response Times

**Do pothole repair times in Chicago vary with neighborhood income? An observational analysis of 76k 311 requests.**

Across Chicago's 77 community areas, lower-income neighborhoods show modestly longer pothole repair times. The pattern persists after controlling for request volume — so it isn't just a backlog effect — but it's weak: income accounts for only about 9% of the variation. This is an observed association, not evidence of causation; unmeasured factors like road condition and pothole severity likely matter more. I framed the project around separating *differences in neighborhood conditions* from *differences in measured response times* — a methodological question, not a policy claim.

## Data
- **311 pothole requests** (Chicago Data Portal): ~76k, 2020–2025, filtered to "Pothole in Street."
- **Socioeconomic indicators by community area** (Chicago Data Portal, 2008–2012): per-capita income and hardship index, joined on community-area number.

Income data predates the pothole data by ~a decade, so it serves as a proxy for *relative* neighborhood wealth; areas that changed substantially may be misclassified.

## Method
1. Response time = closed − created date, per request.
2. Aggregated to one row per community area, using the **median** (the distribution is right-skewed).
3. Tested the most obvious alternative explanation first: **request volume** (busier areas may build backlogs).
4. Regressed response time on **income + volume together**, isolating income's association with volume held constant.
5. Robustness check: re-ran using the hardship index instead of income — same direction.

## Findings
The raw spread is large — the slowest community area (Kenwood, ~64 days) shows repair times roughly **13x** longer than the fastest (the Loop, ~5 days).

Volume doesn't account for most of it: request volume correlates only weakly with response time (~0.33, ~**11%** of the variation). Income shows a negative association with response time (**−0.25**) that **persists after controlling for volume** — but it's weak, accounting for only ~**9%**. Income is a measurable but minor factor; most of the variation is associated with something else.

## Why the Simple Story Doesn't Hold
The extremes don't fit a clean "lower-income = slower" pattern: Kenwood (slow) is mixed-to-affluent, O'Hare (slow) is an airport rather than a residential area, and some lower-income areas like West Englewood and Roseland are among the *fastest*. This is consistent with income accounting for so little of the variation — at the neighborhood level, unmeasured factors like land use and road infrastructure appear more relevant than wealth.

## Charts
![Scatter of per-capita income vs. median pothole response time](scatter_income_vs_response.png)
*Income vs. median response time, one point per community area. The downward trend line shows the association; the loose scatter shows how much it leaves unexplained.*

![Bar chart of fastest and slowest community areas](bar_fastest_slowest.png)
*The 10 fastest and 10 slowest community areas — the ~13x spread.*

## Limitations & Next Steps
- **Duplicates:** repeated reports of one pothole appear as separate rows; not deduplicated, which may affect volume counts.
- **Open requests:** ~2k requests had no close date and are excluded, which may shift response-time estimates.
- **Income vintage & outliers:** 2008–2012 income figures; non-residential areas like O'Hare aren't directly comparable to neighborhoods.

**Next steps (analysis):** deduplicate repeated reports, incorporate current income data, and add road-infrastructure variables to better account for physical conditions.
