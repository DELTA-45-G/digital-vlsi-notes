# DECIMAL NUMBER SYSTEM

## 1. What is it?

The decimal system uses 10 digits:

### `0 1 2 3 4 5 6 7 8 9`

**Base = 10**

Each position has a power of 10.

**Example:**

`538`

means

```text
5×10² + 3×10¹ + 8×10⁰
```

---

## 2. Why is it needed?

Humans use decimal, but digital circuits use binary.

You must know how to convert between human numbers and machine numbers.

---

## 3. Real hardware example

When you type:

```text
25
```

on a calculator or computer, it is eventually converted into binary inside the processor.

---

## 4. Important rule ⭐

For any base `b`:

```text
(dₙdₙ₋₁…d₀)ᵦ = ∑ᵢ₌₀ⁿ dᵢbⁱ
```

For decimal, `b = 10`.

---

## 5. Common mistakes

* Forgetting that the rightmost digit has power 0.
* Confusing digit value with positional value.

---

## 6. Placement interview question

**Q: What is the positional weight of digit 7 in 5724?**

**Answer:**

```text
7×10² = 700
```

---

## 7. MCQ

**Q1. The base of decimal system is:**

* A) 2
* B) 8
* C) 10 ✅
* D) 16

---

## 8. Numerical

### Easy

**Expand 204**

```text
2×10² + 0×10¹ + 4×10⁰ = 204
```

### Medium

**Expand 5072**

```text
5×1000 + 0×100 + 7×10 + 2 = 5072
```

---

## 9. Verilog relevance

Decimal is often used in testbenches:

```verilog
a = 25;
```

But synthesis converts it to binary.

---

## 10. One-page quick revision

### Decimal Quick Notes

```text
Base = 10
Digits: 0–9
Positional weights: ... 10³ 10² 10¹ 10⁰
Example: 482 = 4×10² + 8×10¹ + 2×10⁰
Rightmost position always has power 0.
```
