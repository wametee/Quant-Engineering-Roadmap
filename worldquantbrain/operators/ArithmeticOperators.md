# 🔢 Learning Journey: Arithmetic Operators in WorldQuant BRAIN

**Arithmetic Operators** in the WorldQuant BRAIN platform.  
These operators form the foundation of quantitative signal design, enabling transformations, comparisons, and mathematical manipulations of financial data.

---

## 🎯 Purpose
The goal of this learning is to:
- Understand the role of arithmetic operators in quant research.
- Learn how to apply them to financial time series data.
- Build intuition for constructing signals that capture meaningful relationships.

---

## 📚 Operators and Examples

### 1. `abs(x)`
- **Definition:** Returns the absolute value of a number, removing any negative sign.
- **Use Case:** Focus on magnitude, not direction.
- **Example:**  
  `abs(close - open)` → absolute daily price change.

---

### 2. `add(x, y, filter=false)`
- **Definition:** Adds two or more inputs element-wise.  
- **Tip:** Use `filter=true` to treat NaNs as 0.
- **Example:**  
  - `add([1, NaN, 3], [4, 5, NaN]) = [5, NaN, NaN]`  
  - `add([1, NaN, 3], [4, 5, NaN], filter=true) = [5, 5, 3]`

---

### 3. `densify(x)`
- **Definition:** Converts grouping fields with many buckets into fewer, efficient buckets.
- **Example:**  
  Industry codes `{0, 1, 2, 99}` → mapped to `{0, 1, 2, 3}`.

---

### 4. `divide(x, y)`
- **Definition:** Performs element-wise division.  
- **Example:**  
  `divide(close, vwap)` → ratio of closing price to VWAP.

---

### 5. `inverse(x)`
- **Definition:** Computes reciprocal, `1/x`.  
- **Example:**  
  `inverse(volume)` → inverse liquidity measure.

---

### 6. `log(x)`
- **Definition:** Natural logarithm of input.  
- **Example:**  
  - `log(10) ≈ 2.3026`  
  - `log(0.5) ≈ -0.6931`

---

### 7. `max(x, y, ..)`
- **Definition:** Returns maximum of inputs.  
- **Example:**  
  `max(close, vwap)` → higher of close or VWAP.

---

### 8. `min(x, y, ..)`
- **Definition:** Returns minimum of inputs.  
- **Example:**  
  `min(close, vwap)` → lower of close or VWAP.

---

### 9. `multiply(x, y, .., filter=false)`
- **Definition:** Element-wise multiplication.  
- **Tip:** `filter=true` replaces NaNs with 1.  
- **Examples:**  
  - `multiply(2, 3) = 6`  
  - `multiply(5, NaN, filter=true) = 5`

---

### 10. `power(x, y)`
- **Definition:** Raises `x` to power `y`.  
- **Example:**  
  `power(returns, volume/adv20)` → nonlinear scaling of returns.

---

### 11. `reverse(x)`
- **Definition:** Negates input (`-x`).  
- **Example:**  
  `reverse(close - open)` → inverse of daily change.

---

### 12. `sign(x)`
- **Definition:** Returns sign of input (+1, -1, 0).  
- **Example:**  
  `sign(close - open)` → direction of daily move.

---

### 13. `signed_power(x, y)`
- **Definition:** Raises `x` to `y` while preserving sign.  
- **Example:**  
  - `signed_power(3, 2) = 9`  
  - `signed_power(-9, 0.5) = -3`

---

### 14. `sqrt(x)`
- **Definition:** Square root of input.  
- **Example:**  
  - `sqrt(9) = 3`  
  - `sqrt(-4) = NaN` (use `signed_power(-4, 0.5) = -2`)

---

### 15. `subtract(x, y, filter=false)`
- **Definition:** Element-wise subtraction, left to right.  
- **Examples:**  
  - `subtract(10, 3) = 7`  
  - `subtract(10, 3, 2) = 5`  
  - `subtract(NaN, 5, filter=true) = -5`

---

## 🛠️ Practical Outcomes
By mastering these operators, I will:
- Build signals that capture magnitude, direction, and ratios.
- Handle missing data effectively with filters.
- Apply transformations (log, sqrt, power) to normalize and scale inputs.
- Construct robust, interpretable signals for simulation.

---

## 📅 Progress Tracking
- [ ] Absolute & Sign Operators (`abs`, `sign`)  
- [ ] Basic Arithmetic (`add`, `subtract`, `multiply`, `divide`)  
- [ ] Transformations (`log`, `sqrt`, `power`, `signed_power`)  
- [ ] Data Handling (`densify`, `filter options`)  
- [ ] Extremes (`max`, `min`)  

---

## 🚀 Big Takeaway
Arithmetic operators are the **building blocks of quant signals**. They allow me to transform raw market data into structured, testable expressions that can reveal hidden patterns in financial markets.
