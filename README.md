//@version=5
strategy("BTC Breakout RSI Trend Strategy", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=10)

// === INPUTS === //
rangeLength = input.int(30, title="Range Length (Bars)")
breakoutBuffer = input.float(0.5, title="Breakout Buffer (%)") / 100
rsiPeriod = input.int(14, title="RSI Period")
rsiMin = input.int(50, title="Minimum RSI for Long")
rsiMax = input.int(50, title="Maximum RSI for Short")
useMAFilter = input.bool(true, title="Filter with 50 EMA?")
takeProfit = input.float(3.0, title="Take Profit (%)") / 100
stopLoss = input.float(1.5, title="Stop Loss (%)") / 100

// === CALCULATIONS === //
highestHigh = ta.highest(high, rangeLength)
lowestLow = ta.lowest(low, rangeLength)
rangeMid = (highestHigh + lowestLow) / 2

rsi = ta.rsi(close, rsiPeriod)
ema50 = ta.ema(close, 50)

// === CONDITIONS === //
longCond = close > highestHigh * (1 + breakoutBuffer) and rsi > rsiMin and (not useMAFilter or close > ema50)
shortCond = close < lowestLow * (1 - breakoutBuffer) and rsi < rsiMax and (not useMAFilter or close < ema50)

// === STRATEGY EXECUTION === //
strategy.entry("Long", strategy.long, when=longCond)
strategy.exit("Long TP/SL", from_entry="Long", profit=takeProfit, loss=stopLoss)

strategy.entry("Short", strategy.short, when=shortCond)
strategy.exit("Short TP/SL", from_entry="Short", profit=takeProfit, loss=stopLoss)

// === PLOTTING === //
plot(highestHigh, color=color.green, title="Range High", linewidth=1)
plot(lowestLow, color=color.red, title="Range Low", linewidth=1)
plot(rangeMid, color=color.gray, title="Mid Range", style=plot.style_dotted)

plot(ema50, color=color.orange, title="EMA 50")
