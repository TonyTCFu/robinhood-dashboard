# MEMORY.md

Robinhood Markets, Inc. (NASDAQ: HOOD) tracking dashboard. Static single page
served by GitHub Pages. This repo is independent of `spacex-dashboard`,
`tempus-dashboard`, `nvda-dashboard`, `micron-dashboard`, and
`lam-research-dashboard`; keep them separate (own quote.json, own workflow,
own public link).

## Deployment
- Public link: https://tonytcfu.github.io/robinhood-dashboard/
- Source: `index.html` at the `main` branch root, generated from the
  `hood-dashboard` web artifact (re-export on data updates; do not hand-edit).
- GitHub Pages setting: Deploy from a branch / main / /(root).

## Quote snapshot
- `quote.json` at repo root; refreshed by `.github/workflows/quote.yml`
  (cron `*/15 13-21 * * 1-5` UTC, Mon-Fri, plus manual dispatch).
- Source: Nasdaq official API (`api.nasdaq.com/api/quote/HOOD/info`), real-time.
- Page fallback chain: quote.json -> Nasdaq direct -> Yahoo Finance -> Stooq (hood.us).
- Format: {"symbol":"HOOD","price":..,"netChange":..,"pctChange":..,"prevClose":..,
  "quoteTime":"YYYY-MM-DD HH:MM","status":"intraday|postmarket|close","source":"Nasdaq"}.
- The workflow uses `zoneinfo.ZoneInfo("America/New_York")` for the ET wall
  clock (correct across EDT/EST transitions). Cron 13-21 UTC covers
  09:30-17:00 ET in EDT and 08:00-16:00 ET in EST.

## Icon
- robinhood.com official favicon.ico (15,086 bytes, three 48x48 icons, verified
  real), converted to a 48px PNG and embedded as data URI.
- robinhood.com/apple-touch-icon.png returns an HTML page, NOT an image;
  never use it as an icon.

## Data baseline
- Price/financials/short/analyst snapshot: 2026-10-01 close ($111.15, -1.20%).
- Q2 2026 (2026-07-29): total net revenue $1.31B (+32% YoY), GAAP diluted EPS
  $0.62 (incl. ~$0.14 one-time deconsolidation gain), net income $573M,
  adj. EBITDA $741M (~57%); event contracts revenue $156M (>10x), crypto
  revenue $100M (-38%); platform assets $369B, record net deposits $21.7B,
  Gold subscribers 4.84M. MAU no longer disclosed (funded customers 28.4M).
- Short interest (FINRA 2026-09-15): 36,165,147 shares, 4.65% of float,
  ~1.5 days to cover (up from 35,537,085 prior).
- Analysts: 17-firm ladder on page (StoneX $170 top, KBW $115 at bottom);
  consensus averages differ by aggregator (~$131-133), shown side by side.
- Options (2026-10-01, OptiView only; FlashAlpha has no HOOD data):
  dealer GEX positive (+$2.77B), call wall $120, put wall $100,
  max pain $100, P/C OI 0.68, 30d ATM IV 53.0% (rank 42/100).
  No Gamma Flip value is displayed.
- Q3 2026 earnings date unconfirmed: OptiView 2026-11-02 vs MarketBeat
  11-04 after close (estimate). Marked as pending confirmation.
