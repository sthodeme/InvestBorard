# PortfolioWatch

A zero-dependency, offline-capable personal investment dashboard for tracking
ETFs, Mutual Funds, and Shares across NSE/BSE, DAX, and NYSE/NASDAQ.

---

## Quick Start

1. Copy the entire `portfoliowatch/` folder to any machine.
2. Open `index.html` in any modern browser (Chrome, Firefox, Edge, Safari).
3. Done — no server, no install, no internet required for the UI itself.

> **Note:** Live price fetching uses Yahoo Finance via a public proxy.
> You need an internet connection to refresh prices.

---

## File Structure

```
portfoliowatch/
├── index.html              ← The entire app (open this)
├── README.md               ← This file
└── data/
    ├── portfolio.json      ← Your instruments (bulk-edit here)
    └── exchanges.json      ← Exchange config reference
```

---

## Managing Your Portfolio

### Option A — Via the UI (recommended)
- Click **+ Add instrument** to add a new ETF/MF/Share
- Click ✎ to edit any instrument
- Click ✕ to delete
- Use the **Exchange tabs** to switch between NSE, DAX, NYSE
- Use the **View dropdown** to switch between Portfolio and Watchlist
- Click **⬇ Export JSON** to download your current data as `portfolio.json`
- Click **⬆ Import JSON** to load a previously exported file

### Option B — Edit portfolio.json directly
Edit `data/portfolio.json` in any text editor, then use **⬆ Import JSON** in
the app to load your changes. Each instrument follows this schema:

```json
{
  "id": 1,
  "ticker": "NIFTYBEES.NS",
  "name": "Nippon Nifty BeES ETF",
  "type": "ETF",
  "qty": 200,
  "buyPrice": 220.00,
  "exchange": "NSE",
  "view": "portfolio",
  "notes": "SIP monthly"
}
```

| Field     | Values                                  |
|-----------|-----------------------------------------|
| type      | `ETF` / `MF` / `Share`                  |
| exchange  | `NSE` / `DAX` / `NYSE`                  |
| view      | `portfolio` / `watchlist`               |
| notes     | any string (shown as tooltip on hover)  |

---

## Ticker Symbol Format (Yahoo Finance)

| Exchange       | Suffix    | Example           |
|----------------|-----------|-------------------|
| NSE (India)    | `.NS`     | `HDFCBANK.NS`     |
| BSE (India)    | `.BO`     | `HDFCBANK.BO`     |
| XETRA/DAX      | `.DE`     | `EXS1.DE`         |
| NYSE / NASDAQ  | none      | `SPY`, `AAPL`     |

---

## Data Persistence

All data is saved automatically to your **browser's localStorage** after
every change. This means:

- Your data survives page refreshes and browser restarts.
- Data is stored per-browser, per-machine.
- To move data to another machine: **Export JSON** → copy file → **Import JSON**.

---

## Keyboard Shortcuts

| Key | Action             |
|-----|--------------------|
| `n` | New instrument     |
| `r` | Refresh prices     |
| `Esc` | Close modal      |

---

## Adding More Exchanges

Edit the `EXCHANGES` array near the top of `index.html`:

```javascript
const EXCHANGES = [
  {id:'NSE',  label:'NSE / BSE',      currency:'INR', symbol:'₹', color:'#38bdf8'},
  {id:'DAX',  label:'DAX',            currency:'EUR', symbol:'€', color:'#a78bfa'},
  {id:'NYSE', label:'NYSE / NASDAQ',  currency:'USD', symbol:'$', color:'#3dd68c'},
  // Add more here:
  {id:'LSE',  label:'LSE',            currency:'GBP', symbol:'£', color:'#f5a623'},
];
```

---

## Planned Enhancements

- [ ] Charts: allocation donut + P&L bar chart per exchange
- [ ] Consolidated view: all exchanges with forex conversion to INR
- [ ] Price alerts
- [ ] Transaction history / cost averaging tracker
- [ ] Export to Excel / CSV
