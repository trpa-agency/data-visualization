# Cumulative Accounting Dashboards · What's New & Addressed
*May 11-18, 2026 review cycle*

## Layout options per dashboard (status as of 2026-05-18)

The Option A/B/C exploration phase is **complete**. Every active dashboard is
now a single canonical file; the rejected variants moved to `html/_archive/`.

| Dashboard | Canonical file | Archived variants |
|---|---|---|
| **Tahoe Development Tracker** | 4-section layout (i Existing · ii Banked · iii Reserved, not constructed · iv Not reserved and not released) | `_option1.html` (3-tile no-banked), `_option2.html` (3-tile + banked) |
| **Allocation Tracking & Pool Balances** (merged 2026-05-18) | Two tabs in one dashboard: **Basin overview by commodity** (stacked-bar tile per commodity, from layer 10) + **Pool balances by jurisdiction** (per-pool cards with click-to-drill metering chart, from layers 12 + 13). Folded the standalone Pool Balance Cards in. | `allocation-tracking_card-grid.html` (original card-grid Option A), `pool-balance-cards.html` (standalone, now tab 2), `pool-balance-cards_option1.html` (compact KPI hero variant) |
| **Residential Additions by Source** | 5-source facet chart with Source Legend chips (hover for definitions) + combined-view toggle | `_option1.html` (facet-only + inline source strip) |
| **Development History** | Cumulative trajectory area chart on top + year-over-year change bars per commodity below; year-over-year percent change in hover tooltips; full-range y-axis from 0 | original `development_history.html` (year-slider + KPIs + dampened y-axis) |

The public-facing entry point (`index.html`) lists the 5 canonical dashboards
without variant selectors. The internal review page (`review.html`) surfaces the
same canonical files plus an Archive section linking to the rejected variants
for reference.

## What's new (since the last review)

### Tahoe Development Tracker
- Hero strip with three live basin totals (RES / CFA / TAU)
- 4-section structure (i / ii / iii / iv); all "as of 2025"
- Live Banked Development Rights from REST layer 9
- "Capacity" dropped from title; subtitle no longer references "Regional Plan totals"
- Section i links to Development History; section iii to Allocation Tracking
- Variants archived 2026-05-18 (3-tile commodity-first layouts didn't earn their place vs the 4-section canonical)

### Allocation Tracking
- 4 commodity rows × 5 cards (TAU has 4 — no Unreleased)
- Verbose total descriptions (e.g., "1987 RP provided 800,000 sq ft; 2012 RP added 200,000 for a total of 1,000,000")
- "Unreleased" pulled out as its own card (was rolled into TRPA pool)
- Added RBU (Residential Bonus Units) section
- "Static; not metered annually" sub-line removed (data restructure underway)
- Deep Dive tab (Sankey + per-jurisdiction bar + per-pool summary table) retired 2026-05-18 because its row-level sums weren't reconciling to 2,600; Allocation Tracking is now a single Overview surface

### Pool Balance Cards
- New "All Jurisdictions" combined card; default-selected on load
- 4-commodity toggle: Residential Allocations · Residential Bonus Units · Commercial Floor Area · Tourist Bonus Units
- "Standalone" CFA group renamed "Unreleased"
- Commodity-aware explainer cards with full analyst-authored content for all 4 commodities (Residential / RBU / CFA / TAU; delivered May 18)
- Per-year released-vs-assigned metering chart in the residential detail drilldown

### Residential Additions by Source
- New Source Legend card at the top with hover tooltips for each of the 5 sources
- 5-source facet chart (redundant Total panel removed)
- Variant archived 2026-05-18 (the From-Bank / From-Conversion grouping was preserved as a backlog idea but the canonical facet-toggle layout was chosen)
- "Residential units removed by year" sits in a single card with To Bank + To Conversion as side-by-side panels (shared y-axis for aligned zero lines)
- "Added Units This Year" KPI clarifies what 215 actually represents

### Development History (simplified to a single canonical layout May 18)
- Option A archived; the former Option B is now the canonical `development_history.html`
- Cumulative trajectory chart moved to the top; year-over-year change bars below
- Full-range y-axis from 0 (the earlier honest-dampening pass was reverted; small-percent changes now read as near-flat lines at the top of each panel, truthful for the absolute totals)
- Year-over-year percent change in hover tooltips via customdata
- Year slider + 3 KPI cards removed (the charts always show the full 2012-2025 trajectory; only the jurisdiction pills remain as a filter)

### Cross-cutting
- New decision-tree review page (`review.html`) with 7 audience-color-coded cards (for internal reviewers); public-facing landing (`index.html`) with 4 cards + photo hero for the trpa.gov embed
- Data architecture reference moved to `reference.html`
- Option A/B/C exploration phase closed 2026-05-18; rejected variants archived
- Unified header treatment across all dashboards: navy band + color TRPA logo on left + plain white title + no accent gradient stripe (matches index.html)
- Locked commodity colors across every dashboard: **Residential = TRPA forest green**, **Commercial = TRPA earth**, **Tourist = TRPA purple**
- Live Data badge + loading splash overlay on every dashboard
- WCAG title contrast fix (orange instead of blue on navy)
- ESRI dashboard links dropped (data is now in `development_history.html` locally)
- QA corrections to allocation balances now flow through REST layer 10 (no analyst xlsx needed)

## What's been addressed

| Round | Reviewer | Items | Addressed |
|---|---|---:|---:|
| May 11 (framing) | Dan Segan | 4 | 3 ✅ + 1 🟡 |
| May 14 ("Why look?") | Dan Segan | 14 | 13 ✅ + 1 🟡 |
| May 13 (round 1 detail) | Ken Kasman | 32 | 32 ✅ |
| May 15 (round 2 response) | Ken Kasman | 19 | 19 ✅ |
| May 16 (round 3) | Ken Kasman | 9 | 8 ✅ + 1 🟡 |
| **Total** | | **78** | **75 ✅ + 3 🟡 (96 percent)** |

Full per-item detail in `REVIEW_HISTORY_2026-05.md`. Zero items currently deferred.

## Still open (data-dependent backlog)

- Tracker: single "ground state" composite card per commodity (needs built + banked in one shape)
- Residential additions: per-year banked additions (units re-entering the pool from prior bankings)
- Pool-balance-cards: per-year metering chart on every card, not just the detail panel
- TRPA pool year-assignment timeline (needs new REST surface)
- Live Banked Development Rights on the Tracker (vs hardcoded snapshot; blocked on Layer 7 filter decision)
- Per-project Banked Development detail (no REST equivalent today)
- Net change KPI on residential-additions (added minus removed)

## Next milestones

- **Mon May 18:** Communications reviewer per `REVIEWER_BRIEF_2026-05.md`
- **Wed May 20:** publish target
- **TBD:** Ken's walkthrough of banked reconciliation findings + Layer 7 filter decision
