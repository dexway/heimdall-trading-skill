---
name: heimdall-trading
description: Heimdall Trading — a mechanical, top-down chart-reading system (market structure, order blocks, liquidity, imbalances, 50 EMA bias, premium/discount) plus a WAIT-STATE guardrail. Use when reading or marking up charts, building a bias, checking a setup against rules, or analysing Deriv synthetic indices, forex, gold or US indices. Describes charts against rules; never gives buy/sell advice.
---

# Heimdall Trading

A rule-based way to read a chart from the top down and say, objectively, which conditions of a setup are met and which are still missing.

**Guardrail.** Use this to describe what the chart shows. Never turn it into personal "buy now / sell now", position sizing, or "take this trade" advice. The trader decides and executes. Mechanical levels may be quoted as *what the rules produce*, not as a recommendation.

**Credit.** The framework was inspired by public lessons on the Trading Fanatic YouTube channel (youtube.com/@TradingFanatic). This file is an independent, simplified, mechanical restatement written for this project; it is not that channel's material or its paid program, and nothing here is endorsed by it.

---

## 1. Three timeframes, read top-down

| Role | Default | What you decide there |
|---|---|---|
| Bias | 4H (Daily for swing) | Direction, the current dealing range, strong vs weak swing points, premium/discount |
| Zones | 15M | Internal structure inside the 4H leg; the order block that would host a trade |
| Trigger | 5M (1M for tight entries) | Only after a 15M zone is reached: a liquidity sweep followed by a trend change |

- The higher timeframe wins any disagreement. If a lower timeframe turns unexpectedly, look one timeframe up for the reason.
- Daily and Weekly are a quick context glance: is price pushing or pulling back, and is it sitting inside a large higher-timeframe zone or imbalance?

## 2. Market structure

- **Uptrend:** higher highs and higher lows. **Downtrend:** lower lows and lower highs. **Range:** highs and lows keep failing to break.
- **Swing points.** This project uses *fractal* swings (a high with lower highs on both sides; a low with higher lows on both sides; two candles each side by default). A stricter alternative is the "valid range" rule: a swing only counts once the pullback away from it prints a candle closing the other way **and** a candle that fails to extend the extreme.
- **Break of structure (BOS):** price takes the last swing in the direction of the trend — continuation.
- **Trend change (TC):** price takes the last swing *against* the trend — the first sign the direction has flipped. A new trend is only established after a second swing confirms it.
- **Strong vs weak points.** The swing that caused a break is *strong* (it is defended). The extreme that has not caused a break is *weak* (it tends to be taken). Plan away from strong points and toward weak ones.
- **Wick or body.** Pick one definition of a break and stay consistent; this engine counts wicks. Context outranks break type: a break straight into an obvious liquidity pool, or against the higher-timeframe bias, is suspect. Many wick breaks in a row means chop — stand aside.

## 3. Premium and discount

- Measure the current 4H dealing range (strong point to the latest extreme). Only three levels matter: 0, 50%, 100%.
- In an uptrend, look for longs in the lower half (discount); in a downtrend, shorts in the upper half (premium). 50% is equilibrium.
- Fast, momentum-driven instruments often retrace less than half; know the instrument before demanding a deep pullback.

## 4. Order blocks (zones)

