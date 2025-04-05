# 📈 BTC Breakout RSI Trend Strategy

A backtest-ready Pine Script strategy designed for **Bitcoin (BTC)** and other crypto pairs using **4H charts**.

This script captures **breakouts** from consolidation zones, with filters like:
- ✅ RSI confirmation
- ✅ 50 EMA trend direction
- ✅ Take Profit & Stop Loss system

---

## 🔍 Strategy Logic

The strategy identifies when price breaks out of a tight range (default: 30 candles), and enters a trade **only when RSI confirms momentum**.

### Long Setup:
- Price closes **above** the highest high of range
- RSI is **above** a threshold (e.g., 50)
- Optional: Price is **above EMA 50**

### Short Setup:
- Price closes **below** the lowest low of range
- RSI is **below** a threshold (e.g., 50)
- Optional: Price is **below EMA 50**

---

## ⚙️ Settings

| Parameter           | Description                                 |
|---------------------|---------------------------------------------|
| Range Length        | Number of bars to define range              |
| Breakout Buffer     | Adds % buffer to prevent fakeouts           |
| RSI Period          | RSI calculation length                      |
| RSI Min/Max         | Entry filter for longs/shorts               |
| EMA Filter          | Trend filter using 50 EMA                   |
| Take Profit / SL    | Risk management in %                        |

---

## 📊 Backtest Instructions

1. Open TradingView → Pine Editor  
2. Paste the contents of `BTC_Breakout_RSI_Trend_Strategy.pine`  
3. Click “Add to Chart”
4. Adjust parameters to fit your asset or timeframe

---

## 💡 Tips
- Best on trending pairs (BTC/ETH)
- Works well on 4H and 1H
- Combine with other confluence tools (e.g., volume, divergence)
