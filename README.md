# PulseFolio

**PulseFolio** is a single-file, client-side, read-only portfolio tracker for **PulseChain**, **Ethereum**, and a handful of EVM sidechains — built as one self-contained `index.html`, with no backend, no wallet connection, and no data ever leaving the browser except direct calls to public RPCs and price APIs.

Just paste one or more wallet addresses and get a live, multi-chain view of your holdings, its value over time, and a few PulseChain/HEX-ecosystem-specific extras like ATH "dream" pricing.

![PulseFolio](https://img.shields.io/badge/type-single--file%20app-8b3bff) ![No backend](https://img.shields.io/badge/backend-none-35d68b) ![License](https://img.shields.io/badge/license-see%20below-555)

---

## Features

- **Multi-chain balances** — track token balances on:
  - PulseChain (native)
  - Ethereum
  - Base, Arbitrum, BNB Chain (optional, added on top in *combined* mode)
- **Multiple wallets at once** — enter any number of addresses and see them aggregated into a single portfolio.
- **Multiple saved portfolios** — create, rename, switch between, and delete separate portfolios (e.g. "Main", "Trading", "Cold storage"), each with its own addresses, network selection, and custom/manual tokens, stored independently.
- **Combined view** — merge PulseChain + Ethereum (+ optionally Base/Arbitrum/BNB) into one unified total.
- **Manual tokens** — add any token by symbol via CoinGecko lookup and enter a holding amount by hand, for anything not detectable on-chain (e.g. CEX balances, illiquid tokens).
- **Farm & staked tokens** — HEX stakes and PulseX LP farm holdings can be folded into or split out from the main token list.
- **Portfolio value chart** — an inline SVG chart of total portfolio value over time (24h / 7d / 30d), built from local snapshots recorded on every refresh. History is scoped per network/wallet context, so switching wallets or networks never mixes unrelated history together, and stale/out-of-order responses (e.g. fast wallet switching) can't corrupt it or flash the wrong chart on screen.
- **ATH Dream mode** — see what your PulseChain/HEX-ecosystem portfolio would be worth at each token's all-time-high price.
- **Multiplier mode** — apply a custom price multiplier across the board for "what if" scenarios.
- **Currency display** — toggle between USD, PLN, and BTC (click the total value to cycle).
- **Light/dark theme.**
- **English / Polish UI** (`en` / `pl`), fully translatable via a simple string table.
- **Client-side caching** — token prices, DexScreener prices, CoinGecko icons, and portfolio snapshots are cached locally (`localStorage`) with sensible TTLs, so the app stays fast and usable offline-ish between refreshes.
- **No wallet connection, no signing, no write access** — addresses are just looked up read-only via public RPC `eth_call`s. Nothing is ever transacted or approved.

## How it works

PulseFolio is a **single static HTML file**. There is no server, no build step, and no database:

- Balances are fetched directly from public JSON-RPC endpoints (PulseChain, Ethereum, Base, Arbitrum, BNB Chain) using [ethers.js](https://docs.ethers.org/v5/), loaded from a CDN.
- Prices come from [DexScreener](https://docs.dexscreener.com/) and [CoinGecko](https://www.coingecko.com/en/api) public APIs.
- Everything you enter (addresses, portfolios, settings, custom tokens, price/history caches) is stored in the browser's `localStorage`. Nothing is sent to any first-party server, because there isn't one.
- A strict `Content-Security-Policy` locks the page down to only the RPC/API domains it actually needs.

## Getting started

No installation required.

1. Download `index.html`.
2. Open it in any modern browser (Chrome, Firefox, Edge, Safari).
3. Paste one or more wallet addresses and click **Load**.

That's it — you can also just double-click the file locally, or serve it from any static host (GitHub Pages, Netlify, S3, etc.) since it has no server-side dependencies.

```bash
# Optional: serve it locally instead of opening the file directly
python3 -m http.server -d . 8080
# then visit http://localhost:8080/index.html
```

## Supported networks

| Network | Role |
|---|---|
| **PulseChain** | Primary/default network |
| **Ethereum** | Primary alternative network |
| **Base** | Optional, combined mode only |
| **Arbitrum** | Optional, combined mode only |
| **BNB Chain** | Optional, combined mode only |

Switch networks from the network selector, or turn on **combined mode** to merge PulseChain + Ethereum (and any optional extra networks you pick) into a single total.

## Privacy & security

- **Read-only.** PulseFolio never asks you to connect a wallet, sign a message, or approve a transaction — it only reads public on-chain balances for the addresses you type in.
- **No backend.** There is no server component to log your addresses or portfolio value; all state lives in your browser's `localStorage`.
- **Locked-down CSP.** The page's Content-Security-Policy restricts script/style/connect sources to exactly what's needed (ethers.js CDN, Google Fonts/cdnjs for styling, the RPC endpoints, DexScreener, and CoinGecko) and blocks `object-src`, `base-uri`, `form-action`, and `frame-ancestors` outright.
- Clearing your browser's site data for this page will erase all saved portfolios, history, and preferences — there is no cloud backup.

## Disclaimer

Token contract addresses for secondary networks (Base, Arbitrum, etc.) are best-effort and should be independently verified on a block explorer before you rely on them. ATH/Multiplier "dream" pricing is a hypothetical display mode only — it does not reflect real, tradable value and is excluded from the saved value history/chart.

This is not financial advice, and PulseFolio is not affiliated with PulseChain, HEX, or any token/project it happens to display.

## License

See repository license file (or add one — none specified here).