An order block qualifies only if both are true:
1. **It broke structure** — the move away took out a fractal swing.
2. **It left an imbalance** — a fair value gap (three candles where the outer two wicks don't overlap).

Then:
- The zone is the last opposite-coloured candle before the impulse, **including any run of consecutive opposite candles** before it. Don't shrink it to a sliver; a larger zone plus a lower-timeframe trigger beats a tiny zone that never gets reached.
- Use recent zones aligned with the current trend. Old zones against the trend are just reaction points.
- A zone is considered spent once a candle closes through it.
- Avoid zones sitting at the far extreme of the range: a pullback that deep is close to a trend change.

## 5. Liquidity

Resting orders cluster above highs and below lows. The engine tracks:
- **Equal highs / equal lows** (within ~0.15 ATR) that price has not yet swept.
- **Inducement:** a minor swing just before a zone that tempts early entries.
- **Fake trend change:** a flip that happens *before* liquidity is taken; the real one usually follows the sweep.

Rule: **wait for the sweep before the trigger**, and require momentum after it. Entering before the sweep is how traders become the liquidity.

## 6. The 50 EMA as an objective filter

- Bias requires the 4H structure and the 50 EMA to agree: price above a rising EMA for longs, below a falling EMA for shorts.
- Flat EMA (slope under ~0.1 ATR over five bars) = consolidation. Stand aside.
- Timeframes disagreeing = a "determination zone". Do nothing until they line up.

## 7. WAIT-STATE guardrail

Two conditions block an otherwise complete setup:
- **Compression:** the last 10 trigger-timeframe candles average less than 60% of the last 100 candles' range — the market is coiling.
- **Over-extension:** the trigger candle's body is more than 2.5× the average of the previous 14 bodies — chasing it risks an immediate snap-back.

Waiting is a valid decision. Say "sit on hands" when either is true.

## 8. The checklist

1. 4H structure and 50 EMA agree (bias).
2. Price is in the correct half of the 4H range.
3. An unbroken 15M order block exists in the bias direction.
4. Price has reached that zone.
5. A 5M liquidity sweep has happened in or near the zone.
6. A 5M trend change follows with momentum.
7. The WAIT-STATE guardrail is clear.
8. *(Confluence, not required)* the trigger leg left a fair value gap.

When 1–7 are met, the mechanical levels are: entry at the trigger close, stop beyond the sweep (+0.25 ATR), target at 2.5R or the 4H weak high/low.

## 9. How to report a read

For each of 4H, 15M and 5M give: trend, last BOS/TC, strong and weak points, premium/discount position, EMA side and slope, the nearest qualifying zone, and visible liquidity pools. Then:
- Classify the state: aligned, pullback, determination zone, or consolidation.
- List each checklist item as met or missing, and name the exact event that would complete the next missing one.
- Give one bullish and one bearish scenario, each with its trigger and its liquidity target. Let the market choose.

## 10. Evidence and limits

- **Backtest (60 days, 18 Deriv synthetic indices, 2.5R target, one trade at a time):** rules alone 268 trades, 31.7% wins, +27.7R, max drawdown −20R. With the WAIT-STATE guardrail: 208 trades, 32.2% wins, +25.5R, max drawdown −15R. Per-symbol samples are small; treat this as unproven.
- Deriv Volatility and Step indices are generated by a random number generator. There are no sessions, news or institutional order flow behind their "structure", so session rules don't apply and any edge must be proven by your own testing.
- Gold, forex and US30 do have sessions and news; respect them.
- This is educational software. It is not financial advice.

## 11. Gold (XAU/USD) notes

Gold has sessions and news, so read it with these additions to the checklist.

- **Shallow pullbacks.** Gold is a momentum market and often retraces only about 30% of a leg. A setup that insists on a deep discount can miss the move, so state how deep the pullback actually is.
- **Round numbers.** Levels at every 10, 50 and 100 attract liquidity. Note any that sit near a zone or a stop.
- **Violent sweeps.** Rule-based stop levels belong beyond the sweep wick plus a buffer.
- **News blackout.** Gold reacts to all high-impact USD news. Report WAIT-STATE from 30 minutes before to 30 minutes after an event.
- **Correlation.** Gold usually moves against the dollar and US yields. A rally alongside a rising dollar is unusual, so flag it. Silver is the comparison market: a new gold low that silver does not confirm is a divergence worth noting.
- **Precision and evidence.** Quote gold levels to 2 decimals. The backtest in section 10 did not include gold, and Deriv's free feed serves too little gold history to test these notes, so they are unproven.

## Live data

Deriv public candles (no account needed): `wss://api.derivws.com/trading/v1/options/ws/public`, request
`{"ticks_history": "R_75", "style": "candles", "granularity": 900, "count": 300, "end": "latest"}`.
Instruments covered: R_10/25/50/75/100, 1HZ10V/15V/25V/30V/50V/75V/90V/100V, stpRNG–stpRNG5, frxXAUUSD, frxEURUSD, frxGBPUSD, frxGBPJPY, OTC_DJI.
