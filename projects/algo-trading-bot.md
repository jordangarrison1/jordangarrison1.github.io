---
layout: project
type: project
image: img/algo-trading-bot/algo-trading-bot-square.png
title: "Algo-Trading Bot"
date: 2026
era: professional
published: true
labels:
  - Python
  - Alpaca API
  - Algorithmic Trading
  - AI-Assisted
summary: "Vibe coding an algorithmic trading bot with an AI assistant — an experiment in AI-directed development and quantitative trading, built and tested on a paper-trading account."
---

## Vibe Coding an Algo-Trading Bot

This project is an ongoing experiment at the intersection of two things I want to get
sharper at: **AI-assisted software development** and **quantitative trading**.

The premise is simple — rather than hand-writing every line, I build and iterate on the
bot by *directing an AI coding assistant* in plain language: describing the behavior I
want, reviewing the code it produces, correcting course, and learning the underlying
concepts as I go. "Vibe coding," but with guardrails: I read every diff, keep secrets out
of the repo, and validate against a sandbox before anything touches real markets.

### Why paper trading first

The bot runs against [Alpaca](https://alpaca.markets)'s **paper-trading** API — a full
simulated brokerage with a fake balance and live market data, but zero real money at
risk. It's the right way to learn: I can let strategies run, break things, and measure
results without a dollar on the line. API keys authenticate the bot instead of a
password, and credentials live in a git-ignored `.env` file — never in the repository.

### The stack

- **Python** with the official `alpaca-py` SDK
- **Alpaca paper-trading API** for market data, account state, and order execution
- **A secure local setup** — virtual environment, git-ignored secrets, read-only
  connection checks before any order logic
- **An AI coding assistant** as the pair-programmer driving implementation

### A first milestone — connecting to the account

The first checkpoint was a read-only connection: authenticate, pull the (simulated)
account, and confirm buying power before writing a single line of order logic.

```python
from alpaca.trading.client import TradingClient

# Paper-trading account — no real funds at risk
client = TradingClient(API_KEY, SECRET_KEY, paper=True)

account = client.get_account()
print(f"Status:        {account.status}")
print(f"Buying power:  ${account.buying_power}")
```

### What I'm learning

- How far AI-directed development can go on a real, non-trivial project — and where a
  human still has to own the judgment calls
- The mechanics of a modern brokerage API: order types, positions, market data
- Building the safety habits that matter *before* automating anything financial:
  sandboxing, secret management, and reviewing every change

This page will grow as the experiment does — from a read-only connection, to simple
strategies, to backtesting and measured results.
