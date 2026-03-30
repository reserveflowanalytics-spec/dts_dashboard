# Reserve Flow Analytics — Dashboard Improvement Roadmap
*Drafted: March 26, 2026*

---

## Context & Analytical Foundation

This roadmap is informed by a comparison between the Reserve Flow DTS Dashboard (reserveflow.info/dashboard.html) and Mike Norman MMT Economics (YouTube: @mikeydoggy), conducted using live transcript and dashboard data. Mike Norman has 40 years of markets experience applying an MMT/fiscal flow lens. His approach is qualitative, momentum-based, and informed by long historical pattern recognition. The dashboard provides systematic, data-conditional, near-term quantitative analysis of the same underlying source — the Daily Treasury Statement.

The core finding: the two approaches are complementary rather than contradictory. The dashboard excels at near-term regime identification and marginal momentum. Mike's framework captures absolute-level context and long-cycle structural support. The improvements below are designed to bridge that gap.

---

## Current Dashboard Strengths

- Real-time DTS data via FiscalData API
- Clean regime classification (Restrictive / Expansionary / Neutral)
- FYTD YoY scorecard with full flow decomposition
- Transmission channel analysis (fiscal → reserves → rates → term premium)
- Forward calendar for known drain events
- Invalidation logic built into the Analysis tab
- Market Narrative section with headline scanning

---

## Improvement Priorities

### Priority 1 — Absolute Level Context Panel

**What:** Add a panel alongside the existing YoY comparison showing current MTD/FYTD injection against the same metric at 5, 10, and 20 years ago in nominal dollar terms.

**Why:** The -18.8% YoY reads as restrictive in isolation but the absolute FYTD injection of $931.8B would have been the entire annual federal deficit as recently as 2008. Without this context, users with a longer frame of reference may correctly dismiss the restrictive signal as a relative rather than absolute condition. FRED series FYONET and MTSDS133FMS provide the historical benchmarks.

**Implementation:** Static reference table or small sparkline panel on the main dashboard header. Low complexity, high contextual value.

---

### Priority 2 — Dedicated Tariff Drain Tracker

**What:** Elevate tariff receipts from a line in the Scorecard tab to its own dedicated visual — monthly trend chart, pre vs post-SCOTUS comparison, and trajectory relative to SSA payment cycle size.

**Why:** Tariffs/customs are running +239.4% YoY FYTD ($180.2B vs $53.1B prior year) and are operationally identical to taxes — they destroy private sector dollar balances. This is the single most important new structural variable in the current fiscal regime. The SCOTUS ruling produced a measurable and tradeable dip in the monthly drain (Mike Norman observed ~$17.8B vs prior ~$23B). That kind of signal should be impossible to miss on the dashboard.

**Implementation:** New sub-tab or expandable card within Composition tab. Include a "SCOTUS regime change" annotation marker on the monthly chart.

---

### Priority 3 — Fiscal Flow vs Market Overlay

**What:** A chart overlaying the core fiscal injection series (or 20d rolling average) against a risk asset proxy — S&P 500, SPY, or a credit spread.

**Why:** Mike's entire value proposition is the connection between fiscal flows and market direction. The dashboard currently stops at the flow data. An empirical overlay would let users see how Restrictive vs Expansionary regimes have historically mapped to market outcomes, making the signal actionable rather than purely descriptive.

**Implementation:** Could use a public market data API (Yahoo Finance, Alpha Vantage) for the equity overlay. Display as a dual-axis chart in a new "Market Linkage" tab. Include shaded regime periods.

---

### Priority 4 — Interest Income Channel Prominence

**What:** Elevate the trailing 12-month interest payment series to a top-level metric, alongside a YoY trend and projected annual run-rate.

**Why:** At ~$659.1B trailing 12-month (8.4% of total government spending), interest payments to bondholders are one of the largest single fiscal injection channels and they operate on autopilot at current rates. This creates a paradox — Fed "tightening" simultaneously injects more dollars through interest income, partially offsetting the restrictive intent. This is the most widely misunderstood channel in public macro commentary and a genuine edge for users of this dashboard.

**Implementation:** Add a dedicated "Interest Income Channel" card in the Analysis tab. Show trailing 12m total, YoY change, and projected forward path if rates hold vs if rates cut. Flag the Warren Mosler "basic income for those who already have money" framing as a tooltip or annotation.

