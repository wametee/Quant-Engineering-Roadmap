# Futures, Options & Volatility — How It Fits Together

This note builds ideas **step by step** so they connect to **real trading**, not just definitions.

---

## 1. What Are Futures and Options?

### Futures

A **futures contract** is an agreement to **buy or sell** an asset at a **fixed price** on a **future date**.

**Example:** You agree today to buy oil at **$80** in **three months**. You are generally **obligated** to follow through (or to **close** the position before expiry by offsetting in the market).

**Typical uses**

| Use | Idea |
|-----|------|
| **Hedging** | Lock in price to **reduce** business or portfolio risk |
| **Speculation** | Bet on **direction** (or carry) with leverage-like exposure |

### Options

An **option** gives you the **right**, but **not the obligation**, to buy or sell something at a **set price** before (or at) a **certain date**. You pay a **premium** for that right.

| Type | Right |
|------|--------|
| **Call** | Right to **buy** |
| **Put** | Right to **sell** |

### Futures options (the bridge)

A **futures option** is an option whose **underlying** is a **futures contract**, not the spot commodity or stock itself.

So instead of “buying oil” in the spot sense, you might hold the **right to enter** a specific **oil futures** position at a defined strike. Same logic chain: **premium** → **right** → **underlying is futures**.

---

## 2. Key Option Concepts

| Term | Meaning |
|------|--------|
| **Strike** | Price at which you may buy (call) or sell (put) |
| **Expiration** | Last moment the right exists (style matters: American vs European, etc.) |
| **Premium** | What you pay (long) or receive (short) for the option |

### Moneyness (rough intuition)

| Label | Call (simplified) | Put (simplified) |
|-------|-------------------|------------------|
| **ITM** | Spot **above** strike → exercise has “real” edge | Spot **below** strike |
| **ATM** | Spot **≈** strike | Spot **≈** strike |
| **OTM** | Spot **below** strike | Spot **above** strike |

ITM options have **intrinsic** value if exercised *now*; OTM options are **all extrinsic** until the market moves.

---

## 3. Volatility (Why It Dominates Options)

**Volatility** measures **how much** price tends to **move** (usually annualized in models).

- **High vol** → larger typical swings  
- **Low vol** → calmer paths  

### Two vols traders separate

1. **Historical volatility (HV)** — inferred from **past** returns.  
2. **Implied volatility (IV)** — the vol **implied by current option prices** (what the market is “pricing in” forward-looking uncertainty).

👉 In practice, **IV** is what options traders argue about most: it is **extracted** from premiums using a pricing model, then used to compare **cheap vs rich** options.

### Why vol matters even if spot barely moves

Option premiums embed **expected movement** and **time**. **Higher IV** → **more expensive** options (all else equal). **Lower IV** → **cheaper** options.

So you can be **roughly right on direction** and still lose if **IV collapses** or **time decay** eats you—see below.

---

## 4. Option Pricing — Core Idea

Models such as **Black–Scholes–Merton** (and **binomial/lattice** trees) connect:

- Underlying price  
- Strike  
- Time to expiry  
- Volatility (**critical**)  
- Rates (and sometimes dividends / carry)  

…to a **fair value** or **no-arbitrage** range for the premium.

### Intrinsic vs extrinsic

| Piece | Meaning |
|-------|--------|
| **Intrinsic** | Payoff **if exercised now** (max of zero and immediate moneyness) |
| **Extrinsic** | **Everything else**: time value + vol + rates effects (“optionality”) |

Long options are **long convexity**: you can benefit from large moves; you pay for that in **premium** and **theta**.

---

## 5. The Greeks (Sensitivity, Not Magic)

Greeks describe **how the option price changes** when inputs move:

| Greek | Measures |
|-------|----------|
| **Delta (Δ)** | Sensitivity to **underlying price** (also used as a hedge ratio) |
| **Gamma (Γ)** | Rate of change of **delta** (curvature / pin risk) |
| **Theta (Θ)** | **Time decay** — option value erosion per day |
| **Vega** | Sensitivity to **IV** |
| **Rho (ρ)** | Sensitivity to **interest rates** (often smaller for short-dated equity options) |

👉 Serious risk management is **delta-aware**, often **gamma-aware**, and always **theta- and vega-aware** for directional vs vol trades.

---

## 6. What a Standard Derivatives Textbook Covers

A common anchor is **John C. Hull**, *Options, Futures, and Other Derivatives* — widely used for market structure and pricing.

**Simplified map**

1. **Foundations** — Futures vs options, mechanics, margin, arbitrage intuition.  
2. **Pricing** — Black–Scholes, risk-neutral expectation, replication / no-arbitrage.  
3. **Volatility** — IV, smiles and skews, model vs market.  
4. **Hedging** — Delta hedging, P&L from gamma/theta, portfolio Greeks.  
5. **Strategies** — Spreads, straddles/strangles, butterflies, protective puts, covered calls, etc.  
6. **Options on futures** — Different carry/convenience; contract specs; hedging with futures options.  
7. **Risk** — VaR, stress tests, tail scenarios.

Use the book for **rigor**; use markets for **behavior** (skew, term structure, event IV).

---

## 7. Real Trading Reality Check

Options are **not** “easy money.” Most edges are small and **fragile**.

You can be **right on direction** and still lose because:

- **Theta** — time runs out; OTM options can go to zero.  
- **Vega** — IV **drops** after events (“vol crush”).  
- **Gamma path** — you needed a **large enough** move **soon enough**.

**Risk control** (size, max loss, structure choice, and when *not* to trade) matters as much as the thesis.

---

## 8. Simple P&L Example (Call)

- Stock **$100**  
- **Call** strike **$105**, premium **$3**  

If at expiry stock is **$110**:

- Intrinsic at expiry = \(110 - 105 = 5\) per share (on the contract notional, multiply by contract size in real markets).  
- Profit vs premium paid ≈ **$5 − $3 = $2** *per share of underlying represented by one option unit* (simplified; ignores fees and early exercise nuances).

If the stock **drifts** to **$106** but **IV falls** or **time** passes:

- Mark-to-market P&L can still be **negative** even with a **slight** favorable move—**extrinsic** value shrank.

---

## 9. How This Folder Fits In

Use this doc with the rest of **`optionVolatilityPricing/`** as a **concept spine**: definitions → vol → pricing → Greeks → strategies → **reality** (theta, IV, path).

When you code or paper-trade, force yourself to answer:

1. What am I **long/short** in: **delta, vega, theta**?  
2. What has to happen in **price**, **time**, and **IV** for this to win?

That is how book knowledge becomes **trading sense**.

---

## Further reading

- Hull, *Options, Futures, and Other Derivatives* (any recent edition).  
- Companion notes in this repo: `optionVolatilityPricing/README.md`, `languageOfOptions.md` (if present).

*Educational material only; not investment advice.*
