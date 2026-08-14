# PHASE 1 — PLACEMENT QUESTION BANK ⭐⭐⭐

## A. Number Systems & Conversions

### 1. What is the base of the binary number system?

**Answer:** 2.

### 2. What digits are used in binary?

**Answer:** `0` and `1`.

### 3. What is the base of hexadecimal?

**Answer:** 16.

### 4. What is the base of octal?

**Answer:** 8.

### 5. What is the hexadecimal representation of decimal 10?

**Answer:** `A`.

### 6. What is the hexadecimal representation of decimal 15?

**Answer:** `F`.

### 7. Convert `101101₂` to decimal.

**Answer:**

```text
32 + 8 + 4 + 1
```

**45₁₀**

### 8. Convert `45₁₀` to binary.

**Answer:** `101101₂`.

### 9. Convert `1111₂` to hexadecimal.

**Answer:** `F₁₆`.

### 10. Convert `10101100₂` to hexadecimal.

**Answer:**

```text
1010 1100 → AC
```

**AC₁₆**

### 11. Convert `3F₁₆` to decimal.

**Answer:**

```text
3×16 + 15 = 63
```

**63₁₀**

### 12. Why is hexadecimal commonly used instead of long binary numbers?

**Answer:** One hexadecimal digit represents exactly **4 binary bits**, making binary values much more compact and readable.

### 13. How many binary bits correspond to one octal digit?

**Answer:** **3 bits**.

### 14. How many binary bits correspond to one hexadecimal digit?

**Answer:** **4 bits**.

### 15. How many different values can be represented using 8 bits?

**Answer:**

```text
2⁸ = 256
```

So **256 values**.

---

# B. 1's & 2's Complement ⭐⭐⭐

### 16. What is 1's complement?

**Answer:** Invert every bit.

```text
0 → 1
1 → 0
```

### 17. What is 2's complement?

**Answer:** Take the 1's complement and add 1.

### 18. Find the 1's complement of `10110010`.

**Answer:** `01001101`.

### 19. Find the 2's complement of `10110010`.

**Answer:**

```text
1's complement → 01001101
+1              → 01001110
```

**Answer:** **`01001110`**

### 20. What is the fastest method for finding 2's complement?

**Answer:** Starting from the right, copy bits through the first `1`; invert all bits to its left.

### 21. Why is 2's complement preferred over 1's complement?

**Answer:** It provides a single representation for zero and allows addition/subtraction using simpler hardware.

### 22. How many zeros exist in 1's complement representation?

**Answer:** **Two**: positive zero and negative zero.

### 23. How many zeros exist in 2's complement?

**Answer:** **One**.

### 24. What is the 2's complement representation of −5 using 8 bits?

**Answer:**

```text
+5 = 00000101
1's complement = 11111010
+1 = 11111011
```

**Answer:** **`11111011`**

---

# C. Signed & Unsigned Numbers ⭐⭐⭐

### 25. What is the range of an n-bit unsigned number?

**Answer:**

```text
0 to 2ⁿ−1
```

### 26. What is the range of an n-bit signed 2's complement number?

**Answer:**

```text
−2ⁿ⁻¹ to 2ⁿ⁻¹−1
```

### 27. What is the range of an 8-bit unsigned number?

**Answer:** **0 to 255**.

### 28. What is the range of an 8-bit signed number?

**Answer:** **−128 to +127**.

### 29. What is the range of a 4-bit signed number?

**Answer:** **−8 to +7**.

### 30. What is the range of a 5-bit signed number?

**Answer:** **−16 to +15**.

### 31. What does the MSB represent in a signed 2's complement number?

**Answer:** It acts as the **sign bit**.

```text
0 → non-negative
1 → negative
```

### 32. Interpret `11111111` as unsigned and signed 8-bit.

**Answer:**

Unsigned = **255**

Signed = **−1**

### 33. Interpret `10000000` as unsigned and signed 8-bit.

**Answer:**

Unsigned = **128**

Signed = **−128**

### 34. Why is the signed range asymmetric?

**Answer:** The negative side contains one extra value because `1000...0` represents −2ⁿ⁻¹, while the maximum positive value is only 2ⁿ⁻¹−1.

