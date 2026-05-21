# Dashboard Footer Pattern - Recommendation for Public Launch
*Audit date: 2026-05-18. Pattern shipped same day across all 5 active dashboards.*

## Shipped 2026-05-18

- **Footnote rewrites:** every dashboard now has a short public footnote (agency attribution + optional dashboard-specific note like "Banked tracked separately" on Allocation Tracking).
- **`reference.html` methodology link removed** - that page is internal/developer-facing; a public visitor doesn't need to be pointed at the data architecture reference.
- **Agency `<footer>` block:** every dashboard now has a `<footer>` with copyright + trpa.gov + Feedback (`mailto:info@trpa.gov` confirmed).
- **Accessibility link omitted for now** - awaiting `trpa.gov/accessibility/` to exist. Easy to add once that page lands.

## Open items (still need Comms input)

- **Accessibility page URL** - drop into the `<footer>` once available
- **Suggested citation** - decide if a public-facing citation is worth surfacing anywhere

---


The footer area on each dashboard currently mixes three distinct concerns:
cross-link navigation, technical source attribution, and (sometimes) page
footer copyright. The patterns are inconsistent across the 5 active
dashboards, and most are written for internal/analyst readers rather than
public visitors.

This doc audits what's there today, lists the issues, and proposes a
unified public-facing pattern to ship with.

## 1. Current state audit (2026-05-18)

| Dashboard | `.related-dashboards` strip | `.footnote` block | `<footer>` (copyright) |
|---|---|---|---|
| `tahoe-development-tracker.html` | ✓ | **5-paragraph footnote** with raw REST URLs, technical detail (`<code>Source='Grand Total'</code>`), per-section data lineage, even a pointer to a QA markdown file (`data/qa_data/banked_reconciliation_summary.md`) | ✗ |
| `allocation-tracking.html` | ✓ | 3 paragraphs, REST layer URLs, mentions of `<code>Source='Grand Total'</code>` and `as-of` span | ✗ |
| `residential-additions-by-source.html` | ✓ | 2 paragraphs, layer NAME links (cleaner) | ✗ |
| `development_history.html` | ✓ | 2 short paragraphs, single source + Carson caveat | ✗ |
| `qa-change-rationale.html` | ✓ | 1 paragraph but very technical (mentions `qa_change_events.csv`, `notebooks/04_load_ca_changes.ipynb`, `scripts/convert_qa_corrections.py`) | ✗ |
| `index.html` (public landing) | (uses an "About this data" card instead) | (none - public surface) | ✓ (copyright + trpa.gov + Dashboard review link) |

## 2. Issues with current footers for a public launch

1. **Wildly inconsistent length and tone.** Tracker has 5 paragraphs of technical source citations; Development History has 2 sentences. Reads like 5 different teams wrote them.
2. **Raw REST URLs are developer-facing.** `https://maps.trpa.org/server/rest/services/Cumulative_Accounting/MapServer/0` is useful for someone building an integration, opaque for a citizen.
3. **References to internal artifacts** like `data/qa_data/banked_reconciliation_summary.md`, `scripts/convert_pool_balances.py`, `notebooks/04_load_ca_changes.ipynb`. These point to files no public visitor can open.
4. **No publication / last-updated timestamp.** A public visitor seeing a number can't tell if it's a week old or a year old.
5. **No accessibility statement link.** Required for `trpa.gov`-hosted content per Section 504 / 508 and California Government Code §11135.
6. **No feedback / contact path.** A user who spots a wrong number has nowhere to flag it.
7. **No agency-level copyright / page footer** on the dashboard pages themselves. The public landing has one (`<footer>`) but the dashboards don't.
8. **`.related-dashboards` is mostly redundant with the public landing.** Public visitors typically arrive via a card on `index.html` and don't need a second navigation strip - though it's useful for embed contexts where the landing might not be visible.

## 3. Recommended public-facing pattern

Three stacked blocks at the bottom of every dashboard, in this order:

### Block 1: `.related-dashboards` (KEEP, simplified)

Same idiom as today, but trim to 2-3 cross-links plus "All dashboards" at the end. Drop the technical wayfinding labels in parens ("(per-pool drilldown)", "(per-commodity overview)") - they read as internal jargon. A short cross-link sentence is plenty.

```html
<div class="related-dashboards">
  <strong>Related views:</strong>
  <a href="other-dashboard.html">&harr; Other Dashboard</a>
  <a href="index.html">All dashboards</a>
</div>
```

### Block 2: `.footnote` (REWRITE, public-facing)

Three short lines, in this order: source + last updated + methodology link.

```html
<div class="footnote">
  <strong>Source:</strong> Tahoe Regional Planning Agency Cumulative Accounting service.
  <strong>Last updated:</strong> <span id="footnote-asof">&hellip;</span>.
  <br>For methodology and full data lineage, see the
  <a href="reference.html">Data &amp; Architecture Reference</a>.
</div>
```

Rules for the public footnote:
- **No raw REST URLs in visible copy.** The reference page collects those.
- **No file paths or script names.** Anything starting with `data/`, `scripts/`, or `notebooks/` is internal.
- **Last-updated timestamp** populated at runtime from the data source's `AsOfDate` field where available (Layer 10, Layer 12 carry this; Layer 0 uses `MAX(YEAR)`).
- **Single methodology link** pointing at `reference.html`, which can be exhaustive without polluting every dashboard.

