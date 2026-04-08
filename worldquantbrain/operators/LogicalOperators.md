# ⚖️ Learning Journey: Logical Operators in WorldQuant BRAIN

**Logical Operators** in the WorldQuant BRAIN platform.  
These operators allow me to introduce conditional logic, comparisons, and Boolean rules into quantitative signals, making them adaptive to market conditions.

---

## 🎯 Purpose
The goal of this learning is to:
- Understand how logical operators control decision-making in signals.
- Learn to apply conditions, comparisons, and Boolean logic to financial data.
- Build signals that react dynamically to market events.

---

## 📚 Operators and Examples

### 1. `and(input1, input2)`
- **Definition:** Returns `1` if both inputs are true (`1`), otherwise `0`.
- **Example:**  
  `and(volume > adv20, close > open)` → true only if volume spikes and price rises.

---

### 2. `or(input1, input2)`
- **Definition:** Returns `1` if either input is true, otherwise `0`.
- **Example:**  
  `or(close > open, volume > adv20)` → true if either price rises or volume spikes.

---

### 3. `not(x)`
- **Definition:** Logical negation. Returns `1` when input is false (`0`), and `0` when input is true (`1`).
- **Example:**  
  `not(close > open)` → true if closing price is not greater than opening price.

---

### 4. `if_else(condition, value_if_true, value_if_false)`
- **Definition:** Returns one of two values based on a condition.
- **Example:**  
``` Event = volume > adv20
if_else(Event, 2 * ts_delta(close, 3), ts_delta(close, 3))```

→ doubles position change when volume exceeds 20-day average.

---

### 5. Comparison Operators
- **`input1 < input2`** → true if input1 is smaller.  
Example: `close < vwap`
- **`input1 <= input2`** → true if input1 is smaller or equal.  
Example: `returns <= 0`
- **`input1 == input2`** → true if inputs are equal.  
Example: `rank(volume) == 0.5`
- **`input1 > input2`** → true if input1 is larger.  
Example: `close > open`
- **`input1 >= input2`** → true if input1 is larger or equal.  
Example: `returns >= 0`
- **`input1 != input2`** → true if inputs differ.  
Example: `sector != industry`

---

### 6. `is_nan(input)`
- **Definition:** Returns `1` if input is NaN, else `0`.
- **Example:**  
`if_else(is_nan(rank(sales)), 0.5, rank(sales))`  
→ replaces missing sales values with mean rank (0.5).

---

## 🛠️ Practical Outcomes
By mastering logical operators, I will:
- Introduce conditional rules into signals.
- Handle missing data gracefully with `is_nan` and `if_else`.
- Build adaptive signals that respond to thresholds, comparisons, and events.
- Combine Boolean logic with arithmetic for robust quant expressions.

---

## 📅 Progress Tracking
- [ ] Boolean Logic (`and`, `or`, `not`)  
- [ ] Conditional Rules (`if_else`)  
- [ ] Comparisons (`<`, `<=`, `==`, `>`, `>=`, `!=`)  
- [ ] Data Validation (`is_nan`)  

---

## 🚀 Big Takeaway
Logical operators are the **decision-making engine** of quant signals. They allow me to embed rules, comparisons, and conditions so that signals can adapt intelligently to changing market environments.
