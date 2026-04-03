# live-vol-surface

Small Python app that connects to Interactive Brokers, requests live option data, and renders a live implied volatility surface with Matplotlib.

## Prerequisites

- Python 3.11
- [uv](https://docs.astral.sh/uv/)
- An IBKR account
- Interactive Brokers TWS or IB Gateway installed locally

## Project Setup

### 1. Install Python dependencies

Create the local virtual environment and install the Python packages:

```bash
uv sync
```

### 2. Set up Interactive Brokers access

This project depends on Interactive Brokers market data. As part of setup, you need to:

1. Create or use an existing IBKR account
2. Install either TWS or IB Gateway
3. Log in to TWS or IB Gateway on your machine
4. Open the API settings in TWS / Gateway
5. Enable socket client access so this script can connect locally
6. Confirm the socket port matches the value used in the script

The script currently connects to `127.0.0.1:7497`, which is commonly the TWS paper trading port.

### 3. Start TWS or IB Gateway

Before running the script, make sure TWS or IB Gateway is open and logged in.

## Run

Run the app with:

```bash
uv run python live_surface.py
```

## What It Does

- Connects to the Interactive Brokers API
- Resolves the underlying contract for a stock symbol
- Pulls option chain metadata
- Subscribes to near-the-money option market data
- Builds a live IV surface from the returned implied vol values
- Shows a 3D surface plot plus a front-month skew chart

## Notes

- The script uses Matplotlib interactive mode for a desktop plot window.
- It expects the IB API port to be available on `7497` unless you change the code.
- The current implementation targets US stock options and defaults to `SPY`.
- If you need a fresh environment later, rerun `uv sync`.
