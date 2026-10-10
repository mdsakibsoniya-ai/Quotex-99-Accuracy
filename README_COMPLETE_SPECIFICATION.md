# Md Jibon Quotex 99% - COMPLETE COMPREHENSIVE SPECIFICATION

**Project Name:** Md Jibon Quotex 99%
**App Name:** Md Jibon Quotex 99%
**Package Name:** com.mdjibon.quotex99
**Repository Name:** Quotex-99-Accuracy
**Version:** 1.0.0
**Language:** Kotlin
**Platform:** Android
**Min SDK:** 26
**Target SDK:** 34
**Compile SDK:** 34
**Build System:** Gradle 8.0+
**JDK:** 11+

---

## ⚠️ CRITICAL INSTRUCTION
- Read this entire document completely
- Do NOT ask any questions
- Do NOT change timing values
- Do NOT change trading logic
- Do NOT modify feature requirements
- Start implementation immediately after reading
- This is the ONLY specification needed

---

## SECTION 1: PROJECT OVERVIEW

### Goal
Build an Android trading automation app for Quotex that:
1. Shows floating icon on screen
2. User taps icon to start scanning during the last 5 seconds of a 15-second candle
3. App displays blue overlay scan effect
4. App captures chart screenshot
5. App analyzes candlestick pattern
6. App compares with 96 saved pattern images
7. If exact match found → auto-execute BUY or SELL
8. Trade happens automatically via Accessibility Service
9. User can tap icon again to stop
10. All trades logged locally

### Core Success Metric
The app trades with ~99% accuracy by matching exact candlestick patterns.

---

## SECTION 2: APP NAME AND REPOSITORY DETAILS

### Official App Name
**Md Jibon Quotex 99%**

### Package Name (for Android)
`com.mdjibon.quotex99`

### GitHub Repository Name
`Quotex-99-Accuracy`

### Repository Structure
```
Quotex-99-Accuracy/
├── README.md
├── README_COMPLETE_SPECIFICATION.md
├── BUILD_INSTRUCTIONS.md
├── PATTERN_ANALYSIS_GUIDE.md
├── FEATURE_CHECKLIST.md
├── UI_MOCKUP.md
├── app/
│   ├── src/main/
│   │   ├── java/com/mdjibon/quotex99/
│   │   │   ├── MainActivity.kt
│   │   │   ├── SettingsActivity.kt
│   │   │   ├── TradeHistoryActivity.kt
│   │   │   ├── service/
│   │   │   │   ├── FloatingIconService.kt
│   │   │   │   ├── ScreenCaptureService.kt
│   │   │   │   ├── ScanningService.kt
│   │   │   │   ├── TradeExecutorService.kt
│   │   │   │   └── NotificationService.kt
│   │   │   ├── engine/
│   │   │   │   ├── PatternDetector.kt
│   │   │   │   ├── PatternMatcher.kt
│   │   │   │   ├── MarketDetector.kt
│   │   │   │   ├── ScanningEngine.kt
│   │   │   │   ├── CandleAnalyzer.kt
│   │   │   │   └── TimingEngine.kt
│   │   │   ├── database/
│   │   │   │   ├── TradeDatabase.kt
│   │   │   │   ├── Trade.kt
│   │   │   │   ├── TradeDao.kt
│   │   │   │   └── Statistics.kt
│   │   │   ├── accessibility/
│   │   │   │   ├── QuotexAccessibilityService.kt
│   │   │   │   └── TradeClickHandler.kt
│   │   │   ├── ui/
│   │   │   │   ├── overlay/
│   │   │   │   │   ├── BlueOverlay.kt
│   │   │   │   │   └── FloatingIcon.kt
│   │   │   │   └── widgets/
│   │   │   │       ├── StatusIndicator.kt
│   │   │   │       └── TradeHistoryAdapter.kt
│   │   │   └── utils/
│   │   │       ├── Constants.kt
│   │   │       ├── Logger.kt
│   │   │       ├── TimeUtils.kt
│   │   │       ├── ImageUtils.kt
│   │   │       └── PermissionManager.kt
│   │   ├── assets/
│   │   │   ├── patterns/
│   │   │   │   ├── pattern_list.txt
│   │   │   │   ├── 01_EURUSD_BUY.png
│   │   │   │   ├── 02_EURUSD_SELL.png
│   │   │   │   ├── 03_GBPUSD_BUY.png
│   │   │   │   ├── 04_GBPUSD_SELL.png
│   │   │   │   ├── 05_AUDUSD_BUY.png
│   │   │   │   ├── 06_AUDUSD_SELL.png
│   │   │   │   ├── 07_GBPJPY_BUY.png
│   │   │   │   ├── 08_GBPJPY_SELL.png
│   │   │   │   ├── 09_USDJPY_BUY.png
│   │   │   │   ├── 10_USDJPY_SELL.png
│   │   │   │   ├── 11_USDCAD_BUY.png
│   │   │   │   ├── 12_USDCAD_SELL.png
│   │   │   │   ├── 13_NZDUSD_BUY.png
│   │   │   │   ├── 14_NZDUSD_SELL.png
│   │   │   │   ├── 15_EURJPY_BUY.png
│   │   │   │   ├── 16_EURJPY_SELL.png
│   │   │   │   ├── 17_Gold_BUY.png
│   │   │   │   ├── 18_Gold_SELL.png
│   │   │   │   ├── 19_Oil_BUY.png
│   │   │   │   ├── 20_Oil_SELL.png
│   │   │   │   ├── 21_Silver_BUY.png
│   │   │   │   ├── 22_Silver_SELL.png
│   │   │   │   ├── 23_NaturalGas_BUY.png
│   │   │   │   ├── 24_NaturalGas_SELL.png
│   │   │   │   ├── 25_Bitcoin_BUY.png
│   │   │   │   ├── 26_Bitcoin_SELL.png
│   │   │   │   ├── 27_Ethereum_BUY.png
│   │   │   │   ├── 28_Ethereum_SELL.png
│   │   │   │   ├── 29_Litecoin_BUY.png
│   │   │   │   ├── 30_Litecoin_SELL.png
│   │   │   │   ├── 31_Ripple_BUY.png
│   │   │   │   ├── 32_Ripple_SELL.png
│   │   │   │   ├── ... (33 to 96 for other markets)
│   │   │   │   └── 96_OTC_SELL.png
│   │   │   └── config/
│   │   │       └── markets.json
│   │   ├── res/
│   │   │   ├── layout/
│   │   │   │   ├── activity_main.xml
│   │   │   │   ├── activity_settings.xml
│   │   │   │   ├── activity_history.xml
│   │   │   │   ├── item_trade_history.xml
│   │   │   │   └── overlay_scan.xml
│   │   │   ├── values/
│   │   │   │   ├── strings.xml
│   │   │   │   ├── colors.xml
│   │   │   │   ├── dimens.xml
│   │   │   │   └── styles.xml
│   │   │   ├── drawable/
│   │   │   │   ├── ic_chart.xml
│   │   │   │   ├── ic_play.xml
│   │   │   │   ├── ic_stop.xml
│   │   │   │   ├── ic_settings.xml
│   │   │   │   └── ic_history.xml
│   │   │   └── mipmap/
│   │   │       ├── ic_launcher.xml
│   │   │       └── ic_launcher_round.xml
│   │   └── AndroidManifest.xml
│   ├── build.gradle.kts
│   └── proguard-rules.pro
├── build.gradle.kts
├── settings.gradle.kts
├── gradle.properties
├── gradlew
├── gradlew.bat
├── .gitignore
└── local.properties
```

