# Md Jibon Quotex 99% - Complete Developer Handoff Specification

Project Name: Md Jibon Quotex 99%
Package Name: com.mdjibon.quotex99
Platform: Android
Language: Kotlin
Build: Gradle
Target: Android app using floating icon, screen overlay, automated pattern matching, and accessibility-based trading automation

IMPORTANT:
- Read this file completely
- Do not ask questions
- Do not change the logic
- Do not change the 15-second timing rule
- Do not change the 5-second trade window
- Start implementation immediately

---

## 1. Project Objective
Build an Android application named "Md Jibon Quotex 99%" that:
- shows a floating icon on top of other apps
- user taps the floating icon to start or stop the scanning process
- app captures the current Quotex chart screen
- app detects the market and the last candlesticks
- app compares the live chart with a database of 96 saved screenshots
- if the live pattern matches a stored pattern, the app decides BUY or SELL
- app executes the trade automatically using Accessibility Service
- trade is allowed only during the last 5 seconds of a 15-second candle
- a blue visual overlay appears while the app is scanning
- app logs trade history locally

---

## 2. Core Trading Rule (Mandatory)

### Candle Timing
- Candle length: 15 seconds
- Valid trading window: ONLY the final 5 seconds of the candle
- Meaning: trade is only allowed when the current candle is between 10 seconds and 15 seconds
- If user taps the icon outside this window, the scan must be skipped and no trade must happen

### Example
```
0s ------------------------------- 15s
|                                 |
|---- last 5 seconds = 10s-15s ---|
```

### Required logic
```kotlin
if (secondsRemainingInCandle <= 5000 && secondsRemainingInCandle > 0) {
    // valid window
    startScanAndTrade()
} else {
    // invalid window
    skipTrade()
}
```

---

## 3. App Behavior Flow

### Normal flow
1. User opens Quotex app
2. Floating icon appears on screen
3. User taps the floating icon during the last 5 seconds of the current candle
4. App shows a blue overlay or blue scan visual effect on screen
5. App captures the visible chart area
6. App detects current market and candlestick pattern
7. App compares the live pattern with saved 96 pattern images
8. If a valid match is found, app decides BUY or SELL
9. App triggers the trade automatically through Accessibility Service
10. Trade is logged to local database
11. User taps the floating icon again to stop scanning

### Stop flow
- User taps floating icon again
- App disables scanning
- Blue scan overlay disappears
- No more auto trade occurs until started again

---

## 4. Floating Icon Requirements

### Visual requirements
- floating icon always visible above other apps
- icon should be small and non-intrusive
- recommended position: upper-right corner
- draggable by user
- active/inactive visual state

### States
- inactive: gray icon or disabled style
- active: green icon or enabled style
- scanning: blue overlay active + icon highlighted
- trade executed: success state or glow effect

### Action
- single tap: start/stop scanning
- drag: reposition icon

---

## 5. Blue Overlay Scan Effect

### Visual requirement
When scanning is active, the app should display a blue transparent overlay over the screen or chart area to show the system is scanning.

### Overlay behavior
- blue transparent layer / blue glow effect
- visible while scanning is active
- disappears when scanning stops
- overlay should not completely block the user from seeing the chart
- overlay should be subtle but clearly visible

### Example behavior
- scanning active: blue shimmer or blue translucent overlay
- pattern found: overlay changes to blue+green glow
- no match: overlay remains blue and minimal

---

## 6. Screen Capture Requirements

### Requirements
- capture the Quotex chart area
- use MediaProjection API
- screenshot should include the market chart and last candlesticks
- current timeframe must be interpreted as a 15-second candlestick chart

### Process
1. capture current screen
2. detect chart region
3. crop relevant candlestick area
4. identify last 2 candles
5. detect shape, color, wick lengths, and trend

---

## 7. Pattern Matching Engine

### Requirement
The app must compare the current chart with a set of 96 pattern screenshots.

### Pattern database folder
`app/src/main/assets/patterns/`

### Naming format
- `01_EURUSD_BUY.png`
- `02_EURUSD_SELL.png`
- `03_GBPUSD_BUY.png`
- `04_GBPUSD_SELL.png`
- ...
- `96_USDJPY_SELL.png`

### Pattern list file
`pattern_list.txt` should include mapping like:
```txt
01, EURUSD, BUY
02, EURUSD, SELL
03, GBPUSD, BUY
04, GBPUSD, SELL
...
96, USDJPY, SELL
```

### Matching condition
- compare current screenshot against all 96 reference pattern images
- compute similarity score
- require around 90% match or more
- market must match the predicted market name
- only execute if both conditions pass

### Matching logic summary
```kotlin
val similarity = calculateSimilarity(currentPattern, referencePattern)
if (similarity >= 90f && currentMarket == referencePattern.market) {
    trade(referencePattern.action)
} else {
    skipTrade()
}
```

---

## 8. Candlestick Pattern Analysis

The app must analyze:
- candle color (green/red)
- candle body size
- upper wick size
- lower wick size
- last 2 candle shapes
- trend shape and price structure

### Example pattern signature
```kotlin
data class PatternSignature(
    val candle1Color: String,
    val candle1BodySize: String,
    val candle1UpperWick: String,
    val candle1LowerWick: String,
    val candle2Color: String,
    val candle2BodySize: String,
    val candle2UpperWick: String,
    val candle2LowerWick: String
)
```

The live chart should be converted into the same structure and compared against the reference patterns.

---

## 9. Market Detection

