# PATTERN_ANALYSIS_GUIDE

## Purpose
This file explains how the 96 pattern image set should be interpreted and used for matching.

## Required Input
A ZIP file containing the pattern screenshots, each named with the pattern number, market, and action, for example:
- `01_EURUSD_BUY.png`
- `02_EURUSD_SELL.png`
- `03_GBPUSD_BUY.png`
- ...
- `96_USDJPY_SELL.png`

## What to analyze in each image
For every pattern image, determine:
- first candle color
- second candle color
- body size
- wick size
- overall market pattern
- market name
- action (BUY or SELL)

## Example
```text
01_EURUSD_BUY.png
- Candle 1: GREEN
- Candle 2: RED
- Pattern shape: bullish-bearish reversal or green-red combination
- Market: EURUSD
- Action: BUY
```

## Matching Principle
Current live screenshot should be reduced to a pattern signature using the same logic:
- candle 1 color
- candle 2 color
- candle body size
- wick length
- market label

Then compare against the 96 stored patterns.

## Matching Threshold
- Use a similarity threshold of around 90% or higher
- No trade should be allowed below this threshold

## Timing Logic to Match with App Execution
- Only trade in the last 5 seconds of a 15-second candle
- Pattern match must happen during that window
- App then executes BUY or SELL automatically

## Important Rule
The pattern set is the core of the system. The app must compare the live chart to these exact screenshots as the decision basis. This is the main logic of the trading automation.
