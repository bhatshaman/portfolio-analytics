# Portfolio Analytics Tool

> A web-based portfolio analytics platform for investors to upload their holdings and receive deep financial insights — built with Python, Flask, and React.

![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python) ![Flask](https://img.shields.io/badge/Flask-2.x-black?logo=flask) ![React](https://img.shields.io/badge/React-Frontend-61DAFB?logo=react) ![Status](https://img.shields.io/badge/Status-In%20Development-yellow)

---

## About

Portfolio Analytics is a full-stack financial analytics tool that allows investors to upload a CSV of their current holdings and receive a comprehensive breakdown of their portfolio's performance, risk, and composition — benchmarked against the S&P 500.



---

## Features

- **Sector & Asset Allocation** — Breakdown of portfolio exposure by sector, dollar amount invested, and number of holdings per sector
- **Portfolio Performance** — Cumulative returns, annualized return, and daily P&L over a 1-year lookback period
- **Benchmark Comparison** — Portfolio returns vs S&P 500 (SPY), including alpha and tracking error
- **Risk Metrics** — Sharpe ratio, Sortino ratio, Value at Risk (VaR 95%), Conditional VaR (CVaR), and Maximum Drawdown

---

## Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python, Flask |
| Frontend | React |
| Database | PostgreSQL |
| Financial Data | yfinance |
| Data Processing | pandas, NumPy |

---

## How It Works

The tool follows a simple 3-step flow:

```
1. Select Analysis   →   2. Upload CSV   →   3. View Results
   (multi-select)        (holdings file)      (metrics + charts)
```

Users select which analyses they want (performance, risk, benchmark, allocation), upload a CSV of their current holdings, and receive a full analytics dashboard — no broker connection or login required.

---

## Getting Started

### Prerequisites
- Python 3.11+
- Node.js 18+
- PostgreSQL

### Installation

```bash
# Clone the repository
git clone https://github.com/bhatshaman/portfolio-analytics.git
cd portfolio-analytics

# Install Python dependencies
pip install -r requirements.txt

# Start the Flask server
cd server
python api.py
```

The API will be running at `http://localhost:8000`.

---

## CSV Format

Upload a CSV with the following columns:

| Column | Type | Description |
|---|---|---|
| `ticker` | string | Stock ticker symbol (e.g. AAPL) |
| `quantity` | float | Number of shares held |
| `avg_buy_price` | float | Average purchase price per share |

**Example:**
```csv
ticker,quantity,avg_buy_price
AAPL,25,145.30
MSFT,15,280.50
SPY,20,420.00
```

A demo portfolio CSV is available at [`data/demo_portfolio.csv`](data/demo_portfolio.csv) — use this to try the tool without your own data.

---

## API Reference

### `POST /submit`

Accepts a portfolio CSV and returns a full analytics response.

**Request:**
```
Content-Type: text/csv
Body: CSV file contents
```

**Response:**
```json
{
  "analytics": {
    "holdings": {
      "sector": [...],
      "portfolio_allocation": [...]
    },
    "performance": {
      "annualized_return": 0.287,
      "portfolio_perf": {...},
      "benchmark_perf": {...},
      "portfolio_alpha": 0.058,
      "tracking_error": 0.002,
      "return_series": {...},
      "daily_pl_series": {...}
    },
    "risk": {
      "sharpe_ratio": 1.16,
      "sortino_ratio": 1.47,
      "portfolio_var": -0.0139,
      "portfolio_cvar": -0.0262,
      "portfolio_max_drawdown": -0.143
    }
  }
}
```

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).