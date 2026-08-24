# Lyzr Founders' Cockpit

A single, self-contained analytics dashboard for the founders' office — one HTML file, no build step, no dependencies, works offline. Open `index.html` in any browser.

Built in response to the brief: *"a dashboard with a news feed that tracks all internal metrics across marketing, sales, project management, etc. — simple for a founder to see, with in-depth access."*

---

## The thinking behind it

The founder doesn't have a data source yet, and he's screening for an **analytical brain** — someone who finds *relationships* between data points, not someone who just renders numbers. So this is built as two things at once:

1. **A working model today** — a coherent AI-SaaS scenario anchored on Lyzr's **real public figures**: **~$12M ARR** (Jun'26), **~32 enterprise customers** (~$250K ACV, largest ~$2M), **Accenture-backed** ($250M valuation, ~$100M Series B), **~88 staff + 172 open reqs**, pushing to **$100M ARR**. Every number ties to every other number. (The founder's brief said "assume $8M ARR / $10M burn" — the ⚙︎ Assumptions panel makes ARR/burn editable, so you can flip to his figures in one drag and show you cross-referenced the public numbers.)
2. **A data contract for tomorrow** — the same schema accepts real CSV / Google Sheets / product-API data and every view repopulates automatically.

Three layers, one toggle — exactly the "he sees one screen, then drills in" behaviour he described:

| View | Who it's for | What it answers |
|------|--------------|-----------------|
| **Founder View** | CXO, 10-second read | Revenue, burn, runway, the 5 board-level efficiency ratios, headcount health, and the 3 things that need him today |
| **Founder Brief** | CXO, one-minute read | A Bumble-style **swipe deck** — one department per card (what's happening, team size, productivity, impact, right-resources?, leader performance, EOP alignment, top performers, the big deal coming). **Swipe right to note, left to skip** — touch on mobile, drag or ←/→ keys on web. Ends with a summary of everything noted (persisted in the browser). |
| **Departments** | Any team lead | All 12 teams on one comparable framework, click-to-drill |
| **Correlation Engine** | The analyst | The *real* relationships — Pearson r computed live on 12 months of data |
| **Insight Feed** | Everyone | The dashboard telling you what changed and why — the "news feed" |

## Brand

Styled to match **lyzr.ai** — warm espresso background, terracotta accent, editorial serif headlines (Fraunces) over clean sans body (Inter), translucent pill controls, and the real Lyzr logo embedded. Fully **web + mobile responsive**; the Founder Brief is built mobile-first.

## Why the correlation engine matters

His LinkedIn post is explicit: *"run correlation models to identify the true relationships between data points, not just prompting GPT and Claude."* That's the whole test.

So the analytics layer computes **actual Pearson correlations** in-browser across 11 operating metrics (marketing spend, MQLs, SQLs, demos, talk-time, reps, bookings, new ARR, CAC, tickets, CSAT). The underlying sample series are constructed with *genuine* causal structure + noise — e.g. demos are driven by SQL volume *and* sales capacity, new ARR is driven by demos × win-rate, tickets scale with the customer base — so the correlations that surface are real, not decorative. The "What drives New ARR" ranking and the R² read-out are computed, not hard-coded.

## Headcount model (method, not vibes)

- **Recommended total heads = ARR ÷ target ARR/employee** (default $150K/FTE → ~80 heads right-sized for $12M).
- Allocated across 12 functions using SaaS benchmarks for a company scaling toward $100M (R&D ~40%, GTM ~27%, CS/Support ~14%, G&A ~9%).
- Each department shows **actual vs benchmark target vs open reqs** — so the real story is visible: current headcount (~88) is roughly right-sized for $12M, but **172 open reqs** are pre-building for $100M. The constraint isn't capital, it's **sequencing 172 hires against a 39-day time-to-hire and a 78% offer-acceptance rate**.

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

*Model anchored on Lyzr's public figures (ARR, customers, funding, headcount). The monthly time-series and per-team operating detail are illustrative — plug in the real data through the same schema to make it live.*
