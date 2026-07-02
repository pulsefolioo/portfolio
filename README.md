# PulseFolio

A lightweight, single-file portfolio tracker for wallets on [PulseChain](https://pulsechain.com/). Paste one or more wallet addresses and get an instant overview of token balances, HEX stakes, and PulseX LP farm positions — all in the browser, no backend required.

![PulseChain](https://img.shields.io/badge/chain-PulseChain-8b3bff)
![No backend](https://img.shields.io/badge/backend-none-35d68b)
![License](https://img.shields.io/badge/license-MIT-informational)

## Features

- **Multi-wallet portfolio** — track one address or combine several into a single merged view.
- **Token balances** — reads a curated whitelist of tokens directly via RPC using `Multicall3`, so it works even without an indexer/explorer API.
- **Live pricing** — fetches USD prices and 24h change from [DexScreener](https://dexscreener.com/).
- **HEX staking** — lists your active HEX stakes with progress and unlock countdown.
- **PulseX farms** — reads your `MasterChef` LP farm positions and breaks each one down into its two underlying tokens.
- **Flexible display** — toggle whether farm tokens are shown separately or merged into your token balances.
- **Locally saved portfolio** — your address list is remembered in the browser so you don't have to re-enter it every visit.
- **Zero backend** — a single `index.html` file; all reads happen client-side against the PulseChain RPC and public APIs.

## Getting started

No build step, no dependencies to install. Just open the file in a browser:

```bash
# clone the repo
git clone https://github.com/<your-username>/pulsefolio.git
cd pulsefolio

# open it directly...
open index.html          # macOS
xdg-open index.html      # Linux

# ...or serve it locally (recommended, some browsers restrict local file APIs)
python3 -m http.server 8000
# then visit http://localhost:8000
```

You can also just double-click `index.html` — it works as a static file with no server at all.

## Usage

1. Paste a PulseChain wallet address (`0x...`) into the address field.
2. Add more addresses if you want to combine several wallets into one portfolio view.
3. Click **Check** to load balances, prices, HEX stakes, and PulseX farm positions.
4. Use the **Tokens** / **Farms & staking** tabs to switch views, and the **Farm tokens** toggle to show LP-derived tokens separately or merged into your main token list.
5. Your address list is saved automatically so it's ready next time you open the page.

## Privacy

Wallet addresses you enter are stored **only locally in your browser** (`localStorage`). They are never sent to, or stored on, any server — PulseFolio has no backend at all. Clearing your browser data (or using "Create new") removes them.

All balance/price lookups happen directly from your browser to the PulseChain RPC and to DexScreener's public API — no intermediary server sees your addresses.

## How it works

- **Balances**: instead of relying on a block explorer API, PulseFolio batches `balanceOf` calls for a whitelist of known token contracts (`KNOWN_TOKENS`) through the `Multicall3` contract, in a single RPC round-trip.
- **Prices**: token prices and 24h changes come from the DexScreener API, filtered to PulseChain pairs.
- **HEX staking**: reads `stakeCount` / `stakeLists` / `currentDay` from the HEX contract to compute active stakes, progress, and days remaining.
- **PulseX farms**: reads `userInfo` / `poolInfo` from the `MasterChef` contract for every pool, then values each LP position by splitting it into its two underlying tokens using on-chain reserves.
- **RPC fallback**: if the primary RPC endpoint fails, requests automatically retry against a fallback endpoint.

## Adding tokens

The token list is a manually curated whitelist (`KNOWN_TOKENS` in `index.html`) rather than an auto-discovered list, so it stays fast and predictable. To track an additional token, add an entry with its contract address, symbol, name, and decimals:

```js
{ address: '0x...', symbol: 'TOKEN', name: 'Token Name', decimals: 18 },
```

## Tech stack

- Vanilla HTML / CSS / JavaScript — no framework, no build tools
- [ethers.js v5](https://docs.ethers.org/v5/) for contract calls and formatting
- [Multicall3](https://github.com/mds1/multicall) for batched on-chain reads
- [DexScreener API](https://docs.dexscreener.com/) for token pricing
- [Tabler Icons](https://tabler.io/icons) for UI icons

## Disclaimer

PulseFolio is a read-only viewer. It never requests wallet signatures, private keys, or transaction approval — it only reads public on-chain data for the addresses you provide. Prices are sourced from third-party APIs and may be delayed or inaccurate; do not rely on this tool for financial decisions.

## License

MIT
