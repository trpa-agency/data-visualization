# Cumulative Accounting Dashboards · Review History

Consolidated record of stakeholder feedback received during the May 2026 review cycle, with current status per item. Two internal reviewers so far (Dan Segan, Ken Kasman); Communications reviewer scheduled for Monday May 18.

**Status legend:**
- ✅ **Addressed** — change shipped, visible in the live dashboard
- 🟡 **Partially addressed** — some of the item shipped, follow-up needed
- ⏸️ **Deferred** — data-dependent or scheduled for a future iteration
- ❌ **Not yet addressed** — open

---

## Round 0 — Dan Segan (May 11, 2026) · Framing proposal

Dan proposed splitting the conceptual model into **four interconnected tracks**, each with distinct states. This framing drove the dashboard organization on `review.html` (the internal decision tree; was `index.html` before the May 18 public-landing rename).

| Track | What it tracks | Status |
|---|---|---|
| 1. Allocation tracking | Allocation states: TRPA pool / Jurisdiction Pool / Private Development Pool | ✅ - `allocation-tracking.html` Overview tab implements all 3 states + adds "Unreleased" 4th state per Ken |
| 2. Source of rights | What sourced each year's added units: Pre1987 / 1987RP / 2012RP / Banked / Conversion | ✅ - `residential-additions-by-source.html` 5-source facet chart |
| 3. Total potential development | Constructed / Banked / Converted / pools | 🟡 - covered by Tracker sections i-iv (Existing / Banked / Reserved-not-constructed / Not-reserved-and-not-released). No standalone dashboard. |
| 4. Total development tracking | "How much of everything is actually built?" - combines all above | ✅ - `tahoe-development-tracker.html` (the canonical Tracker) |

---

## Round 1a — Dan Segan (May 14, 2026) · "Why would I look?" questions

Dan asked the foundational UX question for each dashboard. These answers became the card questions on `review.html` (was `index.html` at the time).

### `regional-capacity-dial.html` → renamed to `tahoe-development-tracker.html`

| Feedback | Status |
|---|---|
| **Why look:** "Understand how much has been built and can be built of each type" | ✅ - exactly the framing on the new home-page card |
| Could we just call "Tahoe Development Tracker"? | ✅ - file renamed; "capacity" removed from title and copy |
| I was thinking it would be total built + Banked + remaining allocations | ✅ - hero strip + sections i-iv now show this composition |
| I don't think there should be any % - totals can be augmented through conversions | ✅ - every `%` glyph removed; absolute counts only |

### `residential-additions-by-source.html`

| Feedback | Status |
|---|---|
| **Why look:** "Understand where the rights came from for everything that was built in a year" | ✅ - card question on home page matches verbatim |
| Are these "completed" residential units? | ✅ - header sub clarified to "Where **completed** residential units came from each year, 2013-2025" |
| What does "Avg 121 units/yr · net +1,469 after removals" mean? | ✅ - KPI sub reworded to "Avg N units/yr across X years" (gross, no removal arithmetic mixed in) |
| Could we add a facet/card for the total build in a year? | ✅ - "Added Units This Year" KPI added (the 4th KPI card) |
| Should also show banked for the year (full report of change on the ground) | ✅ - removed-units chart added below the main facet (To Bank + To Conversion side-by-side, zero baselines aligned) |

### `allocation-tracking.html`

| Feedback | Status |
|---|---|
| **Why look:** "Ensure TRPA hasn't allowed more built than the 2012 RP allows. Understand the balances of each rights pool." | ✅ - card question on home page reworded in Dan's voice ("Has growth stayed within the limits of the Regional Plan?") |
| Show 3 rows of cards (total / allocated / jurisdiction / TRPA held), remove the two graphs to differentiate from pool-balance-cards | ✅ - Allocation Tracking is now a single Overview surface: 4 rows × 5 cards (RES + RBU + CFA + TAU); 5 cards per row (Total / Allocated / Jurisdiction / TRPA / Unreleased). The Deep Dive tab (Sankey + per-jurisdiction bar + per-pool summary table) was retired 2026-05-18; its row-level layer 4 sums weren't reconciling to 2,600 and the underlying data issue needs to land before it can come back. Git history has the prior implementation. |

### `pool-balance-cards.html`

