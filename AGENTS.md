# AGENTS.md

Single-page static dashboard (Robinhood Markets, Inc. / HOOD tracker) deployed via
GitHub Pages. Independent repo; do not mix with spacex-dashboard, tempus-dashboard, nvda-dashboard,
micron-dashboard, or lam-research-dashboard.

## Rules
- `index.html` is the entire site. It is generated from the `hood-dashboard`
  web artifact: do not hand-edit the deployed copy; edit the artifact and re-export.
- Deploy = overwrite `index.html` on the `main` branch root. GitHub Pages serves
  from `main` / `(root)`. No build step.
- Keep the page self-contained (inline CSS/JS, data URIs). No external JS libraries.
- Live quotes: `quote.json` snapshot in the repo root, refreshed every 15 minutes
  during NYSE trading hours by `.github/workflows/quote.yml` (Nasdaq official API,
  real-time, delayMin=0). The page reads it same-origin; client-side fallback chain
  is quote.json -> Nasdaq direct -> Yahoo Finance -> Stooq (hood.us).
  Never claim tick-level real time.
- Page copy in Chinese; code, comments, and commit messages in English.
- Cite every data point with source link and date. Distinguish verified facts,
  estimates, and unverifiable items; never merge conflicting calibers into one
  "certain" value.
- No secrets in the repo. No destructive git operations (no hard reset, no force push).