The app must detect which market is currently active.

### Supported markets
- EURUSD
- GBPUSD
- AUDUSD
- GBPJPY
- USDJPY
- USDCAD
- NZDUSD
- Gold
- Oil
- Bitcoin
- Ethereum
- SP500
- DAX
- FTSE100
- Nikkei
- OTC markets

### Market check requirement
The action must match the detected market before the trade is executed.

---

## 10. Accessibility Service Trade Execution

### Must use
Android Accessibility Service

### Required flow
1. detect BUY or SELL action
2. locate BUY or SELL button
3. tap BUY or SELL
4. find amount field
5. fill the configured amount
6. confirm the trade
7. log result to database

### Important rule
Do not hardcode screen coordinates unless absolutely required. Use Accessibility Node information when possible.

---

## 11. Auto-Trade Rules

### Allowed trade logic
Trade can happen only when:
- scan is active
- the user tapped the floating icon during the valid final 5 seconds of the candle
- pattern match score is high enough
- market is recognized
- trade action is BUY or SELL

### Disallowed cases
- trade outside the final 5-second window
- no pattern match
- unknown market
- duplicate invalid trade loop

---

## 12. Main UI Structure

### Activity 1: Main Activity
Contains:
- title
- start scanning button
- stop scanning button
- status text
- last trade result
- trade count
- trade history button
- settings button

### Activity 2: Settings Activity
Contains:
- trade amount
- scan interval
- sound setting
- notification toggle
- market preference
- clear log

### Activity 3: Trade History Activity
Displays:
- timestamp
- market
- action
- amount
- result
- status

### Floating overlay
- visible above other apps
- draggable
- active/inactive toggle
- colored indicator
- blue scan effect when using auto scan

---

## 13. UI and Visual Design Description

### Main UI look
- modern, clean Android screen
- simple top header with app name
- green and blue color scheme
- status card with scanning state
- action buttons centered
- trade history card below

### Floating icon style
- small round icon with chart symbol
- green when active
- gray when inactive
- blue glow when scanning

### Blue overlay style
- translucent blue blur or blue tint over the screen area
- minimal but visible
- no full black overlay
- should not obscure the whole UI too much

---

## 14. Local Storage

Use Room or SQLite.

### Store:
- trade history
- trade timestamp
- market
- action
- amount
- status
- result

### Example schema
```kotlin
@Entity
data class Trade(
    @PrimaryKey(autoGenerate = true) val id: Int = 0,
    val timestamp: Long,
    val market: String,
    val action: String,
    val amount: Int,
    val status: String,
    val result: String?
)
```

---

## 15. Permissions

Required:
- INTERNET
- SYSTEM_ALERT_WINDOW
- FOREGROUND_SERVICE
- ACCESSIBILITY_SERVICE

Also handle runtime permission flow for screen capture and overlay.

---

## 16. Project Structure

```text
app/
├── src/main/java/com/mdjibon/quotex99/
│   ├── MainActivity.kt
│   ├── SettingsActivity.kt
│   ├── TradeHistoryActivity.kt
│   ├── service/
│   │   ├── FloatingIconService.kt
│   │   ├── ScreenCaptureService.kt
│   │   ├── ScannerService.kt
│   │   └── AccessibilityTradeService.kt
│   ├── engine/
│   │   ├── PatternDetector.kt
│   │   ├── PatternMatcher.kt
│   │   ├── MarketDetector.kt
│   │   └── ScanningEngine.kt
│   ├── database/
│   │   ├── TradeDatabase.kt
│   │   ├── Trade.kt
│   │   └── TradeDao.kt
│   └── utils/
│       ├── Constants.kt
│       ├── Logger.kt
│       └── TimeUtils.kt
├── src/main/assets/patterns/
│   ├── pattern_list.txt
│   ├── 01_EURUSD_BUY.png
│   ├── 02_EURUSD_SELL.png
│   └── ...
├── src/main/res/layout/
│   ├── activity_main.xml
│   ├── activity_settings.xml
│   └── activity_history.xml
├── src/main/AndroidManifest.xml
├── build.gradle.kts
├── settings.gradle.kts
└── gradlew
```

---

## 17. Build Instructions

### Local build
```bash
./gradlew assembleRelease
```

### Output APK
```bash
app/build/outputs/apk/release/app-release.apk
```

### CodeMagic
Use this command:
```bash
./gradlew assembleRelease
```

---

## 18. Acceptance Criteria
The app is considered complete only if all the following are true:
- floating icon appears correctly
- start/stop scanning works
- blue scanning overlay appears while active
- screen capture works
- candlestick analysis works
- market detection works
- pattern matching works with the 96 images
- BUY or SELL action is selected correctly
- trade only occurs in the final 5 seconds of the 15-second candle
- app uses Accessibility Service to trade
- app logs trade results
- app is buildable and APK is generated

---

## 19. Final Developer Instruction
Build exactly according to these rules:
- Use 15-second candle logic
- Only trade in the final 5 seconds
- Use floating icon as trigger
- Use blue overlay while scanning
- Use screen capture and pattern matching
- Use 96 pattern screenshots as database
- Use Accessibility Service for auto trade
- Skip trade if no pattern match
- Do not ask additional questions
- Start implementation immediately

---

## 20. Summary in One Sentence
Build an Android app that displays a floating icon, shows a blue scan overlay while active, analyzes the live Quotex chart against 96 pattern images, and auto-executes BUY or SELL only during the final 5 seconds of a 15-second candle using Accessibility Service.
