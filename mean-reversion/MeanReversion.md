# 📉 Learning Journey: Mean Reversion

**Mean reversion** is the idea that after an extreme move, many series—especially prices—tend to drift back toward a “normal” or **average** level. Prices often oscillate around that average and repeatedly revisit it over time.

Mean reversion applies not only to **prices**. You can use the same intuition for **volatility**, **earnings**, **growth rates**, and **indicator levels**.

> **Reference:** This note summarizes concepts discussed in [Mean reversion: trading strategies and indicators](https://www.cmcmarkets.com/en-gb/trading-strategy/mean-reversion) (CMC Markets). Charts and platform-specific examples in the original article are not reproduced here—open the link for visuals.

---

## Contents

- [What is mean reversion in trading?](#what-is-mean-reversion-in-trading)
- [Mean reversion formula](#mean-reversion-formula)
- [Example of mean reversion](#example-of-mean-reversion)
- [Mean reversion strategies](#mean-reversion-strategies)
- [Mean reversion and regression](#mean-reversion-and-regression)
- [Building a mean reversion workflow](#building-a-mean-reversion-workflow)
- [Automation (e.g. MT4)](#automation-eg-mt4)
- [Summary](#summary)

---

## What is mean reversion in trading?

In trading, mean reversion **theorizes** that values tend to return toward average levels and that **large, sustained deviations** from that average are often hard to maintain. Practitioners look for **extremes**—in price, volatility, growth, or an indicator—and bet that the series will **move back** toward a typical level.

That does **not** guarantee timing or direction on every trade; it is a **framework** for signals and risk management, not a law of physics.

---

## Mean reversion formula

To work with mean reversion, you first need a **mean**: the average over a chosen window of observations.

- On a price chart, a common proxy is the **simple moving average (SMA)**—the arithmetic average of prices over the last \(n\) periods.
- Over time, price often **wanders around** that average and eventually **crosses or nears** it again.

**Distance from the mean** (e.g. price minus SMA, or standardized distance) is a building block for signals.

**Indicators** that relate price to a moving average and a measure of spread—**Bollinger Bands**, **Keltner channels**, **envelopes**, **regression channels**—help flag when price is **far** from “typical.” They provide **signals**, not guarantees of reversal.

---

## Example of mean reversion

Reversion does **not** always mean “price falls back down to the mean” or “rises up to the mean.” The **mean itself moves** (e.g. the SMA updates every bar). If price **stalls**, the average can **catch up** to price—**that** is still a form of mean reversion: price and average are **aligned** again.

Indicators that use **standard deviation** (e.g. Bollinger Bands) measure how far price sits from the mean in **volatility units**. Larger deviations sometimes precede moves back toward the mean, but **not necessarily immediately**.

---

## Mean reversion strategies

Strategies try to **profit as** price or a spread **returns** toward a more normal level. Important nuance: if price **runs away** from the average, the next “reversion” might be the **average moving toward price**, not price crashing back. Reversion **happens often**; **sitting exactly on** the mean usually does **not** last long.

### Pairs trading (statistical arbitrage)

- Find two **highly correlated** instruments whose prices usually **move together**.
- When they **diverge** (one lags, one leads), you may **long the weak** name and **short the strong** name, betting the **spread** **converges** again.
- **Hedge ratio** matters: if one asset moves roughly **twice** as much as the other per day, position sizes are often scaled so the trade is **balanced** on risk, not just dollar-neutral.
- **Transaction costs** and **divergence risk** matter: tiny gaps may not be worth trading; **stop-losses** limit damage if the pair **does not** realign.

### Intraday mean reversion

- Day traders often work **around a moving average** in a **trending** environment: in an uptrend, **pullbacks toward** the average may offer **long** entries; in a downtrend, **rallies to** the average may offer **short** entries.
- This style often **pairs** with **trend context**; pure chop without trend can make mean-reversion around one line **less reliable**. (Strong trend-following is closer to **momentum**—worth studying as a separate topic.)

### Forex-style oscillator approach (MACD / PPO)

- Tools like **MACD** or **PPO** can compare a **fast** view of price (e.g. fast length 1) to a **slow** average (e.g. 21 periods), so the oscillator shows **deviation from** a mean-like level.
- Traders sometimes mark **historical reversal zones** on the indicator and combine **break back through** a level with a **target** near the mean (or indicator zero line) and a **stop** beyond a recent swing.
- **Past behavior** does not guarantee the future; **volatility regimes** change—**stops** address when the pattern **fails**.

---

## Mean reversion and regression

A **regression line** is another way to define “normal”: the **best-fit line** through a segment of prices. Price often **oscillates** around that line. **Channel tools** (e.g. linear regression with upper/lower bounds) mark **extreme** distances from the line where **reversion toward the line** might be considered—again, as a **signal**, not certainty.

---

## Building a mean reversion workflow

A practical setup for research or discretionary trading often combines:

| Idea | Role |
|------|------|
| Moving averages / regression | Define the **mean** or **trend line** |
| Bands, channels, or z-scores | Measure **how extreme** the deviation is |
| Spreads (pairs) or single-name signals | Define **what** you trade |
| Stops and position sizing | **Risk** when the mean does not come soon enough |

For **pairs**, overlaying two series on one chart (or modeling the spread in code) helps spot **divergence** and plan **entries/exits**.

---

## Automation (e.g. MT4)

Platforms such as **MetaTrader 4** support **Expert Advisors (EAs)**—rules coded to run automatically. Mean reversion logic can be implemented as EAs; community libraries exist, but **always** validate logic, costs, and risk on **your** data and constraints.

---

## Summary

- Mean reversion is a **useful mental model**: extremes often **partially unwind** toward a moving average or equilibrium spread—but **when** and **how** are **uncertain**.
- Price can **stay away** from the mean longer than expected; **trends** and **volatility** can **change**.
- **Risk management** (stops, size, diversification) matters because **reversion is not guaranteed** on your horizon.

This document is **educational**, not investment advice. For the full article, examples, and disclaimers from the publisher, see [CMC Markets — Mean reversion](https://www.cmcmarkets.com/en-gb/trading-strategy/mean-reversion)

---

## See also

- [CMC Markets: Mean reversion — trading strategies and indicators](https://www.cmcmarkets.com/en-gb/trading-strategy/mean-reversion)
