---
title: "Momentum Factor Research"
date: 2026-03-08
categories: [factor]
tags: [quant, momentum]
toc: true
---

## Overview

Momentum is one of the most well-known factors in quantitative finance.  
It is based on the idea that assets which performed well in the past tend to continue performing well in the near future.

This note explores a simple momentum strategy and outlines a basic backtest framework.

---

## Momentum Definition

A common definition of momentum is:

$$
Momentum_i = \frac{P_{t} - P_{t-k}}{P_{t-k}}
$$

where

- $P_t$ : current price
- $P_{t-k}$ : price k periods ago

Typical lookback windows:

- 3 months
- 6 months
- 12 months

---

## Simple Strategy

Basic momentum strategy:

1. Calculate past 12-month return
2. Rank assets
3. Long top decile
4. Rebalance monthly

---

## Example Python Code

```python
import pandas as pd

def momentum_signal(prices, lookback=252):
    returns = prices.pct_change(lookback)
    ranks = returns.rank(axis=1, pct=True)
    return ranks