### 35. What is sign extension?

**Answer:** Increasing the width of a signed number while preserving its value by copying the sign bit.

Example:

```text
1101 → 11111101
```

---

# D. Binary Addition ⭐⭐⭐

### 36. What is `1 + 1` in binary?

**Answer:** `10₂`.

```text
Sum = 0
Carry = 1
```

### 37. What is `1 + 1 + 1` in binary?

**Answer:** `11₂`.

```text
Sum = 1
Carry = 1
```

### 38. Add `1011 + 0101`.

**Answer:** `10000`.

### 39. Add `1101 + 1011`.

**Answer:** `11000`.

### 40. What are the outputs of a half adder?

**Answer:**

```text
Sum   = A XOR B
Carry = A AND B
```

### 41. What is the difference between a half adder and a full adder?

**Answer:**

**Half adder:** 2 inputs, no carry input.

**Full adder:** 3 inputs — A, B, and carry-in.

### 42. Why is carry propagation important?

**Answer:** A carry generated at a lower bit may need to travel through higher bits, increasing the delay of the adder.

### 43. Which type of adder has carry propagation through each stage?

**Answer:** **Ripple Carry Adder.**

---

# E. Binary Subtraction ⭐⭐⭐

### 44. How is subtraction implemented using 2's complement?

**Answer:**

```text
A−B = A + 2’s complement of B
```

### 45. Calculate `0111 − 0101`.

**Answer:** `0010` = **2**.

### 46. Calculate `0101 − 0111` using 4-bit 2's complement.

**Answer:** `1110` = **−2**.

### 47. What happens when there is an end carry in 2's complement subtraction?

**Answer:** The end carry is **discarded**.

### 48. What happens when there is no end carry?

**Answer:** The result is negative; take its 2's complement to obtain the magnitude.

### 49. Why is 2's complement subtraction useful in hardware?

**Answer:** The same adder hardware can perform both addition and subtraction.

---

# F. Carry vs Overflow ⭐⭐⭐⭐⭐

This is one of the **highest-priority Phase 1 interview topics**.

### 50. What is carry?

**Answer:** A carry is generated when the result exceeds the available bit position, primarily relevant to **unsigned arithmetic**.

### 51. What is overflow?

**Answer:** Overflow occurs when the mathematical result is outside the representable range of a **signed number**.

### 52. Is carry the same as overflow?

**Answer:** **No.**

```text
Carry ≠ Overflow
```

### 53. Can carry occur without signed overflow?

**Answer:** Yes.

Example:

```text
1111 + 0001
```

There is a carry, but signed interpretation gives `−1 + 1 = 0`, so no signed overflow.

### 54. Can signed overflow occur without a final carry?

**Answer:** Yes.

Example:

```text
0111 + 0001 = 1000
```

Signed: `+7 + +1` → invalid 4-bit signed result.

Overflow occurs, with no final carry.

### 55. When does signed addition overflow?

**Answer:**

**Positive + Positive → Negative**

or

**Negative + Negative → Positive**

### 56. Can adding numbers with different signs cause signed overflow?

**Answer:** **No.**

### 57. Does `1011 + 1101` overflow in 4-bit signed arithmetic?

**Answer:**

```text
1011 = −5
1101 = −3
```

Result = `−8`, which is representable.

**No overflow.**

### 58. Does `1100 + 1011` overflow in 4-bit signed arithmetic?

**Answer:**

```text
−4 + −5 = −9
```

Range is −8 to +7.

**Yes, overflow.**

---

# G. Binary Multiplication ⭐⭐

### 59. What are the basic binary multiplication rules?

**Answer:**

```text
0×0=0
0×1=0
1×0=0
1×1=1
```

### 60. What is the basic hardware idea behind binary multiplication?

**Answer:** **Shift and add**.

### 61. Calculate `101 × 101`.

**Answer:** `11001₂` = **25**.

### 62. What is the maximum result width of n-bit × m-bit multiplication?

**Answer:** Up to **n + m bits**.

### 63. What is the result width of 8-bit × 8-bit multiplication?