---

## SECTION 3: MANDATORY TIMING RULE

### The 15-Second Candle System
- **Total candle duration:** 15 seconds (FIXED - DO NOT CHANGE)
- **Valid trading window:** Last 5 seconds of the candle
- **Trading moment:** Between 10-second mark and 15-second mark

### Timing Diagram
```
Candle Timeline:
0s ──── 5s ──── 10s ──── 15s
        |                |
        |         VALID TRADE WINDOW
        |    (10s to 15s = last 5 seconds)
        |
    User can observe/wait
    but NO TRADE allowed
```

### Implementation Logic
```kotlin
fun isValidTradingWindow(): Boolean {
    val currentCandle = getCurrentCandleTimer()
    val timeRemaining = currentCandle.timeRemaining
    
    // Trade only if 5 seconds or less remain
    return timeRemaining in 1..5000 // milliseconds
}

fun shouldExecuteTrade(): Boolean {
    return isValidTradingWindow() && patternMatches() && marketVerified()
}
```

### Important Rule
- If user taps the floating icon OUTSIDE the valid 5-second window (between 0-10 seconds):
  - Show warning: "Please tap during the final 5 seconds of the candle"
  - Do NOT perform scan
  - Do NOT execute trade
  - Wait for next candle

---

## SECTION 4: COMPLETE FEATURE LIST

### Feature 1: Floating Icon Service ✅
**What it does:**
- Always visible overlay icon
- Position: top-right corner (user-draggable)
- Size: 80x80 pixels
- Shows active/inactive status
- Single tap: start/stop scanning

**Visual States:**
- Inactive: Gray color, 50% opacity
- Active Scanning: Green color, 100% opacity
- Found Pattern: Yellow, blinking animation
- Trade Executed: Green with checkmark overlay

**Behavior:**
```kotlin
class FloatingIconService {
    fun showFloatingIcon()
    fun updateStatus(state: IconState)
    fun makeIconDraggable()
    fun onIconTapped()
    fun hideFloatingIcon()
}
```

---

### Feature 2: Blue Overlay Scan Effect ✅
**What it does:**
- Displays blue translucent overlay when scanning
- Shows visual feedback that app is analyzing

