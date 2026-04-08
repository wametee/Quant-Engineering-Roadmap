# ⏱️ Learning Journey: Time Series Operators in WorldQuant BRAIN

**Time Series Operators** in the WorldQuant BRAIN platform.  
These operators analyze values across historical windows, helping build signals based on momentum, mean reversion, volatility, stability, and event timing.

---

## 🎯 Purpose
The goal of this learning is to:
- Understand how rolling-window operators transform raw financial data.
- Learn when to use lag, delta, rank, regression, and distribution-based operators.
- Build robust alphas using historical context, not just today’s value.

---

## 📚 Operators and Examples

### 1. `days_from_last_change(x)`
- **Definition:** Returns days since the last time `x` changed.
- **Use Case:** Track “age” of the current value (often for event timing).
- **Example:**  
  `days_from_last_change(ern2_earnrelease_d1_calendar_prev)`

---

### 2. `hump(x, hump = 0.01)`
- **Definition:** Limits day-to-day change in output to reduce turnover.
- **Use Case:** Smooth signal changes and control trading aggressiveness.
- **Example:**  
  `hump(-ts_delta(close, 5), hump = 0.00001)`

---

### 3. `kth_element(x, d, k, ignore="NaN")`
- **Definition:** Returns the `k`-th valid historical value from last `d` days.
- **Use Case:** Efficient backfilling (e.g., `k=1` for most recent valid value).
- **Example:**  
  `kth_element(sales/assets, 252, k="1", ignore="NaN 0")`

---

### 4. `last_diff_value(x, d)`
- **Definition:** Returns the most recent value in last `d` days that differs from today’s value.
- **Use Case:** Detect previous regime/value before the current level.
- **Example:**  
  `last_diff_value(eps, 63)`

---

### 5. `ts_arg_max(x, d)`
- **Definition:** Returns how many days ago the maximum occurred in last `d` days.
- **Example:**  
  `ts_arg_max(close, 10)`

---

### 6. `ts_arg_min(x, d)`
- **Definition:** Returns how many days ago the minimum occurred in last `d` days.
- **Example:**  
  `ts_arg_min(close, 10)`

---

### 7. `ts_av_diff(x, d)`
- **Definition:** Returns `x - ts_mean(x, d)` (mean ignores NaNs).
- **Use Case:** Fast deviation-from-average measure.
- **Example:**  
  `ts_av_diff(close, 20)`

---

### 8. `ts_backfill(x, lookback = d, k = 1)`
- **Definition:** Replaces NaNs using recent valid values within lookback window.
- **Use Case:** Improve coverage and reduce missing-data noise.
- **Example:**  
  `ts_backfill(fnd6_newqv1300_xrdq, 252)`

---

### 9. `ts_corr(x, y, d)`
- **Definition:** Rolling Pearson correlation between `x` and `y`.
- **Use Case:** Capture co-movement/relationship strength.
- **Example:**  
  `ts_corr(vwap, close, 20)`

---

### 10. `ts_count_nans(x, d)`
- **Definition:** Counts number of NaN observations in last `d` days.
- **Use Case:** Data quality / coverage diagnostics.
- **Example:**  
  `ts_count_nans(volume, 10)`

---

### 11. `ts_covariance(y, x, d)`
- **Definition:** Rolling covariance between `y` and `x` over `d` days.
- **Use Case:** Directional co-movement magnitude (scale-dependent).
- **Example:**  
  `ts_covariance(returns, volume, 20)`

---

### 12. `ts_decay_linear(x, d, dense = false)`
- **Definition:** Applies linearly weighted average (recent points weighted more).
- **Use Case:** Smooth noisy series and lower turnover.
- **Example:**  
  `ts_rank(ts_decay_linear(close, 5), 252)`

---

### 13. `ts_delay(x, d)`
- **Definition:** Returns value of `x` from `d` days ago.
- **Use Case:** Build lagged features and comparisons.
- **Example:**  
  `ts_delay(close, 5)`

---

### 14. `ts_delta(x, d)`
- **Definition:** Returns change vs. `d` days ago (`x - ts_delay(x, d)`).
- **Use Case:** Momentum/reversal building block.
- **Example:**  
  `ts_delta(close, 5)`

---

### 15. `ts_mean(x, d)`
- **Definition:** Rolling arithmetic mean over `d` days.
- **Use Case:** Smoothing and baseline estimation.
- **Example:**  
  `ts_mean(returns, 21)`

---

