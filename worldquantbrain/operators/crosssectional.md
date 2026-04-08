# 📊 Learning Journey: Cross-Sectional Operators in WorldQuant BRAIN

**Cross-Sectional Operators** in the WorldQuant BRAIN platform.  
These operators transform values across instruments on the same date, helping normalize signals, reduce outliers, and control portfolio exposure.

---

## 🎯 Purpose
The goal of this learning is to:
- Understand daily cross-sectional transformations across the universe.
- Learn how to normalize, rank, scale, and robustify alpha vectors.
- Build more stable and comparable signals across instruments.

---

## 📚 Operators and Examples

### 1. `normalize(x, useStd = false, limit = 0.0)`
- **Definition:** Mean-centers values each day; optionally divides by cross-sectional std and optionally clamps to `[-limit, +limit]`.
- **NaN Handling:** NaNs are ignored in mean/std calculations and remain NaN in output.
- **Use Case:** Cross-sectional de-meaning and optional z-score-style scaling.
- **Example:**  
  `normalize(rank(returns), useStd=true, limit=3)`

---

### 2. `quantile(x, driver = gaussian, sigma = 1.0)`
- **Definition:** Ranks and shifts cross-sectional values, then maps to chosen distribution.
- **Drivers:** `gaussian`, `cauchy`, `uniform`.
- **Sigma:** Scales the final output (affects scale, not rank order).
- **Use Case:** Distribution shaping and outlier control while preserving rank structure.
- **Examples:**  
  `quantile(implied_volatility_call_60 - implied_volatility_put_60, driver=cauchy)`  
  `quantile(close, driver=gaussian, sigma=0.5)`

---

### 3. `rank(x, rate = 2)`
- **Definition:** Cross-sectional rank mapped to `[0,1]` for each date.
- **Use Case:** Robust normalization and reduced sensitivity to raw scale/outliers.
- **Note:** `rate` controls sorting precision (`rate=0` for exact sorting).
- **Example:**  
  `rank(ts_returns(close, 5))`

---

### 4. `scale(x, scale = 1, longscale = 1, shortscale = 1)`
- **Definition:** Rescales vector so total absolute exposure matches target size.
- **Default:** `sum(abs(output)) = 1`.
- **Use Case:** Book-size control and exposure normalization.
- **Flexibility:** `longscale` and `shortscale` allow asymmetric long/short sizing.
- **Example:**  
  `scale(returns, scale=4)`

---

### 5. `winsorize(x, std = 4)`
- **Definition:** Clamps values to mean ± `std` * standard deviation.
- **Use Case:** Reduce impact of extreme outliers before further modeling.
- **Example:**  
  `winsorize(ts_backfill(fn_op_lease_min_pay_due_a/enterprise_value, 63), std=4.0)`

---

### 6. `zscore(x)`
- **Definition:** Standardizes cross-sectional values as `(x - mean(x)) / std(x)`.
- **Interpretation:** Output in standard deviation units (mean ~0, std ~1).
- **Use Case:** Make different fields directly comparable and reduce outlier influence.
- **Example:**  
  `zscore(close)`

---

## 🧮 Walkthrough: `normalize` Example
Given a single day cross section:

`x = [3, 5, 6, 2]`

- Mean = `(3 + 5 + 6 + 2) / 4 = 4`
- Mean-centered = `[-1, 1, 2, -2]`

1. `normalize(x, useStd=false, limit=0.0)`  
   Output: `[-1, 1, 2, -2]`

2. `normalize(x, useStd=true, limit=0.0)`  
   Cross-sectional std of centered values is about `1.82`, so output is about `[-0.55, 0.55, 1.10, -1.10]`

3. `normalize(x, useStd=true, limit=1.0)`  
   Clamp step (2) to `[-1, 1]` -> `[-0.55, 0.55, 1.00, -1.00]`

4. `normalize(x, useStd=false, limit=1.5)`  
   Clamp step (1) to `[-1.5, 1.5]` -> `[-1, 1, 1.5, -1.5]`

---

## 🛠️ Practical Outcomes
By mastering cross-sectional operators, I will:
- Convert raw signals to comparable daily vectors across stocks.
- Control leverage and long/short book balance with `scale`.
- Improve robustness using `rank`, `quantile`, `winsorize`, and `zscore`.
- Reduce model instability caused by outliers and raw unit differences.

---

## 💡 High-Value Tips
- Use `rank` as a robustness check at the end of your alpha pipeline.
- Apply `winsorize` before regression or averaging when tails are noisy.
- Use `normalize(..., useStd=true)` for z-score-like daily standardization.
- Use `quantile(..., driver=cauchy)` when you want heavier tails than Gaussian mapping.
- Use separate `longscale`/`shortscale` if your strategy needs asymmetric exposure.

---

## 📅 Progress Tracking
- [ ] Cross-Sectional Centering (`normalize`)
- [ ] Distribution Mapping (`quantile`)
- [ ] Robust Ranking (`rank`)
- [ ] Book Control (`scale`)
- [ ] Outlier Handling (`winsorize`, `zscore`)

---

## 🚀 Big Takeaway
Cross-sectional operators are the **daily normalization engine** of alpha research. They make signals comparable across instruments, improve robustness to outliers, and help convert raw ideas into portfolio-ready vectors.
