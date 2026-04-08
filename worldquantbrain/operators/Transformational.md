# 🔁 Learning Journey: Transformational Operators in WorldQuant BRAIN

I am currently studying **Transformational Operators** in the WorldQuant BRAIN platform.  
These operators help reshape alpha behavior through grouping logic and event-driven trading rules.

---

## 🎯 Purpose
The goal of this learning is to:
- Understand how to discretize continuous signals into groups.
- Learn how to control when an alpha updates, holds, or exits.
- Build lower-turnover, event-aware signals with better execution discipline.

---

## 📚 Operators and Examples

### 1. `bucket(rank(x), range="0, 1, 0.1", skipBoth=False, NaNGroup=False)`
### or `bucket(rank(x), buckets="2,5,6,7,10", skipBoth=False, NaNGroup=False)`
- **Definition:** Creates custom discrete groups (bucket IDs) from ranked values.
- **Use Case:** Build group labels for `group_neutralize`, `group_rank`, `group_zscore`, etc.

#### How it works
- `rank(x)` maps values cross-sectionally into `[0, 1]`.
- `bucket(...)` assigns each ranked value into a bucket using one of:
  - `range="start, end, step"` for equal-width intervals.
  - `buckets="b1,b2,...,bn"` for custom boundaries.
- Out-of-range hidden buckets can be controlled by:
  - `skipBoth=True`, or separately `skipBegin=True` / `skipEnd=True`.
- `NaNGroup=True` puts NaN inputs into an additional final bucket.

#### Example calculations
**Using range**

```fast_expression
bucket(rank(x), range="0, 1, 0.1")
```

Given ranked values: `[0.05, 0.45, 0.9]`
- `0.05` in `(0, 0.1]` -> bucket `0`
- `0.45` in `(0.4, 0.5]` -> bucket `4`
- `0.9` in `(0.8, 0.9]` -> bucket `8`

Output: `[0, 4, 8]`

**Using explicit boundaries**

```fast_expression
bucket(rank(x), buckets="0.2,0.5,0.7")
```

Boundaries define:
- Bucket `0`: `<= 0.2`
- Bucket `1`: `(0.2, 0.5]`
- Bucket `2`: `(0.5, 0.7]`
- Bucket `3`: `> 0.7`

Given input values: `[0.1, 0.3, 0.6, 0.8]`  
Output: `[0, 1, 2, 3]`

#### Practical examples

```fast_expression
asset_group = bucket(rank(assets), range="0.1, 1, 0.1")
group_zscore(alpha, densify(asset_group))
```

```fast_expression
my_group = bucket(rank(volume), buckets="0.2,0.5,0.7", skipBoth=True, NaNGroup=True)
group_neutralize(sales/assets, my_group)
```

**Tip:** If simulation is slow, apply `densify()` to the group variable before group operators to remove empty buckets and improve speed.

---

### 2. `trade_when(x, y, z)`
- **Definition:** Updates alpha only on a trigger, holds otherwise, and exits (NaN) on condition.
- **Use Case:** Event-driven trading and turnover reduction.

#### Rule order
- If `z` is true -> output `NaN` (exit position).
- Else if `x` is true -> output `y` (update alpha).
- Else -> keep previous alpha value (hold).

#### Example

```fast_expression
trade_when(volume >= ts_mean(volume, 5), rank(-returns), -1)
```

- If today’s volume is above 5-day average -> alpha becomes `rank(-returns)`.
- Otherwise -> alpha holds previous value.
- Exit condition `-1` is always false, so this rule does not force exits.

---

## 🛠️ Practical Outcomes
By mastering transformational operators, I will:
- Convert continuous values into actionable groups for neutralization and ranking.
- Build event-driven alphas that trade only when conditions justify updates.
- Reduce unnecessary turnover by carrying forward previous positions.
- Improve simulation efficiency and stability with smarter grouping logic.

---

## 📅 Progress Tracking
- [ ] Learn `bucket` with both `range` and `buckets` syntax.
- [ ] Practice `skipBoth`, `skipBegin`, `skipEnd`, and `NaNGroup` behavior.
- [ ] Use grouped outputs with `group_zscore` and `group_neutralize`.
- [ ] Build and test event-driven alphas using `trade_when`.

---

## 🚀 Big Takeaway
Transformational operators are the **control layer** of quant signals. They define *how* and *when* alphas react by grouping instruments and enforcing event-based update rules.