---

### Priority 5 — Live Regime Turning Point Signal

**What:** A visual threshold tracker showing how far current conditions are from a regime flip, with named criteria for what would trigger a change from Restrictive to Neutral/Expansionary.

**Why:** Mike explicitly tries to call inflection points early. The dashboard currently tells you the current regime but not how close you are to the next one. The invalidation logic already exists in the Analysis tab text — it just needs to be surfaced as a live, quantified visual.

**Implementation:** A simple "distance to flip" meter or traffic-light panel. Criteria example: *"Regime flips when 5d average net transfer exceeds 20d average for 3 consecutive sessions AND MTD YoY delta turns positive."* Track each condition independently with a checkmark/cross status.

---

### Priority 6 — Government Shutdown / CR Annotation Layer

**What:** Annotate the Daily Flows chart with named periods of government shutdown or continuing resolution, flagging disbursements that are mechanically suppressed and likely to reverse.

**Why:** During shutdown periods, agency disbursements are reduced in ways that are temporary and reversal-prone — not structural weakness. Without this annotation, users may misread suppressed flow readings as a deteriorating fiscal regime when they are actually a reversible policy artifact. Mike Norman flagged the DHS/TSA payroll gap in his videos; this would surface that automatically from the data.

**Implementation:** Maintain a simple lookup table of shutdown/CR periods with start and end dates. Overlay as a shaded annotation on the Daily Flows chart with a tooltip explanation.

---

### Priority 7 — "Practitioner Checklist" Panel

**What:** A small panel tracking the specific variables that experienced MMT-informed practitioners (like Mike Norman) watch as a quick go/no-go checklist: leading fiscal flows YoY, TGA direction, refund season pace, monthly tariff drain vs prior month, and 5d vs 20d net transfer average.

**Why:** Makes the comparison between the systematic dashboard regime and a practitioner's intuitive checklist explicit and live. Helps users understand what conditions a long-experienced flow watcher would call bullish vs bearish, and whether the current data supports or contradicts that read.

**Implementation:** A compact card, possibly on the main dashboard above the score breakdown. Green/amber/red status for each of 5–6 named variables. Could be labeled "Practitioner Signals" or similar.

---

## Historical Reference Series (FRED)

*For implementing Priority 1 and providing long-term context throughout:*

| Series | Description | Current Value |
|---|---|---|
| FYONET | Federal Net Outlays (annual) | $7.01T (FY2025) |
| MTSDS133FMS | Federal Surplus or Deficit (monthly) | -$307.5B (Feb 2026) |
| FYFSGDA188S | Deficit as % of GDP (annual) | -5.77% (FY2025) |
| WALCL | Fed Total Assets (balance sheet) | $6.66T (Mar 2026) |
| WRBWFRBL | Bank Reserve Balances at Fed | $3.04T (Mar 2026) |

**Key historical anchors for absolute level context:**

- **2000:** Annual outlays ~$1.79T, deficit ~$236B surplus
- **2005:** Annual outlays ~$2.47T, deficit ~$318B
- **2010:** Annual outlays ~$3.46T, deficit ~$1.29T (GFC)
- **2020:** Annual outlays ~$6.55T, deficit ~$3.13T (COVID)
- **2025:** Annual outlays ~$7.01T, deficit ~$1.83T (non-recessionary baseline)

---

## Suggested Implementation Sequence

1. **Tariff Drain Tracker** — highest signal value given current policy environment, relatively contained scope
2. **Regime Turning Point Signal** — most directly actionable for users, logic already exists in the codebase
3. **Absolute Level Context Panel** — low complexity, immediately reframes the YoY narrative
4. **Government Shutdown Annotation** — simple lookup table, meaningful during current DHS/TSA situation
5. **Interest Income Channel Card** — moderate complexity, high conceptual value
6. **Practitioner Checklist Panel** — design-dependent, good for user accessibility
7. **Fiscal Flow vs Market Overlay** — most complex due to external data dependency, highest potential engagement

---

*Source data: US Treasury Daily Treasury Statement via FiscalData API, Federal Reserve FRED database. Dashboard framework: Reserve Flow Analytics. Comparative analysis informed by Mike Norman MMT Economics YouTube channel transcripts (March 2026).*