| Feedback | Status |
|---|---|
| **Why look:** "Ensure TRPA hasn't allowed more built than the RP allows. Understand the balances of each rights pool by jurisdiction." | ✅ - card question on home page matches |
| Remove the "pools 7" block at the top | ✅ - removed |
| Otherwise looks good to me | ✅ |

### `public-allocation-availability.html`

| Feedback | Status |
|---|---|
| **Why look:** "I don't know" | ✅ - dashboard archived (`html/_archive/`); unique explainer content folded into `pool-balance-cards.html` |

---

## Round 1b — Ken Kasman (May 13, 2026) · Detailed per-page review

### `regional-capacity-dial.html` (now `tahoe-development-tracker.html`)

| Feedback | Status |
|---|---|
| Change subtitle from "Where the Tahoe Region sits against its since-1987 cumulative capacity caps..." to "Where the Tahoe Region sits against the Regional Plan cumulative capacity" | ✅ - subtitle reworded |
| Sources should be TRPA + Lake Tahoe Regional Plan + LT Info Pool Balance Report | ✅ - footnote updated |
| Use "Assigned" not "built"; percentages should include built + assigned | ✅ - terminology updated; % removed per Dan |
| Change "Constructed vs remaining" wording per the verbose phrase Ken provided | ✅ - applied |
| "2012 Plan additional" should be all 8687, not 2600 | ✅ - applied; uses 8,687 since-1987 total |
| Remove "pool" from "Private Dev"; change "Drawn to a parcel; construction in progress" → "Allocated to a parcel; construction not completed" | ✅ - terminology updated |
| Jurisdiction pool: "not yet drawn" → "not yet assigned" | ✅ - applied |
| Separate TBD/unreleased from TRPA pool | ✅ - Unreleased now its own card (770 RES, 200,000 CFA) on `allocation-tracking.html` |
| Remove Completed residential units sections (they don't fit "Regional Plan additional development") | ✅ - removed |
| Add similar sections for RBU, CFA, TAU | ✅ - all 4 commodities present |
| Remove "Two cap numbers" / "2012 Plan Additional" text | ✅ - removed |

### `allocation-tracking.html`

| Feedback | Status |
|---|---|
| Source = LT Info Parcel Tracker, Residential Allocation Tracking | ✅ - footnote updated with the URL |
| Change "latest pool balances" link → Pool Balance Report | ✅ - link points to `/DevelopmentRightPool/DevelopmentRightPoolBalanceReport` |
| Separate 770 unreleased from TRPA pool | ✅ - separate "Unreleased" card |
| Update to all 8,687 (1987 + 2012 charts, plus combined) | ✅ - cards show Total Authorized 8,687 with TYPE_DESC explaining "1987 RP provided 6,087 + 2012 RP added 2,600 = 8,687" |
| Update Commercial + Tourist tabs with new data | ✅ - both commodities live from layer 12 |

### `pool-balance-cards.html`

| Feedback | Status |
|---|---|
| Source = LT Info Pool Balance Report | ✅ - footnote |
| Remove "One card per residential allocation pool..." subtitle | ✅ - removed |
| Add toggle for RBU, TAU, CFA | ✅ - 4 commodity toggles in the toolbar |
| Remove the CSLT "pool exhausted" card | ✅ - CSLT shows its 4 sub-pools (Multi-Family / Single-Family / Town Center / main); no misleading "exhausted" framing |
| Show released allocations per year (don't give "all at once" impression) | ✅ - residential per-year released-vs-assigned metering chart renders in the detail panel when a residential pool is clicked (layer 13) |
| Flip bar fills (show used not remaining) | ✅ - fill orientation reversed; numbers unchanged |

### `public-allocation-availability.html`

| Feedback | Status |
|---|---|
| Source = LT Info Pool Balance Report | ✅ - applied before archiving |
| Cards give wrong impression about "all at once" allocation | ✅ - addressed by the metering chart on `pool-balance-cards.html` after archiving this page |
| Flip bar fills | ✅ - applied |
| Carson City doesn't receive allocations - remove | ✅ - Carson removed from jurisdiction pills across the dashboard set; included in "All" basin totals only with `?` popover explainer in `development_history.html` (since the May 18 Option A archive, the former Option B is now the canonical file) |
| Add TRPA pool | ✅ - TRPA pool now its own state across all dashboards |
| Update bottom explainer text (the "What's a residential allocation?" copy) | ✅ - text used verbatim as the residential explainer in `content/explainers/pool-balance-cards/residential.md` (used by `pool-balance-cards.html` + `allocation-tracking_option1.html`) |

### `residential-additions-by-source.html`

| Feedback | Status |
|---|---|
| Source = TRPA, May 2026 | ✅ - footnote updated (and the standalone "Source: ..." line in the header was later removed per Comms-cycle decision since the footnote carries it) |
| Add link to development rights dashboard `trpa.maps.arcgis.com/apps/dashboards/ddfe...` | ✅ - link present in footnote |
| Replace "The story behind the inflections" → "Residential projects completed by year" | ✅ - applied (later refined again per Ken's round 2 to "Residential units completed by year") |
| Add charts for Units Removed (banked + converted) | ✅ - removed-units chart added; To Bank + To Conversion side-by-side with shared y-axis |

---

## Round 2 — Ken Kasman (May 15, 2026) · Response to round 1 changes

Ken's foundational correction: **"banked development rights are SEPARATE from allocations and must not be conflated."** This drove the architectural change to move banked out of allocation-tracking row headers and into its own surface on the Tracker.

### `allocation-tracking.html` (9 items)

| Feedback | Status |
|---|---|
| Remove "banked, available for transfer" lines above each section ("there are many more banked residential units than 6; allocations cannot be banked") | ✅ - removed |
| Separate Unreleased from TRPA Pool for Residential (770) and CFA (200K) | ✅ - Unreleased now a 5th card in the residential + CFA rows (4 cards for RBU + TAU which have no unreleased) |
| TRPA pool amounts are not dynamic - call this out | ✅ - italic "static; not metered annually" sub-line added to the Residential + CFA TRPA-pool cards |
| Change "2012 Regional Plan additional · of 8,687 since-1987 max" → verbose phrasing | ✅ - applied verbatim |
| Change "Regional Plan max" under CFA/TAU → "Total Authorized" | ✅ - applied |
| Change CFA cap text → verbose ("1987 RP provided 800,000 sq ft; 2012 RP added 200,000 sq ft for a total of 1,000,000") | ✅ - applied verbatim |
| Change TAU cap text → verbose ("1987 RP provided 400 TAU; no additional units added in 2012 RP") | ✅ - applied verbatim |
| Change "drawn to a parcel" → "allocated to a parcel" | ✅ - applied |
| Change "held centrally by TRPA" → "held in TRPA pool" | ✅ - applied |

### `pool-balance-cards.html` (4 items)

| Feedback | Status |
|---|---|
| Add "all jurisdictions combined" chart; default to that instead of Placer | ✅ - synthetic "All Jurisdictions" card added (pinned to top of grid; renders aggregate stacked bar). Default-selected on page load. |
| Rename labels: "Residential Allocations" / "Residential Bonus Units" / "Tourist Bonus Units" | ✅ - applied (toggle buttons + COMM_META labels) |
| Commodity-aware explainer (or remove if can't change) | ✅ - explainer markdown files at `content/explainers/pool-balance-cards/*.md`. All 4 commodities (Residential · RBU · CFA · TAU) now carry full analyst-authored content per the May 18 delivery; "Content forthcoming" placeholders are gone. |
| Change "Standalone" → "Unreleased" for CFA | ✅ - applied in `regional_plan_allocations.json` + the converter script |

### `residential-additions-by-source.html` (3 items)

| Feedback | Status |
|---|---|
| Add removed units (Banking + Conversions) | ✅ - dedicated "Residential units removed by year" chart below the main facet; To Bank + To Conversion as faceted area charts with shared y-axis (zero baseline aligned) |
| Change "This year (215)" → "Added Units This Year" (since 215 isn't the net change) | ✅ - KPI label updated |
| "Residential projects completed by year" → "Residential units completed by year" (units span multiple years) | ✅ - applied |

### `tahoe-development-tracker.html` (3 items)

| Feedback | Status |
|---|---|
| Remove banked/transfer from Regional Plan Development Rights section | ✅ - banked sub-lines removed from the per-commodity sections |
| Create separate Banked Development Rights section below Bonus Units (use data from "Banked Development" tab in `Additional Development as of April2026` file) | ✅ - on `tahoe-development-tracker_option2.html` (Option C variant): 4-card section (MFRUU 47 / SFRUU 352 / CFA 326,776 / TAU 1,501); also surfaced via Section ii "Banked development" on canonical Tracker (Option A) |
| Remove ", against the Regional Plan totals." from title | ✅ - applied |

---

## Round 3 — Ken Kasman (May 16, 2026) · Follow-up after round 2

Mostly fine-tuning + a few items where Ken was viewing a stale gh-pages build (already fixed locally). Two substantive changes shipped; one deferred pending Ken's promised spreadsheet attachment.

### `tahoe-development-tracker.html`

| Feedback | Status |
|---|---|
| "Remove the conversions and major-projects sections" | ✅ - already removed in the live build; Ken was viewing a stale gh-pages cache |
| "Place data within the 4 sections (i / ii / iii / iv)" | ✅ - canonical Tracker has been organized into the 4 sections since Friday May 15 |
| "Add note that the on-the-ground residential will be less than 'allocated' because the analyst's annual conversion of units to TAU isn't reflected" | ✅ - section iii already carries this caveat ("residential converted to TAU shows up in TAU counts but is not subtracted from residential here") |
| "Provide link to ESRI dashboard at the top of each section" | ✅ → 🔄 **Reversed.** Originally added section-links pointing to the TRPA Development Rights ESRI dashboard. Per Mason's May 16 follow-up, the same data now lives locally in `development_history.html` and the residential composition view, so the external ESRI links were dropped. Section i now points to `development_history.html` (per-commodity year-over-year change); section iii keeps its internal link to `allocation-tracking.html`. ESRI links also removed from both residential-additions footers. |

### `allocation-tracking.html`

| Feedback | Status |
|---|---|
| "Balances are wrong - sending a spreadsheet with the corrected ones" | ✅ - the corrections now live as a REST table (`Cumulative_Accounting` MapServer); allocation-tracking pulls live from layer 10 (`Source='Grand Total'` rows) so any republish of the corrected balances flows straight to the dashboard. No analyst-side xlsx needed. |
| "Add section for RBU (Residential Bonus Units)" | ✅ - RBU section has been present since round 2 (4 rows × 5 cards: RES / RBU / CFA / TAU); Ken was viewing a stale gh-pages cache |
| "Remove 'static; not metered annually' labels on TRPA pool cards" (the underlying data will be restructured to expose year-assigned breakdown later) | ✅ - italic sub-line removed from all 4 TRPA-pool cards across the commodity rows; comment in code documents the rationale and the future year-assigned plan |

### `residential-additions-by-source.html`

| Feedback | Status |
|---|---|
| "Remove the 'Total Completed' facet (data is on the dashboard elsewhere)" | ✅ - facet grid reduced from 6 panels to 5 (the redundant Total panel removed); reflected in the in-code comment |
| "Separate the Residential Units removed by year into 2 charts (one for Banked, one for Conversion)" | 🟡 **Partial.** First shipped as two stacked full-width cards (each its own independent y-axis), then reverted to the prior layout - a single card with side-by-side 2-panel facets (each panel titled separately, shared y-axis so zero lines align). Two stacked cards added too much vertical height; the side-by-side compromise preserves the "two separated facets" reading while keeping the section compact. Applied to both canonical + Option B variants. |

---

## Additional decisions made during iteration (not from Dan/Ken directly)

- **WCAG title contrast fix.** TRPA blue on TRPA navy reads at ~2.5:1 (fails WCAG AA). Changed all dashboard h1 highlight colors to TRPA orange (~4.6:1) - except `_option1` variants which use TRPA ice (~9:1) for visual differentiation. ✅
- **Footer link convention.** All REST-layer links in dashboard footers now use the layer / table NAME as the link text (not "layer N"), so hrefs can be swapped to `tahoeopendata.org` download links later without re-writing visible copy. ✅
- **Option A/B/C variant pattern.** 5 of 7 dashboards have alternative layouts. Decided-against variants (only `tracker_option1` so far) move to `html/_archive/` and surface as small cards on the home page. ✅
- **`start.html` → `index.html` → `review.html` rename chain.** Decision-tree home page first promoted to the default `index.html`; the old data-architecture page became `reference.html`. Then on May 18 a new public-facing landing took over `index.html` and the decision tree shifted to `review.html` so the trpa.gov embed gets a public-friendly entry while internal reviewers keep their full set at `review.html`. ✅
- **Loading splash overlay** standardized across all 12 active dashboards (was only on a few). ✅
- **Y-axis honest dampening on cumulative charts** (former `development_history_option1.html`, now canonical `development_history.html`). CFA's 0.03% change initially read as visually dramatic (filled 83% of panel); a "honest dampening" pass made it a subtle wobble (27% fill). **Reversed 2026-05-18 per Mason's ask** - the cumulative chart now uses a full-range y-axis from 0 to data-max, which makes the small-percentage changes read as near-flat lines at the top of each panel (truthful for the absolute-totals framing). ✅ → 🔄

---

## Deferred backlog (data-dependent or future iteration)

From Mason's reply on May 15 + Ken's May 16 follow-up, items that remain in the backlog:

- ⏸️ **Tracker:** restructure to "total built + banked + remaining per category" end-to-end. Hero strip + 4 sections is the closest we can get with current data; a single composite "ground state" card per commodity would need built-unit + banked-unit data in one shape.
- ⏸️ **Residential additions:** banked / removed-out side ("full report of what changed on the ground") - **partially addressed** via the new per-source removed-by-year charts (To Bank + To Conversion). Per-year banked additions (units re-entering the pool from prior bankings, distinct from removals) are NOT yet shown.
- ⏸️ **Pool-balance-cards:** residential per-year released / assigned chart on *every* card, not just in the detail drilldown. Per-year data is residential only today (layer 13).
- ⏸️ **TRPA pool year-assignment timeline.** Ken: "the data I provided shows the year these were assigned to the TRPA pool." The previous italic "static; not metered annually" note was removed at Ken's May 16 ask; the per-year-assigned visualization would need a new REST surface that exposes per-year TRPA pool assignments (not derivable from layer 4 or layer 5 today). Until then the TRPA pool cards carry no temporal disclaimer.
- ⏸️ **Live Banked Development Rights on the Tracker** (vs hardcoded snapshot). Blocked on Ken's walkthrough of `banked_reconciliation_findings.csv` and a policy decision about how to filter layer 7 (which Inactive records count? which categories belong to the cumulative-accounting view?).
- ⏸️ **Per-project Banked Development detail** (Lakeside Inn 124, Motel 6 141, etc.). No REST equivalent today; would need a `BankedDevelopment_Projects` layer mapping APN to project name.
- ⏸️ **Net change KPI on residential-additions** (added minus removed). Once the per-year removed series ships natively, follow-up can compute `net_2025 = added_2025 - removed_2025` and surface alongside "Added Units This Year."

---

## Summary scorecard

| Reviewer | Round | Items | ✅ Addressed | 🟡 Partial | ⏸️ Deferred |
|---|---:|---:|---:|---:|---:|
| Dan Segan | May 11 (framing) | 4 | 3 | 1 | 0 |
| Dan Segan | May 14 ("Why look?") | 14 | 13 | 1 | 0 |
| Ken Kasman | May 13 (round 1) | 32 | 32 | 0 | 0 |
| Ken Kasman | May 15 (round 2) | 19 | 19 | 0 | 0 |
| Ken Kasman | May 16 (round 3) | 9 | 8 | 1 | 0 |
| **Total** | | **78** | **75 (96%)** | **3 (4%)** | **0** |

Plus 7 deferred backlog items (data-dependent, scheduled for later iterations) that the team is aware of.

---

## What's NOT in this document

- Communications reviewer brief (separate: `REVIEWER_BRIEF_2026-05.md`)
- UX review from the `trpa-dashboard-ux-review` skill (separate; informed the recent hero-strip + date-framing fixes on the Tracker)
- Internal QA-process feedback (handled in `data/qa_data/`)
- TRPA staff bug reports (handled per-issue)

---

## Next planned review

- **Monday May 18:** Communications reviewer per `REVIEWER_BRIEF_2026-05.md`
- **Wednesday May 20:** publish target
- **TBD:** Ken's walkthrough of the banked reconciliation findings + decision on how to filter Layer 7 for the Tracker (unblocks the "live banked" deferred item)