### Block 3: `<footer>` (NEW, agency-level)

Match the existing `<footer>` on `index.html`. Adds copyright + trpa.gov + accessibility + feedback in a single short row.

```html
<footer>
  &copy; 2026 Tahoe Regional Planning Agency &middot;
  <a href="https://www.trpa.gov/">trpa.gov</a> &middot;
  <a href="https://www.trpa.gov/accessibility/">Accessibility</a> &middot;
  <a href="mailto:info@trpa.gov?subject=Dashboard%20feedback">Feedback</a>
</footer>
```

Matching CSS (already on `index.html` - lift it to a shared rule):

```css
footer {
  padding: 18px 32px 26px;
  font-size: 0.74rem; color: var(--text-light);
  border-top: 1px solid var(--border);
  background: var(--surface);
  margin-top: 28px;
  text-align: center;
}
footer a { color: var(--trpa-blue); text-decoration: none; }
footer a:hover { text-decoration: underline; }
```

## 4. What moves to `reference.html`

Anything cut from individual dashboard footnotes lands on the reference page instead:

- Full REST layer URLs (already there in the layer-inventory table)
- Source-of-load notes (analyst xlsx / script names)
- Per-section data lineage (which `<code>WHERE</code>` clause for each card)
- Reconciliation notes (Layer 7 vs Layer 9 banked totals, etc.)
- Field-mapping notes

A small "For methodology and full data lineage, see the Data & Architecture Reference" link from every dashboard footnote does the job of pointing technical readers there.

## 5. Implementation plan (when we say go)

1. **One-time CSS extraction:** lift the `footer` rules from `index.html` into each dashboard's `<style>` block (or, if we ever consolidate to a shared stylesheet, that's the home).
2. **Per-dashboard rewrites:**
   - Trim `.related-dashboards` to 2-3 cross-links (already mostly OK).
   - Replace `.footnote` body with the public 3-line version.
   - Add a `<footer>` block right above `</body>`.
3. **Wire the as-of timestamp:**
   - The Tracker already pulls `MAX(YEAR)` from Layer 0 - reuse that for `#footnote-asof`.
   - Allocation Tracking uses `balancesAsOf` from Layer 10 - already in place.
   - Pool Balances tab uses Layer 12's `AsOfDate`.
   - Residential Additions can read it from Layer 11's `AsOfDate` field (TBD - verify the field exists; if not, hardcode `'2025'` to match the As-of badge in the header).
   - Development History uses Layer 0's `MAX(YEAR)`.
4. **Move the technical detail to reference.html:**
   - Audit each dashboard's current footnote.
   - For any technical breadcrumb not already in `reference.html`, add it under the matching layer-inventory row.
5. **Add an `Accessibility` page** at `trpa.gov/accessibility/` if it doesn't already exist (this is a Comms / agency-level task, not the dashboard's job). The link in the footer assumes that page exists.
6. **Verify the mailto** - confirm `info@trpa.gov` is the right inbox for dashboard feedback, or swap for a dedicated address (e.g., `data@trpa.gov` or `dashboards@trpa.gov`).

## 6. Reference implementation (drop into any dashboard)

```html
<!-- ============================================================
     PUBLIC-FACING FOOTER PATTERN (as of 2026-05-18)
     ============================================================ -->

<!-- Cross-link strip: 2-3 related dashboards + "All dashboards" -->
<div class="related-dashboards">
  <strong>Related views:</strong>
  <a href="DASHBOARD.html">&harr; Other Dashboard</a>
  <a href="index.html">All dashboards</a>
</div>

<!-- Public footnote: source + last-updated + methodology link.
     Keep at 2-3 short lines max. No raw REST URLs, no file paths. -->
<div class="footnote">
  <strong>Source:</strong> Tahoe Regional Planning Agency Cumulative Accounting service.
  <strong>Last updated:</strong> <span id="footnote-asof">&hellip;</span>.
  <br>For methodology and full data lineage, see the
  <a href="reference.html">Data &amp; Architecture Reference</a>.
</div>

<!-- Agency footer: copyright + trpa.gov + Accessibility + Feedback -->
<footer>
  &copy; 2026 Tahoe Regional Planning Agency &middot;
  <a href="https://www.trpa.gov/">trpa.gov</a> &middot;
  <a href="https://www.trpa.gov/accessibility/">Accessibility</a> &middot;
  <a href="mailto:info@trpa.gov?subject=Dashboard%20feedback">Feedback</a>
</footer>
```

## 7. Open questions (for the Comms reviewer)

- Is there an existing `trpa.gov/accessibility/` page, or do we need to create one?
- Is `info@trpa.gov` the right inbox for dashboard feedback, or should we route to a specific person / team?
- Do we want to add a suggested citation? (`Tahoe Regional Planning Agency. (2026). Allocation Tracking Dashboard. https://...`)
- Do we want a privacy/cookie banner on the public-embed pages? (Probably yes if any analytics gets added.)
- Should the methodology link open in a new tab (target="_blank") given dashboards may be iframe-embedded?
