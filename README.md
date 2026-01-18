# Dynamic DCA SPX/GOLD Indicator

## Overview
This Pine Script indicator provides a long-term Dollar Cost Averaging (DCA) strategy based on the relative valuation of the S&P 500 (SPX) against Gold.

It operates independently of the chart currently being viewed. It forces a request for the ratio `SP:SPX/TVC:GOLD` on the Weekly timeframe to determine the current macro regime.

## Logic and Methodology
The script calculates the ratio of SPX to Gold and compares it against a 200-week Simple Moving Average (SMA). To filter out noise and confirm a long-term trend change, the script utilizes a confirmation threshold:

1.  **Ratio Calculation:** `S&P 500 Close / Gold Close`
2.  **Trend Baseline:** 200-week SMA of the ratio.
3.  **Regime Detection:**
    * **Regime 1 (Ratio High):** The ratio must close above the 200 SMA for **30 consecutive weeks**. This indicates the S&P 500 is historically expensive relative to Gold.
    * **Regime -1 (Ratio Low):** The ratio must close below the 200 SMA for **30 consecutive weeks**. This indicates the S&P 500 is historically cheap relative to Gold.

## Visuals and Signals

The indicator displays data using background coloring and a dashboard table in the bottom-right corner.

### 1. Dashboard Recommendations
* **Recommended DCA: GOLD**
    * Triggered when the ratio is in **Regime 1** (extended above the 200 SMA).
    * Interpretation: Equities are overvalued relative to commodities; capital is rotated into Gold.
* **Recommended DCA: S&P 500**
    * Triggered when the ratio is in **Regime -1** (extended below the 200 SMA).
    * Interpretation: Equities are undervalued relative to commodities; capital is rotated into the S&P 500.

### 2. Background Color Coding
* **Yellow Background:** Corresponds to Regime 1 (DCA Gold).
* **Blue Background:** Corresponds to Regime -1 (DCA S&P 500).

## Technical Implementation Details
* **`request.security`:** Hardcoded to `SP:SPX/TVC:GOLD` with a resolution of `"W"`. This allows you to add the script to any chart (e.g., BTCUSD or AAPL) and still see the macro SPX/GOLD status.
* **State Persistence:** Uses `var` variables to persist the counter for `weeksAbove` and `weeksBelow` across calculation bars.

## Installation
1.  Open the Pine Editor in TradingView.
2.  Paste the script code.
3.  Click "Add to Chart".
4.  The indicator will appear as an overlay (background colors) and a table widget.