**Visual Specification:**
- Color: Blue (#1E88E5 or similar)
- Opacity: 30-40% transparency
- Coverage: Full screen or chart area
- Animation: Subtle pulsing or shimmer effect
- Duration: Shows while scanning active, disappears when stopped

**Implementation:**
```kotlin
class BlueOverlayManager {
    fun showScanOverlay()
    fun updateOverlayWithPattern(found: Boolean)
    fun hideScanOverlay()
    fun animatePulse()
}
```

---

### Feature 3: Multi-Market Simultaneous Scanning ✅
**What it does:**
- Scans ALL markets simultaneously
- No manual market switching
- Detects which market is active
- Compares with all 96 patterns at once

**Supported Markets:**
```
Forex Pairs:
├─ EURUSD
├─ GBPUSD
├─ AUDUSD
├─ GBPJPY
├─ USDJPY
├─ USDCAD
├─ NZDUSD
└─ EURJPY

Commodities:
├─ Gold
├─ Oil
├─ Silver
└─ Natural Gas

Cryptocurrencies:
├─ Bitcoin
├─ Ethereum
├─ Litecoin
└─ Ripple

Indices:
├─ SP500
├─ DAX
├─ FTSE100
└─ Nikkei

OTC Markets:
└─ All available OTC
```

**Implementation:**
```kotlin
fun scanAllMarkets() {
    val liveScreenshot = captureScreen()
    val detectedMarket = detectMarket(liveScreenshot)
    val allPatterns = loadAll96Patterns()
    
    for (pattern in allPatterns) {
        if (pattern.market == detectedMarket) {
            val similarity = comparePatterns(liveScreenshot, pattern)
            if (similarity >= 90f) {
                executeTrade(pattern.action)
                return
            }
        }
    }
}
```

---

### Feature 4: Screen Capture with MediaProjection ✅
**What it does:**
- Captures current Quotex chart
- Happens continuously every 1-2 seconds
- Returns Bitmap format
- Extracts chart region

**Specifications:**
- API: MediaProjection
- Format: Bitmap (RGB_8888)
- Frequency: Every 1 second when scanning active
- Timeout: 2 seconds max per capture
- Resolution: Device native resolution

**Implementation:**
```kotlin
class ScreenCaptureService {
    fun requestScreenCapture()
    fun captureFrame(): Bitmap?
    fun extractChartRegion(bitmap: Bitmap): Bitmap
    fun handleCaptureError(exception: Exception)
}
```

---

### Feature 5: Candlestick Pattern Detection ✅
**What it does:**
- Analyzes last 2 candlesticks from screenshot
- Detects color, body size, wick sizes
- Creates pattern signature
- Compares with saved patterns

**Pattern Analysis Metrics:**
```kotlin
data class CandleInfo(
    val index: Int,                    // 1 or 2
    val color: Color,                  // GREEN or RED
    val bodySize: Size,                // SMALL, MEDIUM, LARGE
    val bodyRatio: Float,              // body height / candle height
    val upperWick: Size,               // SMALL, MEDIUM, LARGE
    val lowerWick: Size,               // SMALL, MEDIUM, LARGE
    val wickRatio: Float,              // wick height / candle height
    val closePrice: Float,
    val openPrice: Float,
    val highPrice: Float,
    val lowPrice: Float
)

data class PatternSignature(
    val candle1: CandleInfo,
    val candle2: CandleInfo,
    val trend: String,                 // BULLISH, BEARISH, REVERSAL
    val patterns: List<String>         // e.g., ["engulfing", "morning_star"]
)
```

**Implementation:**
```kotlin
class CandleAnalyzer {
    fun detectCandleSticks(bitmap: Bitmap): List<CandleInfo>
    fun analyzeCandle(candle: Path): CandleInfo
    fun detectColor(candle: Path): Color
    fun measureSize(path: Path): Size
    fun createPatternSignature(candles: List<CandleInfo>): PatternSignature
}
```

---

### Feature 6: 96 Pattern Database & Matching ✅
**What it does:**
- Loads all 96 reference pattern images
- Compares current pattern with database
- Calculates similarity score
- Returns BUY or SELL if match found

**Pattern Files Location:**
`app/src/main/assets/patterns/`

**File Naming Convention:**
```
01_EURUSD_BUY.png
02_EURUSD_SELL.png
03_GBPUSD_BUY.png
04_GBPUSD_SELL.png
...
96_OTC_SELL.png

Format: {number}_{market}_{action}.png
```

**Pattern List File:**
`app/src/main/assets/patterns/pattern_list.txt`
```
01,EURUSD,BUY
02,EURUSD,SELL
03,GBPUSD,BUY
04,GBPUSD,SELL
05,AUDUSD,BUY
06,AUDUSD,SELL
...
96,OTC,SELL
```

**Matching Algorithm:**
```kotlin
class PatternMatcher {
    fun loadPatterns(): List<Pattern>
    fun matchPattern(currentSignature: PatternSignature, 
                    referencePattern: Pattern): Float {
        var score = 0f
        
        // Candle 1 comparison (50 points)
        if (currentSignature.candle1.color == referencePattern.candle1.color) 
            score += 20f
        if (currentSignature.candle1.bodySize == referencePattern.candle1.bodySize) 
            score += 15f
        if (currentSignature.candle1.upperWick == referencePattern.candle1.upperWick) 
            score += 10f
        if (currentSignature.candle1.lowerWick == referencePattern.candle1.lowerWick) 
            score += 5f
        
        // Candle 2 comparison (50 points)
        if (currentSignature.candle2.color == referencePattern.candle2.color) 
            score += 20f
        if (currentSignature.candle2.bodySize == referencePattern.candle2.bodySize) 
            score += 15f
        if (currentSignature.candle2.upperWick == referencePattern.candle2.upperWick) 
            score += 10f
        if (currentSignature.candle2.lowerWick == referencePattern.candle2.lowerWick) 
            score += 5f
        
        return score // 0-100
    }
    
    fun findBestMatch(currentSignature: PatternSignature): Pattern? {
        var bestMatch: Pattern? = null
        var bestScore = 0f
        
        for (pattern in allPatterns) {
            val score = matchPattern(currentSignature, pattern)
            if (score >= 90f && score > bestScore) {
                bestScore = score
                bestMatch = pattern
            }
        }
        
        return bestMatch
    }
}
```

**Matching Threshold:** 90% similarity or higher required

---

### Feature 7: Market Detection ✅
**What it does:**
- Detects which market is active
- Uses OCR or text recognition
- Validates market before trading
- Prevents wrong-market trades

**Implementation:**
```kotlin
class MarketDetector {
    fun detectMarket(bitmap: Bitmap): String {
        val marketName = extractTextFromScreen(bitmap)
        return validateMarket(marketName)
    }
    
    fun extractTextFromScreen(bitmap: Bitmap): String {
        // Use ML Kit for OCR or TensorFlow
        val recognizer = TextRecognition.getClient()
        val image = InputImage.fromBitmap(bitmap, 0)
        return recognizer.process(image).text
    }
    
    fun validateMarket(name: String): String {
        val validMarkets = listOf(
            "EURUSD", "GBPUSD", "AUDUSD", "GBPJPY", "USDJPY",
            "USDCAD", "NZDUSD", "EURJPY",
            "Gold", "Oil", "Silver", "Natural Gas",
            "Bitcoin", "Ethereum", "Litecoin", "Ripple",
            "SP500", "DAX", "FTSE100", "Nikkei",
            "OTC"
        )
        return if (name in validMarkets) name else "UNKNOWN"
    }
}
```

---

### Feature 8: Accessibility Service Trade Execution ✅
**What it does:**
- Automates clicking of BUY/SELL button
- Fills trade amount automatically
- Clicks CONFIRM button
- Records result

**Permission Required:**
User must manually enable in Android Settings → Accessibility

**Implementation:**
```kotlin
class QuotexAccessibilityService : AccessibilityService() {
    fun executeTrade(action: String) {
        // action = "BUY" or "SELL"
        findAndClickButton(action)
        delay(500)
        fillTradeAmount()
        delay(500)
        clickConfirmButton()
    }
    
    fun findAndClickButton(action: String) {
        val nodeInfo = findNodeByText(action)
        nodeInfo?.performAction(AccessibilityNodeInfo.ACTION_CLICK)
    }
    
    fun findNodeByText(text: String): AccessibilityNodeInfo? {
        val rootNode = rootInActiveWindow ?: return null
        return findNode(rootNode, text)
    }
    
    fun fillTradeAmount() {
        val amountField = findNodeByHint("Amount")
        amountField?.setText("10") // default amount
    }
    
    fun clickConfirmButton() {
        val confirmBtn = findNodeByText("CONFIRM") ?: findNodeByText("OK")
        confirmBtn?.performAction(AccessibilityNodeInfo.ACTION_CLICK)
    }
}
```

---

### Feature 9: Win Rate Calculation ✅
**What it does:**
- Tracks all trades
- Calculates success percentage
- Displays win rate in UI

**Implementation:**
```kotlin
class StatisticsCalculator {
    fun calculateWinRate(): Float {
        val trades = database.getAllTrades()
        val winTrades = trades.filter { it.result == "WIN" }
        return if (trades.isNotEmpty()) 
            (winTrades.size.toFloat() / trades.size) * 100 
        else 0f
    }
    
    fun calculateTotalProfit(): Float {
        val trades = database.getAllTrades()
        return trades.sumOf { 
            if (it.result == "WIN") it.amount.toFloat() else -(it.amount.toFloat())
        }
    }
    
    fun getLastNTrades(n: Int): List<Trade> {
        return database.getLastTrades(n)
    }
}
```

---

### Feature 10: Notification System ✅
**What it does:**
- Sound alert when trade executed
- Vibration alert
- Visual notification

**Implementation:**
```kotlin
class NotificationService {
    fun showTradeNotification(market: String, action: String) {
        val notification = NotificationCompat.Builder(context)
            .setContentTitle("Trade Executed")
            .setContentText("$action on $market")
            .setSmallIcon(R.drawable.ic_chart)
            .setSound(RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION))
            .setPriority(NotificationCompat.PRIORITY_HIGH)
            .build()
        
        NotificationManagerCompat.from(context).notify(1, notification)
    }
    
    fun vibratePhone() {
        val vibrator = context.getSystemService(Context.VIBRATOR_SERVICE) as Vibrator
        vibrator.vibrate(VibrationEffect.createOneShot(200, VibrationEffect.DEFAULT_AMPLITUDE))
    }
    
    fun playSound() {
        val notification = RingtoneManager.getRingtone(context, 
            RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION))
        notification.play()
    }
}
```

---

### Feature 11: Trade History with Database ✅
**What it does:**
- Logs every trade
- Stores trade details
- Shows last 50 trades
- Allows clear history

**Database Schema:**
```kotlin
@Entity
data class Trade(
    @PrimaryKey(autoGenerate = true) val id: Int = 0,
    val timestamp: Long,
    val market: String,
    val action: String,           // BUY or SELL
    val amount: Int,
    val status: String,           // EXECUTED, SKIPPED, FAILED
    val result: String?,          // WIN, LOSS, PENDING
    val screenShotPath: String?,  // path to screenshot if saved
    val patternId: Int?,          // which pattern matched
    val similarity: Float         // match similarity score
)

@Dao
interface TradeDao {
    @Insert
    suspend fun insertTrade(trade: Trade)
    
    @Query("SELECT * FROM Trade ORDER BY timestamp DESC LIMIT 50")
    suspend fun getLastTrades(): List<Trade>
    
    @Query("SELECT * FROM Trade WHERE market = :market ORDER BY timestamp DESC")
    suspend fun getTradesByMarket(market: String): List<Trade>
    
    @Query("DELETE FROM Trade")
    suspend fun clearAllTrades()
    
    @Query("SELECT COUNT(*) FROM Trade WHERE result = 'WIN'")
    suspend fun getWinCount(): Int
    
    @Query("SELECT COUNT(*) FROM Trade")
    suspend fun getTotalCount(): Int
}

@Database(entities = [Trade::class], version = 1)
abstract class TradeDatabase : RoomDatabase() {
    abstract fun tradeDao(): TradeDao
}
```

---

### Feature 12: Settings Screen ✅
**What it does:**
- Configure trade amount (1-1000)
- Configure scan interval (0.5-5 seconds)
- Enable/disable notifications
- Enable/disable vibration
- Select markets to scan
- Clear trade history

**Settings Storage:**
```kotlin
class SettingsManager(context: Context) {
    private val prefs = context.getSharedPreferences("quotex_prefs", Context.MODE_PRIVATE)
    
    fun setTradeAmount(amount: Int) = prefs.edit().putInt("trade_amount", amount).apply()
    fun getTradeAmount(): Int = prefs.getInt("trade_amount", 10)
    
    fun setScanInterval(interval: Float) = prefs.edit().putFloat("scan_interval", interval).apply()
    fun getScanInterval(): Float = prefs.getFloat("scan_interval", 1f)
    
    fun setNotificationEnabled(enabled: Boolean) = prefs.edit().putBoolean("notification", enabled).apply()
    fun isNotificationEnabled(): Boolean = prefs.getBoolean("notification", true)
    
    fun setVibrationEnabled(enabled: Boolean) = prefs.edit().putBoolean("vibration", enabled).apply()
    fun isVibrationEnabled(): Boolean = prefs.getBoolean("vibration", true)
    
    fun setAutoTradeEnabled(enabled: Boolean) = prefs.edit().putBoolean("auto_trade", enabled).apply()
    fun isAutoTradeEnabled(): Boolean = prefs.getBoolean("auto_trade", true)
}
```

---

### Feature 13: Complete UI Structure ✅

#### Main Activity Layout
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp"
    android:background="@color/background">
    
    <!-- Header -->
    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Md Jibon Quotex 99%"
        android:textSize="24sp"
        android:textStyle="bold"
        android:textColor="@color/primary"
        android:gravity="center" />
    
    <!-- Status Card -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        android:background="@drawable/card_background"
        android:padding="16dp"
        android:layout_marginTop="16dp"
        android:layout_marginBottom="16dp">
        
        <TextView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Status:"
            android:textSize="16sp"
            android:textStyle="bold" />
        
        <TextView
            android:id="@+id/statusText"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Not Active"
            android:textSize="14sp"
            android:textColor="@color/gray"
            android:layout_marginTop="8dp" />
    </LinearLayout>
    
    <!-- Stats Card -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:background="@drawable/card_background"
        android:padding="16dp"
        android:layout_marginBottom="16dp">
        
        <LinearLayout
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:orientation="vertical">
            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:text="Total Trades"
                android:textSize="12sp"
                android:textColor="@color/gray" />
            <TextView
                android:id="@+id/tradeCount"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:text="0"
                android:textSize="20sp"
                android:textStyle="bold"
                android:textColor="@color/primary" />
        </LinearLayout>
        
        <LinearLayout
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:orientation="vertical">
            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:text="Win Rate"
                android:textSize="12sp"
                android:textColor="@color/gray"
                android:gravity="center" />
            <TextView
                android:id="@+id/winRate"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:text="0%"
                android:textSize="20sp"
                android:textStyle="bold"
                android:textColor="@color/success"
                android:gravity="center" />
        </LinearLayout>
    </LinearLayout>
    
    <!-- Buttons -->
    <Button
        android:id="@+id/startButton"
        android:layout_width="match_parent"
        android:layout_height="56dp"
        android:text="Start Scanning"
        android:textSize="16sp"
        android:textStyle="bold"
        android:background="@color/primary"
        android:textColor="@color/white"
        android:layout_marginBottom="12dp" />
    
    <Button
        android:id="@+id/stopButton"
        android:layout_width="match_parent"
        android:layout_height="56dp"
        android:text="Stop Scanning"
        android:textSize="16sp"
        android:textStyle="bold"
        android:background="@color/secondary"
        android:textColor="@color/white"
        android:layout_marginBottom="16dp" />
    
    <!-- Last Trade Card -->
    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Last Trade"
        android:textSize="14sp"
        android:textStyle="bold"
        android:textColor="@color/primary" />
    
    <TextView
        android:id="@+id/lastTrade"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="No trades yet"
        android:textSize="12sp"
        android:textColor="@color/gray"
        android:background="@drawable/card_background"
        android:padding="12dp"
        android:layout_marginTop="8dp"
        android:layout_marginBottom="16dp" />
    
    <!-- Navigation Buttons -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:gravity="center">
        
        <Button
            android:id="@+id/historyButton"
            android:layout_width="0dp"
            android:layout_height="48dp"
            android:layout_weight="1"
            android:text="📊 History"
            android:textSize="12sp"
            android:background="@color/primary"
            android:textColor="@color/white"
            android:layout_marginEnd="8dp" />
        
        <Button
            android:id="@+id/settingsButton"
            android:layout_width="0dp"
            android:layout_height="48dp"
            android:layout_weight="1"
            android:text="⚙️ Settings"
            android:textSize="12sp"
            android:background="@color/primary"
            android:textColor="@color/white" />
    </LinearLayout>
</LinearLayout>
```

#### Settings Activity Layout
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">
    
    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Settings"
        android:textSize="24sp"
        android:textStyle="bold"
        android:textColor="@color/primary"
        android:layout_marginBottom="16dp" />
    
    <!-- Trade Amount -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:gravity="center_vertical"
        android:layout_marginBottom="16dp">
        <TextView
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Trade Amount (1-1000)"
            android:textSize="14sp" />
        <EditText
            android:id="@+id/tradeAmountInput"
            android:layout_width="100dp"
            android:layout_height="40dp"
            android:inputType="number"
            android:text="10"
            android:padding="8dp" />
    </LinearLayout>
    
    <!-- Scan Interval -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:gravity="center_vertical"
        android:layout_marginBottom="16dp">
        <TextView
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Scan Interval (0.5-5s)"
            android:textSize="14sp" />
        <EditText
            android:id="@+id/scanIntervalInput"
            android:layout_width="100dp"
            android:layout_height="40dp"
            android:inputType="numberDecimal"
            android:text="1"
            android:padding="8dp" />
    </LinearLayout>
    
    <!-- Notifications Toggle -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:gravity="center_vertical"
        android:layout_marginBottom="16dp">
        <TextView
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Notifications"
            android:textSize="14sp" />
        <CheckBox
            android:id="@+id/notificationToggle"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:checked="true" />
    </LinearLayout>
    
    <!-- Vibration Toggle -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:gravity="center_vertical"
        android:layout_marginBottom="16dp">
        <TextView
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Vibration"
            android:textSize="14sp" />
        <CheckBox
            android:id="@+id/vibrationToggle"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:checked="true" />
    </LinearLayout>
    
    <!-- Auto Trade Toggle -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:gravity="center_vertical"
        android:layout_marginBottom="32dp">
        <TextView
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Auto Trade"
            android:textSize="14sp" />
        <CheckBox
            android:id="@+id/autoTradeToggle"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:checked="true" />
    </LinearLayout>
    
    <!-- Clear History Button -->
    <Button
        android:id="@+id/clearHistoryButton"
        android:layout_width="match_parent"
        android:layout_height="48dp"
        android:text="Clear Trade History"
        android:textSize="14sp"
        android:background="@color/warning"
        android:textColor="@color/white"
        android:layout_marginBottom="12dp" />
    
    <!-- Save Button -->
    <Button
        android:id="@+id/saveButton"
        android:layout_width="match_parent"
        android:layout_height="48dp"
        android:text="Save Settings"
        android:textSize="14sp"
        android:background="@color/primary"
        android:textColor="@color/white" />
</LinearLayout>
```

#### Trade History Activity Layout
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">
    
    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Trade History"
        android:textSize="24sp"
        android:textStyle="bold"
        android:textColor="@color/primary"
        android:layout_marginBottom="16dp" />
    
    <RecyclerView
        android:id="@+id/tradeRecyclerView"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1"
        android:background="@drawable/card_background"
        android:padding="8dp" />
    
    <!-- Back Button -->
    <Button
        android:id="@+id/backButton"
        android:layout_width="match_parent"
        android:layout_height="48dp"
        android:text="Back"
        android:textSize="14sp"
        android:background="@color/primary"
        android:textColor="@color/white"
        android:layout_marginTop="12dp" />
</LinearLayout>
```

---

### Feature 14: Permissions ✅
**Required Permissions:**
```xml
<manifest>
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
    <uses-permission android:name="android.permission.FOREGROUND_SERVICE" />
    <uses-permission android:name="android.permission.FOREGROUND_SERVICE_CAMERA" />
    <uses-permission android:name="android.permission.VIBRATE" />
</manifest>
```

**Runtime Permissions Required:**
- SYSTEM_ALERT_WINDOW (for floating icon)
- ACCESSIBILITY_SERVICE (enable manually in Settings)
- CAMERA (for screen capture via MediaProjection)

---

### Feature 15: Error Handling ✅
**Error Cases:**

```kotlin
class ErrorHandler {
    fun handleScreenCaptureError(exception: Exception) {
        // Log error
        // Show notification "Screen capture failed"
        // Retry after 2 seconds
    }
    
    fun handlePatternMatchError(exception: Exception) {
        // Log error
        // Skip this scan
        // Continue to next scan
    }
    
    fun handleAccessibilityServiceError(exception: Exception) {
        // Log error
        // Show notification "Trade execution failed"
        // Skip this trade
    }
    
    fun handleDatabaseError(exception: Exception) {
        // Log error
        // Continue app (data not critical)
    }
    
    fun handleInvalidTradingWindow() {
        // Show alert: "Please tap during final 5 seconds"
        // Do NOT trade
        // Wait for next valid window
    }
}
```

---

## SECTION 5: BUILD SETUP

### Android Project Configuration

**build.gradle.kts (Project Level)**
```kotlin
plugins {
    id("com.android.application") version "8.0.0" apply false
    id("org.jetbrains.kotlin.android") version "1.9.10" apply false
}

buildscript {
    repositories {
        google()
        mavenCentral()
    }
}
```

**build.gradle.kts (App Level)**
```kotlin
plugins {
    id("com.android.application")
    id("kotlin-android")
    id("kotlin-kapt")
}

android {
    namespace = "com.mdjibon.quotex99"
    compileSdk = 34
    
    defaultConfig {
        applicationId = "com.mdjibon.quotex99"
        minSdk = 26
        targetSdk = 34
        versionCode = 1
        versionName = "1.0.0"
    }
    
    buildTypes {
        release {
            isMinifyEnabled = false
            proguardFiles(getDefaultProguardFile("proguard-android-optimize.txt"), "proguard-rules.pro")
        }
    }
    
    compileOptions {
        sourceCompatibility = JavaVersion.VERSION_11
        targetCompatibility = JavaVersion.VERSION_11
    }
    
    kotlinOptions {
        jvmTarget = "11"
    }
}

dependencies {
    // Core
    implementation("androidx.core:core-ktx:1.10.1")
    implementation("androidx.appcompat:appcompat:1.6.1")
    implementation("com.google.android.material:material:1.9.0")
    
    // UI
    implementation("androidx.constraintlayout:constraintlayout:2.1.4")
    
    // Kotlin Coroutines
    implementation("org.jetbrains.kotlinx:kotlinx-coroutines-android:1.7.1")
    
    // Room Database
    implementation("androidx.room:room-runtime:2.5.2")
    kapt("androidx.room:room-compiler:2.5.2")
    implementation("androidx.room:room-ktx:2.5.2")
    
    // OpenCV
    implementation("org.opencv:opencv-android:4.8.0")
    
    // ML Kit for OCR
    implementation("com.google.mlkit:text-recognition:16.0.0")
    
    // Testing
    testImplementation("junit:junit:4.13.2")
    androidTestImplementation("androidx.test.espresso:espresso-core:3.5.1")
}
```

**AndroidManifest.xml**
```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.mdjibon.quotex99">
    
    <!-- Permissions -->
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
    <uses-permission android:name="android.permission.FOREGROUND_SERVICE" />
    <uses-permission android:name="android.permission.FOREGROUND_SERVICE_CAMERA" />
    <uses-permission android:name="android.permission.VIBRATE" />
    <uses-permission android:name="android.permission.RECORD_AUDIO" />
    
    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:supportsRtl="true"
        android:theme="@style/Theme.AppCompat.Light.DarkActionBar">
        
        <!-- Main Activity -->
        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        
        <!-- Other Activities -->
        <activity android:name=".SettingsActivity" />
        <activity android:name=".TradeHistoryActivity" />
        
        <!-- Services -->
        <service
            android:name=".service.FloatingIconService"
            android:enabled="true"
            android:exported="false" />
        
        <service
            android:name=".service.ScreenCaptureService"
            android:enabled="true"
            android:exported="false" />
        
        <service
            android:name=".service.ScanningService"
            android:enabled="true"
            android:exported="false" />
        
        <service
            android:name=".service.TradeExecutorService"
            android:enabled="true"
            android:exported="false" />
        
        <service
            android:name=".accessibility.QuotexAccessibilityService"
            android:permission="android.permission.BIND_ACCESSIBILITY_SERVICE"
            android:exported="true">
            <intent-filter>
                <action android:name="android.accessibilityservice.AccessibilityService" />
            </intent-filter>
            <meta-data
                android:name="android.accessibilityservice"
                android:resource="@xml/accessibility_service_config" />
        </service>
    </application>
</manifest>
```

---

## SECTION 6: BUILD INSTRUCTIONS

### Step 1: Clone or Download Repository
```bash
git clone https://github.com/mdsakibsoniya-ai/Quotex-99-Accuracy.git
cd Quotex-99-Accuracy
```

### Step 2: Open in Android Studio
- File → Open → Select the project folder
- Wait for Gradle sync to complete

### Step 3: Add Pattern Images
- Create `app/src/main/assets/patterns/` directory
- Add all 96 `.png` pattern files
- Add `pattern_list.txt` file
- Extract from provided ZIP package

### Step 4: Build APK
```bash
./gradlew clean assembleRelease
```

### Step 5: Locate APK
```bash
app/build/outputs/apk/release/app-release.apk
```

### Step 6: Deploy via CodeMagic
1. Go to codemagic.io
2. Create new app
3. Select Android
4. Connect GitHub repository
5. Add build command: `./gradlew assembleRelease`
6. Start build
7. Download APK from CodeMagic dashboard

### Step 7: Install on Device
```bash
adb install app/build/outputs/apk/release/app-release.apk
```

### Step 8: Enable Accessibility Service
1. Open Settings
2. Go to Accessibility
3. Find "Md Jibon Quotex 99%"
4. Enable the service

### Step 9: Grant Permissions
- Allow SYSTEM_ALERT_WINDOW when prompted
- Allow other permissions as needed

### Step 10: Launch App
- Open "Md Jibon Quotex 99%" from app drawer
- Floating icon should appear immediately

---

## SECTION 7: ACCEPTANCE CRITERIA (CHECKLIST)

Before submission, verify all of the following:

- [ ] App name is "Md Jibon Quotex 99%"
- [ ] Package name is "com.mdjibon.quotex99"
- [ ] Floating icon appears on screen
- [ ] Floating icon is draggable
- [ ] Floating icon shows active/inactive state
- [ ] Tapping icon starts/stops scanning
- [ ] Blue overlay appears when scanning active
- [ ] Blue overlay disappears when scanning stops
- [ ] Screen capture works (chart visible)
- [ ] Chart region extraction works
- [ ] Candlestick analysis works (candles detected)
- [ ] Pattern detection creates correct signature
- [ ] All 96 patterns load successfully
- [ ] Pattern matching calculates similarity correctly
- [ ] Market detection works (OCR working)
- [ ] BUY/SELL decision is correct
- [ ] Trade executes only in last 5 seconds window
- [ ] Accessibility Service clicks correct buttons
- [ ] Trade amount is filled automatically
- [ ] CONFIRM button is clicked automatically
- [ ] Trade is logged to database
- [ ] Trade history displays correctly
- [ ] Settings save and load correctly
- [ ] Win rate calculates correctly
- [ ] Notifications work (sound + vibration)
- [ ] No crash during normal operation
- [ ] No excessive battery drain
- [ ] No excessive memory usage
- [ ] APK builds successfully without errors
- [ ] APK is installable on Android device
- [ ] APK runs without force close

---

## SECTION 8: FINAL NOTES FOR DEVELOPER

1. **Do not ask questions** — all information is here
2. **Do not modify timing** — 15 seconds + 5 second window is fixed
3. **Do not skip features** — all features are required
4. **Do not change app name** — must be "Md Jibon Quotex 99%"
5. **Start immediately** — no dependencies on external resources
6. **Use the exact structure** — follow project structure provided
7. **Follow exact logic** — use algorithms provided
8. **Test thoroughly** — verify all acceptance criteria
9. **Submit complete APK** — ready for deployment

---

## SUMMARY

The app must be exactly as described:
- Floating icon overlay with start/stop scanning
- Blue scan effect while scanning active
- Screen capture + candlestick pattern analysis
- 96 pattern database matching with 90%+ threshold
- Auto-execute BUY/SELL only in final 5 seconds of 15-second candle
- Accessibility Service for trade automation
- Trade history logging + win rate calculation
- Settings UI with configurable options
- Multi-market simultaneous scanning support

**Build this exactly as specified. No exceptions. Start now.**
