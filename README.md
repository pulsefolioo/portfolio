# PulseFolio

A single-file, client-side crypto portfolio tracker for **PulseChain, Ethereum, Base, Arbitrum, and BNB Chain**. Paste one or more wallet addresses and see your token balances, farm/staking positions, and total USD value — no backend, no account, no wallet connection required.

🔗 **[Live demo](#)** — replace with your GitHub Pages / hosting link

![PulseFolio](https://img.shields.io/badge/type-static%20HTML-8b3bff) ![No backend](https://img.shields.io/badge/backend-none-35d68b) ![License](https://img.shields.io/badge/license-MIT-00d4ff)

---

## ✨ Features

- **Multi-network support** — PulseChain, Ethereum, Base, Arbitrum, and BNB Chain, plus a combined PulseChain + Ethereum (+ optional extras) view.
- **Multiple portfolios** — create, rename, and switch between several saved portfolios, each with its own addresses, custom tokens, and network settings, all stored independently in your browser.
- **Multiple wallet addresses per portfolio** — track several addresses together as one combined portfolio.
- **Automatic token discovery** — known tokens per network plus the ability to add any ERC-20 by contract address.
- **Manual token tracking** — add tokens you hold on an exchange (Binance, Coinbase, etc.) or on a chain this app doesn't scan directly, by symbol via CoinGecko, and track their live USD value alongside your on-chain balances.
- **Watchlist** — track token prices without needing a wallet address at all.
- **Farms & staking** — HEX staking and PulseX farm/MasterChef positions, with a toggle to merge them into the main token list or view separately.
- **Live pricing** — powered by [DexScreener](https://dexscreener.com/) (on-chain pairs) and [CoinGecko](https://www.coingecko.com/) (manual tokens, watchlist).
- **Portfolio value chart** — snapshots of your total portfolio value over time, rendered as an inline chart.
- **"ATH Dream" & Multiplier modes** — see what your portfolio would be worth at each token's all-time high, or at an arbitrary price multiplier.
- **Offline-friendly caching** — the last successful fetch is cached locally and shown instantly (marked as stale) while fresh data loads in the background.
- **Privacy-first** — everything lives in your browser's `localStorage`. Addresses, custom tokens, and settings are never sent to or stored on any server.

## 🖥️ Tech stack

- Plain **HTML/CSS/JavaScript** — a single static file, no build step, no framework.
- [ethers.js v5](https://docs.ethers.org/v5/) for all on-chain reads (balances, staking contracts, farm contracts) via public RPC endpoints.
- [Tabler Icons](https://tabler.io/icons) for iconography, [Google Fonts](https://fonts.google.com/) (Space Grotesk / Inter) for typography.
- [DexScreener API](https://docs.dexscreener.com/api/reference) for token prices and liquidity data.
- [CoinGecko API](https://www.coingecko.com/en/api) for manual token/watchlist price lookups.
- A strict `Content-Security-Policy` locking network access down to only the RPCs and APIs the app actually uses.

## 🚀 Getting started

No build step, no dependencies to install.

1. Download `index.html` from this repo.
2. Open it directly in a browser, **or** host it anywhere that serves static files (GitHub Pages, Netlify, Vercel, S3, etc.):

   ```bash
   # Example: quick local preview
   npx serve .
   ```

3. Paste a wallet address (or use the demo address) and hit **Check**.

## 📖 Usage

- **Add addresses** — paste one or more `0x…` addresses to check them together as a single portfolio.
- **Switch networks** — use the network selector, or combine PulseChain + Ethereum (and optionally Base/Arbitrum/BNB Chain) into one view.
- **Multiple portfolios** — use the portfolio switcher (visible while editing addresses) to create a new portfolio, rename the current one, or delete it. Each portfolio remembers its own addresses, tokens, and network choice.
- **Add missing tokens** — click *"Missing a token? Add it"* to track any ERC-20 by contract address, or manually add a token from any network/exchange by symbol.
- **Watchlist** — track token prices without linking them to a wallet balance.
- **Farms & staking** — see HEX stakes and PulseX farm positions under the *Farms & staking* tab.

## 🔒 Privacy & data storage

PulseFolio makes no server-side calls of its own — every request goes straight from your browser to public RPC nodes, DexScreener, or CoinGecko. Wallet addresses, custom/manual tokens, watchlist items, portfolios, and settings are stored **only** in your browser's `localStorage` and are never transmitted anywhere else. Clearing your browser data will remove them.

## ⚠️ Disclaimer

PulseFolio is a read-only balance/price viewer. It never asks for a seed phrase or private key, and cannot move funds. Prices are sourced from third-party APIs (DexScreener, CoinGecko) and may be delayed, incomplete, or inaccurate — always verify important figures independently before making financial decisions. This is not financial advice.

## 🤝 Contributing

Issues and pull requests are welcome. Since this is a single static HTML file, most changes can be made and tested by simply editing `index.html` and opening it in a browser.

## 📄 License

[MIT](LICENSE)
