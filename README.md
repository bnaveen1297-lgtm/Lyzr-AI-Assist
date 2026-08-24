# Lyzr Founders' Cockpit

A single, self-contained analytics dashboard for the founders' office — one HTML file, no build step, no dependencies, works offline. Open `index.html` in any browser.

Built in response to the brief: *"a dashboard with a news feed that tracks all internal metrics across marketing, sales, project management, etc. — simple for a founder to see, with in-depth access."*

---

## The thinking behind it

The founder doesn't have a data source yet, and he's screening for an **analytical brain** — someone who finds *relationships* between data points, not someone who just renders numbers. So this is built as two things at once:

1. **A working model today** — a coherent, synthetic AI-SaaS scenario anchored on his stated unit economics (**$8M ARR, ~$10M net burn**), so every number ties to every other number.
2. **A data contract for tomorrow** — the same schema accepts real CSV / Google Sheets / product-API data and every view repopulates automatically.

Three layers, one toggle — exactly the "he sees one screen, then drills in" behaviour he described:

| View | Who it's for | What it answers |
|------|--------------|-----------------|
| **Founder View** | CXO, 10-second read | Revenue, burn, runway, the 5 board-level efficiency ratios, headcount health, and the 3 things that need him today |
| **Departments** | Any team lead | All 12 teams on one comparable framework, click-to-drill |
| **Correlation Engine** | The analyst | The *real* relationships — Pearson r computed live on 12 months of data |
| **Insight Feed** | Everyone | The dashboard telling you what changed and why — the "news feed" |

## Why the correlation engine matters

His LinkedIn post is explicit: *"run correlation models to identify the true relationships between data points, not just prompting GPT and Claude."* That's the whole test.

So the analytics layer computes **actual Pearson correlations** in-browser across 11 operating metrics (marketing spend, MQLs, SQLs, demos, talk-time, reps, bookings, new ARR, CAC, tickets, CSAT). The underlying sample series are constructed with *genuine* causal structure + noise — e.g. demos are driven by SQL volume *and* sales capacity, new ARR is driven by demos × win-rate, tickets scale with the customer base — so the correlations that surface are real, not decorative. The "What drives New ARR" ranking and the R² read-out are computed, not hard-coded.

## Headcount model (method, not vibes)

- **Recommended total heads = ARR ÷ target ARR/employee** (default $165K/FTE → ~49 heads at $8M).
- Allocated across 12 functions using SaaS benchmarks for a company scaling toward $100M (R&D ~38%, GTM ~29%, CS/Support ~14%, G&A ~9%).
- Each department shows **actual vs benchmark target** — so over/under-staffing is visible at a glance. (The model flags Sales *under*-hiring while pushing growth, and Support *over* on heads yet *under* on CSAT — a process problem, not a hiring one.)

## Board-level efficiency ratios

Burn multiple · Rule of 40 · ARR/employee · Gross margin · NRR · CAC payback — the numbers a board actually reads when it sees "$8M ARR on $10M burn."

## Common productivity framework

Every one of the 12 teams (Sales, Marketing, BD, Product, Engineering, QA, Data, PM, Implementation, Support, Ops, HR) is measured on the same five steps so they're directly comparable:

**Capacity → Utilization → Output → Target vs Achievement → Efficiency index**

Then each team layers on its own bespoke output metrics (Sales: demos / talk-time / win-rate; Engineering: velocity / cycle time / uptime; Support: tickets / CSAT / resolution; etc.). Achievement is **direction-aware** — for "lower is better" metrics (time-to-value, time-to-hire, escape rate), beating target correctly reads as *over* 100%.

## Live assumptions

The ⚙︎ Assumptions panel exposes the four load-bearing levers — **ARR, net burn, target ARR/FTE, YoY growth** — and every ratio, chart, and headcount recommendation recomputes instantly. Drag ARR/FTE and watch each department's target move.

## Plugging in real data

Replace the `buildSeries()` output and the `DEPTS` snapshot with real values in the same shape. No other change needed — the schema *is* the contract.

---

*Sample model — all figures are synthetic and anchored on the stated unit economics, not live Lyzr data.*
