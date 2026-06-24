# Data snapshot — `xsmom_universes_prices.csv`

**Read-only reproducibility record. Do not edit by hand.**

`xsmom_universes_prices.csv` is the price panel the **Phase-2 multi-universe XSMOM study**
([`../XSMOM_UNIVERSES_README.md`](../XSMOM_UNIVERSES_README.md)) was run on. It is committed
so every number in that study is **exactly reproducible from a clone**, without re-fetching.

- **Fetched:** 2026-06-22 (via `src/xsmom_data.py`, yfinance `auto_adjust=True`).
- **Coverage:** 47 candidate ETFs across the 5 sealed universes (US sectors / country indices /
  G10 FX / commodities / bonds), daily adjusted closes, **1996-03-18 → 2026-06-18**.
- **Used by:** `src/xsmom_data.py` (loads this file in place; only re-fetches if it is absent).

## Why this is committed (and why it's the canonical record)

The loader *can* re-fetch from yfinance, but **yfinance/Yahoo may silently revise
adjusted-close history** (dividend/split re-adjustments, vendor backfills), so a re-fetch on a
later date can differ slightly from this panel — which would move the study's numbers. The
committed snapshot is therefore the **canonical, frozen input**; treat a re-fetch as a separate,
potentially-revised dataset, not as a reproduction of these results.

## Scope (what is and isn't snapshotted)

- ✅ **Committed:** this file only (the Phase-2 universe panel).
- ❌ **Not committed:** the engine's 17-ETF cache `close_prices_raw.csv` (TSMOM / Phase-1) and
  `fetch_metadata.csv` remain git-ignored (Yahoo licensing / size). TSMOM and Phase-1 results
  re-fetch their data on first run, per the main README's "How to run".
