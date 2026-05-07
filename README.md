# StockSense : Indian-Stock-Price-Forecaster

**Indian Stocks Price Forecaster** is a terminal-based, object-oriented Python utility that fetches market data for Indian exchange tickers (NSE / BSE) and prints a compact, easy-to-read “stock snapshot” report in the terminal. The tool uses Yahoo Finance as a data source (via `yfinance`) and renders the output using the `rich` library for clear, colored, tabular terminal output.

---

## Table of contents

- [Project overview](#project-overview)  
- [Features](#features)  
- [Key design goals](#key-design-goals)  
- [Quick start (install & run)](#quick-start-install--run)  
- [Usage examples](#usage-examples)  
- [Snapshot fields explained (plain language)](#snapshot-fields-explained-plain-language)  
- [Computation details & numerical correctness](#computation-details--numerical-correctness)  
- [Dependencies](#dependencies)  
- [Limitations, caveats and data disclaimers](#limitations-caveats-and-data-disclaimers)  
- [Troubleshooting & common questions](#troubleshooting--common-questions)  
- [Development, testing and contribution guidelines](#development-testing-and-contribution-guidelines)  
- [License & contact](#license--contact)

---

## Project overview

This project provides a small, portable command-line application that:

- Downloads historical prices and company metadata for a given stock symbol (NSE or BSE).
- Builds a concise snapshot containing price, volume, market-cap and common fundamental metrics.
- Computes recent returns (1 day, 1 month, 1 year, etc.) and annualised returns (CAGR).
- Prints a clear, human-readable report to the terminal using the `rich` library.

The tool is intended for reporting and research; it is not a trading platform.

---

## Features

- Fetches company metadata and historical OHLCV (Open, High, Low, Close, Volume) price data.
- Produces a terminal snapshot showing:
  - LTP (last traded/quoted price) with rupee and percent delta
  - Open, Previous Close
  - Day High / Low and a horizontal range bar with a marker
  - 52-week High / Low and its range bar
  - Trading volume and traded value
  - Shares outstanding, float, and market-cap estimates
  - Key fundamentals (EPS, Dividend Yield, P/E, P/B)
  - Recent returns (1D, 5D) and calendar returns (1M, 3M, 1Y, etc.)
  - Annualised returns (CAGR) for multi-year spans
- Uses `rich` for readable colored terminal output.

---

## Key design goals

1. **Accuracy** — Use adjusted close values where appropriate and a clear “on or before” logic for calendar-period returns to avoid holiday/weekend mismatches.  
2. **Readability** — Terminal output formatted for management review and quick interpretation (labels, aligned values, colored deltas, and compact range bars).  
3. **Robustness** — Fallbacks for missing metadata: prefer metadata but compute from history where necessary.  
4. **Explainability** — When a computation cannot be produced (e.g., insufficient history), the report includes a short, explicit reason.  
5. **Portable** — Single-file, CLI friendly; easy to run on common Python environments.

---
