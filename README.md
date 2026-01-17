# NSE Equity MFT Strategies - Zerodha

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat&logo=python&logoColor=white)](https://python.org)
[![Zerodha](https://img.shields.io/badge/Zerodha-Kite-387ED1?style=flat)](https://kite.zerodha.com/)
[![NSE](https://img.shields.io/badge/NSE-Equity-FF6600?style=flat)](https://www.nseindia.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Medium-frequency trading strategies for NSE Cash Market (Equity) using Zerodha Kite Connect API. Designed for retail and semi-institutional traders.

---

## Overview

| Metric | Value |
|--------|-------|
| **Timeframe** | 1min - 15min |
| **Broker** | Zerodha (Kite Connect) |
| **Instruments** | NIFTY 50, Large & Mid caps |
| **Language** | Python |

---

## Features

- **Kite Connect Integration** - Full API support for orders, positions, holdings
- **Intraday Strategies** - Momentum, mean reversion, breakout, gap trading
- **Swing Trading** - Multi-day position strategies
- **Sector Rotation** - Relative strength based sector selection
- **Backtesting** - Historical data backtesting with realistic fills
- **Paper Trading** - Simulated trading without real orders
- **Alerts** - Telegram/Email notifications for signals

---

## Strategies

| Strategy | Timeframe | Description | Win Rate Target |
|----------|-----------|-------------|-----------------|
| **Opening Range Breakout** | 15m | Breakout from first 15min range | 55%+ |
| **Gap Trading** | 9:15 | Trade gap up/down at market open | 50%+ |
| **VWAP Reversion** | 5m | Mean reversion to VWAP | 55%+ |
| **Momentum Scalping** | 1m - 5m | Ride intraday momentum | 50%+ |
| **Sector Momentum** | Daily | Rotate into strong sectors | 55%+ |
| **Support/Resistance** | 15m | Bounce trading at key levels | 55%+ |
| **EMA Crossover** | 5m - 15m | Trend following with EMAs | 50%+ |

---

## Architecture

```
┌─────────────────────────────────────────────────────────────────────────┐
│                 NSE EQUITY MFT - ZERODHA KITE                            │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌───────────────────────────────────────────────────────────────────┐ │
│  │                      ZERODHA KITE CONNECT                          │ │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐               │ │
│  │  │   Orders    │  │  Positions  │  │   Market    │               │ │
│  │  │    API      │  │    API      │  │   Data API  │               │ │
│  │  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘               │ │
│  │         └────────────────┴────────┬───────┘                      │ │
│  └──────────────────────────────────┬┴──────────────────────────────┘ │
│                                     ▼                                  │
│  ┌───────────────────────────────────────────────────────────────────┐ │
│  │                      STRATEGY ENGINE                               │ │
│  │                                                                    │ │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐            │ │
│  │  │   Scanner    │  │   Signal     │  │    Risk      │            │ │
│  │  │  (Watchlist) │  │  Generator   │  │   Manager    │            │ │
│  │  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘            │ │
│  │         └─────────────────┴─────────────────┘                    │ │
│  │                           │                                       │ │
│  │  ┌────────────────────────▼───────────────────────────────────┐  │ │
│  │  │                   STRATEGIES                                │  │ │
│  │  │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌───────────────┐ │  │ │
│  │  │  │   ORB    │ │   Gap    │ │   VWAP   │ │   Momentum    │ │  │ │
│  │  │  │ Breakout │ │ Trading  │ │Reversion │ │   Scalping    │ │  │ │
│  │  │  └──────────┘ └──────────┘ └──────────┘ └───────────────┘ │  │ │
│  │  └────────────────────────────────────────────────────────────┘  │ │
│  └──────────────────────────────────┬───────────────────────────────┘ │
│                                     ▼                                  │
│  ┌───────────────────────────────────────────────────────────────────┐ │
│  │                      EXECUTION & MONITORING                        │ │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐            │ │
│  │  │    Order     │  │   Position   │  │     P&L      │            │ │
│  │  │   Manager    │  │   Tracker    │  │   Dashboard  │            │ │
│  │  └──────────────┘  └──────────────┘  └──────────────┘            │ │
│  └───────────────────────────────────────────────────────────────────┘ │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Project Structure

```
NSE-equity-MFT-strategies-zerodha/
│
├── src/
│   ├── strategies/
│   │   ├── base_strategy.py
│   │   ├── orb_breakout.py
│   │   ├── gap_trading.py
│   │   ├── vwap_reversion.py
│   │   ├── momentum.py
│   │   ├── sector_rotation.py
│   │   └── support_resistance.py
│   │
│   ├── broker/
│   │   ├── kite_client.py
│   │   ├── orders.py
│   │   └── positions.py
│   │
│   ├── scanner/
│   │   ├── stock_scanner.py
│   │   ├── sector_scanner.py
│   │   └── filters.py
│   │
│   ├── indicators/
│   │   ├── vwap.py
│   │   ├── ema.py
│   │   ├── rsi.py
│   │   └── atr.py
│   │
│   ├── risk/
│   │   ├── position_sizer.py
│   │   ├── stop_loss.py
│   │   └── portfolio_risk.py
│   │
│   ├── data/
│   │   ├── market_data.py
│   │   └── historical.py
│   │
│   └── utils/
│       ├── config.py
│       ├── logger.py
│       └── notifications.py
│
├── backtest/
│   ├── engine.py
│   └── metrics.py
│
├── config/
│   └── config.yaml
│
├── tests/
├── notebooks/
├── requirements.txt
└── README.md
```

---

## Quick Start

```bash
# Clone repository
git clone https://github.com/pranay123-stack/NSE-equity-MFT-strategies-zerodha.git
cd NSE-equity-MFT-strategies-zerodha

# Install dependencies
pip install -r requirements.txt

# Configure Kite API
cp config/config.example.yaml config/config.yaml

# Run backtest
python -m backtest.engine --strategy orb_breakout --symbol RELIANCE

# Run live (paper mode)
python -m src.main --strategy momentum --mode paper
```

---

## Configuration

```yaml
# config/config.yaml
zerodha:
  api_key: ${KITE_API_KEY}
  api_secret: ${KITE_API_SECRET}
  user_id: ${KITE_USER_ID}

trading:
  watchlist:
    - RELIANCE
    - TCS
    - HDFCBANK
    - INFY
    - ICICIBANK
  product: MIS  # MIS for intraday, CNC for delivery
  timeframe: 5m

strategy:
  name: orb_breakout
  params:
    range_minutes: 15
    breakout_buffer: 0.1  # percent
    stop_loss_percent: 0.5
    target_percent: 1.0
    entry_time: "09:30"
    exit_time: "15:10"

risk:
  max_loss_per_trade: 1000
  max_daily_loss: 5000
  max_positions: 3
  position_size_percent: 5  # of capital
```

---

## Indicators

| Indicator | Usage |
|-----------|-------|
| **VWAP** | Mean reversion, fair value |
| **EMA (9, 21, 50)** | Trend direction, crossovers |
| **RSI (14)** | Overbought/oversold |
| **ATR (14)** | Volatility, stop-loss sizing |
| **Volume** | Breakout confirmation |
| **Supertrend** | Trend following |

---

## Coming Soon

- [ ] Strategy implementations
- [ ] Kite Connect integration
- [ ] Stock scanner
- [ ] Backtesting engine
- [ ] Telegram alerts
- [ ] Dashboard

---

## Risk Warning

**Equity trading involves risk of capital loss.** Intraday trading is speculative. Past performance does not guarantee future results. Only trade with capital you can afford to lose.

---

## License

MIT License

---

## Contact

**Pranay** - Algo Trader

[![GitHub](https://img.shields.io/badge/GitHub-pranay123--stack-181717?style=flat&logo=github)](https://github.com/pranay123-stack)
