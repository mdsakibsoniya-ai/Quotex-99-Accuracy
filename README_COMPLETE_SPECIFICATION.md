# README_COMPLETE_SPECIFICATION

## Project Name
Md Jibon Quotex 99%

## Package Name
`com.mdjibon.quotex99`

## Status
Ready for development

## Project Overview
Build an Android app that scans Quotex charts, compares them against a pattern database, and automatically executes BUY or SELL trades using Accessibility Service. The app should only trade during the last 5 seconds of a 15-second candle.

## Core Requirements
- Floating icon overlay over the screen
- Start/stop scanning by tapping the floating icon
- Screen capture of current chart
- Pattern detection from the latest candlesticks
- Comparison with a database of 96 screenshot patterns
- Exact or near-exact match required to trade
- Trade execution only in the final 5 seconds of a 15-second candle
- Automatic trade by clicking Quotex UI elements via Accessibility Service
- Logging of trades and settings

## Mandatory Timing Rule
- Candle duration: 15 seconds
- Trade execution window: only the final 5 seconds of the candle
- A tap outside that window must not trigger a trade
- User must tap the floating icon in the last 5 seconds of the candle
- If the user taps outside the valid window: show a warning and skip trading

## Core Logic Flow
1. User opens Quotex
2. Floating icon appears
3. User taps icon during the final 5 seconds of the candle
4. App captures the current chart screenshot
5. App detects candlestick pattern
6. App extracts market information
7. App compares screenshot with saved pattern images
8. If exact match is found → determine BUY or SELL
9. App waits until the correct moment and triggers the trade
10. Accessibility Service clicks the correct button and confirms the trade
11. Trade is logged in local database
12. User taps again to stop scanning

## Must-Use Technology
- Android Kotlin
- MediaProjection for screen capture
- OpenCV for image comparison and pattern detection
- Accessibility Service for auto-clicking trade buttons
- Room/SQLite for logging and settings
- Gradle for Android build

## App Features
- Floating icon with active/inactive status
- Multi-market scanning support
- 96 screenshot pattern database
- BUY/SELL decision logic
- 5-second pre-close trade execution
- Trade history screen
- Settings screen
- No-trade when no pattern match is found

## Market Coverage
The app should scan multiple markets automatically, including:
- EURUSD
- GBPUSD
- AUDUSD
- GBPJPY
- USDJPY
- Gold
- Oil
- Bitcoin
- Ethereum
- SP500
- DAX
- FTSE100
- Nikkei
- OTC markets

## Pattern Requirements
- The app receives a ZIP file with 96 pattern screenshots
- Each image should represent an exact candlestick pattern
- Each pattern should map to a specific market and action (BUY or SELL)
- Pattern files should be named like:
  - `01_EURUSD_BUY.png`
  - `02_EURUSD_SELL.png`
  - `03_GBPUSD_BUY.png`
  - ...
  - `96_USDJPY_SELL.png`

## Pattern Matching Rules
- Compare current chart with all 96 reference images
- Match by candle colors, size, wick length, shape, and market
- Use similarity threshold of around 90% or higher
- If similarity is too low: no trade
- Only exact or near-exact pattern match should trigger trade

## Trade Execution Requirements
- The app must use Accessibility Service
- It must find the BUY or SELL button automatically
- It must find the amount input field
- It must fill amount based on settings
- It must click confirm
- It must log the trade result

## User Flow
1. User opens Quotex
2. Floating icon appears
3. User taps the icon during the last 5 seconds of a candle
4. App captures screen
5. App matches pattern
6. If match found: trade executes automatically
7. User taps again to stop

## UX / UI Requirements
### Main Screen
- Start Scanning button
- Stop Scanning button
- Status display
- Last trade result
- Trade history button
- Settings button

### Floating Icon
- visible above other apps
- draggable
- active/inactive state
- color-coded status

### Settings Screen
- trade amount
- scan interval
- market selection
- notification toggles
- clear history option

## Local Storage
Store locally:
- trade history
- settings
- last scan info
- logs

Use Room or SQLite.

## Build Requirements
- Android Studio
- JDK 11+
- Android SDK 34
- Kotlin
- Gradle 8+

## Build Command
```bash
./gradlew assembleRelease
```

## Output APK
```bash
app/build/outputs/apk/release/app-release.apk
```

## CodeMagic
This project should also be compatible with CodeMagic build pipeline by running:
```bash
./gradlew assembleRelease
```

## Acceptance Criteria
The implementation is successful only if all are true:
- floating icon works
- app starts/stops scanning correctly
- chart is captured
- pattern matching works
- exact match triggers trade
- no trade if no match
- auto trade uses Accessibility Service
- trades execute only in the final 5 seconds of a 15-second candle
- trade history is stored
- build completes successfully
- APK is generated

## Final Notes
This project is an Android automation system for Quotex based on exact screenshot pattern recognition and auto-trading. The developer should implement it directly from this specification and should not ask follow-up questions.

---

## Summary
The app must be built exactly according to the following logic:
- floating icon starts the process
- user taps icon during the last 5 seconds of a 15-second candle
- app captures chart
- app matches against 96 pattern screenshots
- exact match triggers BUY/SELL
- trading is automated through Accessibility Service
- only valid trading window is allowed