**Answer:** **16 bits**.

### 64. Why is multiplication generally more complex than addition?

**Answer:** It typically requires partial-product generation, shifting, and addition.

---

# H. Binary Division ⭐⭐

### 65. What is the basic method for binary division?

**Answer:** Compare → subtract → bring down the next bit.

### 66. Calculate `1100 ÷ 10`.

**Answer:** `110₂` = **6**.

### 67. What is the fundamental division identity?

**Answer:**

```text
Dividend = Divisor × Quotient + Remainder
```

### 68. What is `10111 >> 2`?

**Answer:** `00101₂` = **5**.

### 69. What happens to the remainder when an unsigned integer is right-shifted?

**Answer:** The discarded lower bits contain the remainder and are **lost**.

---

# I. Shift Operations ⭐⭐⭐⭐⭐

### 70. What does a left shift by 1 do to an unsigned number?

**Answer:** Multiplies it by 2, provided no relevant bits are lost.

### 71. What does a left shift by n positions do?

**Answer:**

```text
A << n = A × 2ⁿ
```

for unsigned arithmetic when the result fits the available width.

### 72. What does a right shift by 1 do to an unsigned number?

**Answer:** Integer division by 2.

### 73. What does a right shift by n positions do?

**Answer:**

```text
A >> n = ⌊A / 2ⁿ⌋
```

for unsigned integers.

### 74. What is the difference between logical and arithmetic right shift?

**Answer:**

**Logical right shift:** fills leftmost bits with `0`.

**Arithmetic right shift:** copies the sign bit.

### 75. What are the Verilog operators for logical and arithmetic right shift?

**Answer:**

```text
>>  → logical right shift
>>> → arithmetic right shift
```

### 76. What is `10110000 >> 2`?

**Answer:** `00101100`.

### 77. What is `11110000 >>> 2` for a signed value?

**Answer:** `11111100`.

### 78. Why is arithmetic right shift important for signed numbers?

**Answer:** It preserves the sign while shifting, which is important for signed arithmetic.

---

# J. Verilog-Based Phase 1 Questions ⭐⭐⭐

### 79. What does `8'b10101010` mean?

**Answer:** An 8-bit binary value `10101010`.

### 80. What does `8'hFF` represent as unsigned?

**Answer:** **255**.

### 81. What does `8'hFF` represent as signed?

**Answer:** **−1**, when interpreted as an 8-bit 2's complement signed value.

### 82. What is the difference between:

```verilog
reg [7:0] a;
```

```verilog
reg signed [7:0] b;
```

**Answer:** `a` is unsigned; `b` is signed.

### 83. What does this mean?

```text
a << 2
```

**Answer:** Left shift by 2 positions; for an unsigned value without truncation, equivalent to multiplication by 4.

### 84. What does `a >>> 2` mean?

**Answer:** Arithmetic right shift by 2 positions.

### 85. What can happen if a multiplication result is assigned to a signal that is too narrow?

**Answer:** Higher-order bits can be **truncated**, producing an incorrect numerical result.

---

# ⭐ TOP 20 QUESTIONS TO MEMORIZE FIRST

For a Tier-2 VLSI placement, prioritize these:

1. **Range of n-bit signed number?**
2. **Range of n-bit unsigned number?**
3. **Why is 2's complement preferred?**
4. **Find 2's complement of a binary number.**
5. **Interpret `11111111` as signed/unsigned.**
6. **Interpret `10000000` as signed/unsigned.**
7. **What is sign extension?**
8. **Difference between carry and overflow?**
9. **When does signed overflow occur?**
10. **Can carry occur without overflow?**
11. **Can overflow occur without carry?**
12. **How is subtraction implemented using 2's complement?**
13. **What is `1+1` in binary?**
14. **Half adder sum and carry equations?**
15. **Why is Ripple Carry Adder slow?**
16. **n-bit × m-bit result width?**
17. **What does left shift mean?**
18. **Difference between logical and arithmetic right shift?**
19. **`>>` vs `>>>` in Verilog?**
20. **Convert binary ↔ hexadecimal quickly.**
