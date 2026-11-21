# NAVscope Replay

Replay-based mutual fund NAV estimator with explainable holdings contributions.

[Open the replay dashboard](https://talwarmohnish.github.io/navscope-replay/) · [Download the complete source](./NAVscope-source.zip)

## Demo

1. Choose one of the two Direct Growth funds.
2. Play the synthetic session, then pause at a tick.
3. Open **Backend** to see the displayed NAV reconcile with the portfolio-weighted return. Check which stock drove the move and how much of the fund was priced.

## Backend and calculation

The local backend uses **Node.js**, its built-in HTTP server and Fetch. `serve.mjs` serves the dashboard, and `worker.mjs` implements `GET /api/sources?fund=…` for AMFI NAV and fund-house holdings. AUM comes from dated fund-house snapshots.

The browser runs `site/market.mjs`. It matches stock quotes to disclosed holdings, sums each holding's weight times its return from the NAV-aligned close, and applies that return to the official NAV. Unpriced positions contribute zero. Coverage reports the share of NAV priced by the model.

GitHub Pages serves the self-contained `index.html` with dated official snapshots and synthetic stock moves. Extract the source archive and run `node serve.mjs` with Node.js 22+ to use the local backend. The optional IndianAPI quote check uses a local environment variable. This replay uses synthetic stock prices and is for education.
