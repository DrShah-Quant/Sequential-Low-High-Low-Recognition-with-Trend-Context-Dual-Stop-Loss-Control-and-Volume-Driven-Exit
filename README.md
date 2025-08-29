# 📈 Adaptive Allocation Swing Breakout Strategy:

### Sequential Low–High–Low Recognition with Trend Context, Dual Stop-Loss Control, and Volume-Driven Exit

---

## 🔍 Strategy Description

This algorithm implements a **swing-trading breakout strategy** that dynamically allocates capital based on **sequential swing patterns**, trend context, and volume confirmation. It integrates **pattern recognition, adaptive buying rules, dual stop-loss protection, and volume-based exits** for robust trade management.

---

### **Step 1: Trend Labeling (Context Detection)**

* Uses a **sliding 4-price window** to detect:

  * **Uptrend (1)**: Higher highs/lows continuation.
  * **Downtrend (0)**: Lower highs/lows continuation.
  * **Neutral (-1)**: No clear structure.
* These labels create a timeline of market structure.

**Trading Interpretation:**
Trend labeling provides the **macro context**. Breakout trades are taken with awareness of prevailing structural moves.

---

### **Step 2: Macro Swing Low–High–Low Recognition**

* Extracts **macro swing lows** and **swing highs** from trend-labeled data.
* Checks for **sequential order (Low → High → Low → High → Low)**.
* If condition is met → potential **buy pattern** is identified.

**Trading Interpretation:**
The **sequential Low–High–Low breakout** forms the backbone of the strategy, signaling trend continuation.

---

### **Step 3: Adaptive Allocation Entry Rule**

* On a valid **buy pattern**, the algorithm evaluates **volume and price context**:

  * If current price < last buy price → Allocate **5% of available capital**.
  * Otherwise → Allocate **3% of available capital**.
* Position size is determined by dividing allocated capital by current price.
* Each buy is logged with **timestamp, price, and stop-loss**.

**Trading Interpretation:**
The strategy **adds more aggressively on dips** but scales more conservatively when buying into strength.

---

### **Step 4: Dual Stop-Loss Protection**

* Stop-loss is the **max of**:

  1. **8% below entry price**, and
  2. **Second-last swing low**.

**Trading Interpretation:**
This ensures protection from **both random noise (8%)** and **structural breakdowns (swing low breach)**.

---

### **Step 5: Exit Conditions**

1. **Macro Weakness Exit ("SELL ALL")**

   * Triggered if **swing low count decreases** (structural weakening).
   * All positions are liquidated.

2. **Volume Spike Exit**

   * If volume > **105% of 3-bar average** and price closes above open →
   * Trigger **sell signal**, closing positions.

**Trading Interpretation:**
Exits occur when either **trend weakens structurally** or **climax-like volume exhaustion** is detected.

---

## 📚 Libraries Used

* **AlgoAPI (AlgoAPIUtil, AlgoAPI\_Backtest)**

  * Event-driven backtesting and trading infrastructure.
  * Provides bulk data feeds, instrument subscription, and logging utilities.

* **datetime**

  * Used for timestamp handling in trend labeling and trade logging.

