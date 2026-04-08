# 🧩 Learning Journey: Group Operators in WorldQuant BRAIN

**Group Operators** in the WorldQuant BRAIN platform.  
These operators allow me to handle data within groups (industries, sectors, countries, or custom buckets), making signals more robust by neutralizing group effects, filling missing data, and normalizing values.

---

## 🎯 Purpose
The goal of this learning is to:
- Understand how to aggregate and normalize data within groups.
- Learn to handle missing values using group-level statistics.
- Build signals that compare instruments fairly across categories.

---

## 📚 Operators and Examples

### 1. `group_backfill(x, group, d, std=4.0)`
- **Definition:** Fills missing values using the winsorized mean of non-NaN values in the same group over the past `d` days.
- **Example Calculation:**

```fast_expression
group_backfill(fnd94_rt_gross_mgn_q, subindustry, 21)
```

Fills missing gross margin values within each subindustry using the winsorized mean of the last 21 days.

---

### 2. `group_mean(x, weight, group)`
- **Definition:** Calculates the weighted mean of values within each group.
- **Example Calculation:**

```fast_expression
group_mean(close/eps, 1, industry)
```

Computes the group mean of `close/eps` within each industry.

---

### 3. `group_neutralize(x, group)`
- **Definition:** Neutralizes values by subtracting the group mean, making each group average equal to zero.
- **Example Calculations:**

```fast_expression
alpha1 = group_neutralize(ts_returns(close, 5), industry)
```

Neutralizes 5-day returns within each industry.

```fast_expression
custom_group = bucket(rank(cap), range="0,1,0.2")
alpha2 = group_neutralize(ts_returns(close, 5), custom_group)
```

Neutralizes returns within custom market-cap buckets.

---

### 4. `group_rank(x, group)`
- **Definition:** Ranks each element within its group, normalized between `0.0` and `1.0`.
- **Example Calculations:**

```fast_expression
group_rank(close, subindustry)
```

Ranks closing prices within each subindustry.

```fast_expression
group_rank(ts_rank(eps, 252), industry)
```

Ranks EPS values within each industry after computing 252-day time-series rank.

---

### 5. `group_scale(x, group)`
- **Definition:** Normalizes values within each group to the `[0,1]` range.
- **Example Calculation:**

```fast_expression
group_scale(return_equity, industry)
```

Scales return on equity within each industry so lowest is `0` and highest is `1`.

---

### 6. `group_zscore(x, group)`
- **Definition:** Computes the z-score of each value within its group (distance from group mean in standard deviations).
- **Example Calculation:**

```fast_expression
asset_group = bucket(rank(operating_income/assets), range="0.1,1,0.1")
alpha = group_zscore(cap/income, densify(asset_group))
```

Creates groups based on `operating_income/assets` and computes z-scores of `cap/income` within each group.

---

## 🛠️ Practical Outcomes
By mastering group operators, I will:
- Handle missing data using group-level backfill.
- Neutralize signals to remove group biases.
- Rank and scale values for fair intra-group comparison.
- Standardize signals with group-level z-scores.

---

## 📅 Progress Tracking
- [ ] Learn `group_backfill` for filling missing values.
- [ ] Learn `group_mean` for group-level averages.
- [ ] Learn `group_neutralize` for removing group effects.
- [ ] Learn `group_rank` for intra-group comparisons.
- [ ] Learn `group_scale` for normalization.
- [ ] Learn `group_zscore` for standardization.

---

## 🚀 Big Takeaway
Group operators are the fairness tools of quant signals. They ensure that comparisons are made within relevant categories, reduce bias from group-level effects, and make signals more robust across industries, sectors, and custom-defined buckets.