### 16. `ts_product(x, d)`
- **Definition:** Product of values over last `d` days.
- **Use Case:** Compounding / geometric calculations.
- **Example:**  
  `power(ts_product(returns, 10), 1/10)`

---

### 17. `ts_quantile(x, d, driver="gaussian")`
- **Definition:** Applies inverse CDF transform to `ts_rank(x, d)`.
- **Drivers:** `"gaussian"` (default), `"uniform"`, `"cauchy"`.
- **Use Case:** Distribution shaping / normalization.
- **Example:**  
  `ts_quantile(anl14_mean_div_fy1/cap, 252, driver="gaussian")`

---

### 18. `ts_rank(x, d, constant = 0)`
- **Definition:** Rank of today’s value within last `d` days (optionally shifted by constant).
- **Use Case:** Time-series normalization per instrument.
- **Examples:**  
  `ts_rank(pretax_income, 252)`  
  `rank(ts_rank(cap/income, 252))`

---

### 19. `ts_regression(y, x, d, lag = 0, rettype = 0)`
- **Definition:** Returns rolling OLS regression outputs over `d` days.
- **Common `rettype`:** `0` error term, `1` alpha, `2` beta, `6` R-square.
- **Use Case:** Trend extraction, factor sensitivity, fit diagnostics.
- **Examples:**  
  `ts_regression(est_netprofit, est_netdebt, 252, lag=0, rettype=2)`  
  `ts_regression(ts_mean(volume, 2), ts_returns(close, 2), 252)`

---

### 20. `ts_scale(x, d, constant = 0)`
- **Definition:** Scales to `[0,1]` using rolling min/max, then adds `constant`.
- **Formula:** `(x - ts_min(x,d)) / (ts_max(x,d) - ts_min(x,d)) + constant`
- **Use Case:** Bounded normalization (sensitive to outliers).
- **Example:**  
  `ts_scale(close, 252, constant=0)`

---

### 21. `ts_std_dev(x, d)`
- **Definition:** Rolling standard deviation over `d` days.
- **Use Case:** Volatility / dispersion measure.
- **Example:**  
  `ts_std_dev(returns, 21)`

---

### 22. `ts_step(1)`
- **Definition:** Day counter that increments by one each day.
- **Use Case:** Time index input (often with `ts_regression`).
- **Example:**  
  `ts_regression(returns, ts_step(1), 60, rettype=0)`

---

### 23. `ts_sum(x, d)`
- **Definition:** Rolling sum of `x` over last `d` days.
- **Use Case:** Aggregation across recent history.
- **Example:**  
  `ts_sum(returns, 20)`

---

### 24. `ts_zscore(x, d)`
- **Definition:** Standardizes value: `(x - ts_mean(x,d)) / ts_std_dev(x,d)`.
- **Use Case:** Put signals into sigma units for comparability.
- **Example:**  
  `ts_zscore(returns, 63)`

---

## 🛠️ Practical Outcomes
By mastering time-series operators, I will:
- Build lagged, smoothed, and normalized features from raw market/fundamental data.
- Improve signal robustness using backfill, hump, and decay methods.
- Measure trend, dispersion, and co-movement with statistical operators.
- Create event-driven logic using change-age and historical extrema operators.

---

## 💡 High-Value Tips
- Use `ts_backfill` or `kth_element(..., k=1)` to handle sparse fields.
- Prefer `ts_decay_linear` in intermediate signal layers; use simulation decay for final alpha-level smoothing.
- Keep lookback windows economically meaningful (too long can add stale information).
- Combine `ts_zscore` with cross-sectional `rank` for stronger, more stable signals.
- Watch out for outliers when using `ts_scale`.

---

## 📅 Progress Tracking
- [ ] Event Timing (`days_from_last_change`, `last_diff_value`)
- [ ] Lag/Change Basics (`ts_delay`, `ts_delta`, `ts_sum`, `ts_mean`)
- [ ] Relative Positioning (`ts_rank`, `ts_quantile`, `ts_scale`, `ts_zscore`)
- [ ] Risk/Structure (`ts_std_dev`, `ts_corr`, `ts_covariance`, `ts_regression`)
- [ ] Stability & Data Quality (`hump`, `ts_decay_linear`, `ts_backfill`, `ts_count_nans`)

---

## 🚀 Big Takeaway
Time-series operators are the **memory system** of quant signals. They convert raw observations into structured historical context, allowing alphas to detect persistence, change, and statistical structure rather than reacting only to today’s snapshot.
