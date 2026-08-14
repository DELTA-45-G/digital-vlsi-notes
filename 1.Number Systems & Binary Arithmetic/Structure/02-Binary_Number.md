# BINARY NUMBER SYSTEM ⭐⭐⭐

This is one of the highest-weightage topics for:

* Aptitude / written test
* Technical interview
* Verilog coding
* STA / VLSI understanding

---

## 1. What is Binary?

Binary uses only 2 digits:

### `0 and 1`

**Base = 2**

Why only 0 and 1?

Because electronic circuits can easily represent two stable voltage levels.

---

## 2. Why is it needed?

Imagine a light switch.

```text
OFF → 0
ON  → 1
```

Transistors inside a chip also behave like switches.

So computers use binary.

---

## 3. Real hardware example ⭐

`5`

* CMOS inverter: input 0 → output 1, input 1 → output 0
* Memory cell: stores 0 or 1
* Processor: performs billions of binary operations per second

---

## 4. Positional weights in Binary ⭐

Just like decimal uses powers of 10, binary uses powers of 2.

| Power | Value |
| ----- | ----: |
| 2³    |     8 |
| 2²    |     4 |
| 2¹    |     2 |
| 2⁰    |     1 |

```text
1  0  1  1
8  4  2  1
```

```text
1011₂ = 8 + 0 + 2 + 1 = 11₁₀
```

---

## 5. Memory Trick ⭐

Write powers of 2 until 1024.

```text
1   2   4   8   16   32   64   128   256   512   1024
```

For placements, remember up to 1024.

---

## 6. Binary to Decimal Conversion ⭐⭐⭐

### Method

Multiply each bit by its positional weight and add.

### Example 1

Convert `1101₂` to decimal.

|       Bit | Weight |  Value |
| --------: | -----: | -----: |
|         1 |      8 |      8 |
|         1 |      4 |      4 |
|         0 |      2 |      0 |
|         1 |      1 |      1 |
| **Total** |        | **13** |

✅ `1101₂ = 13₁₀`

### Example 2

Convert `101101₂`.

```text
Weights: 32  16  8  4  2  1
Bits:      1   0  1  1  0  1
```

```text
32 + 0 + 8 + 4 + 0 + 1 = 45
```

✅ `101101₂ = 45₁₀`

---

## 7. Decimal to Binary Conversion ⭐⭐⭐

### Method: Repeated division by 2

Convert `25₁₀`.

| Division | Quotient | Remainder |
| -------- | -------: | --------: |
| 25 ÷ 2   |       12 |         1 |
| 12 ÷ 2   |        6 |         0 |
| 6 ÷ 2    |        3 |         0 |
| 3 ÷ 2    |        1 |         1 |
| 1 ÷ 2    |        0 |         1 |

Read remainders from bottom to top:

### `11001₂`

`25₁₀ = 11001₂`

---

## 8. Shortcut for Interview Questions ⭐

Use powers of 2.

Convert `19`:

* Largest power ≤ 19 is 16
* 19 − 16 = 3
* 3 = 2 + 1

So set bits for 16, 2, 1.

| 16 |  8 |  4 |  2 |  1 |
| -: | -: | -: | -: | -: |
|  1 |  0 |  0 |  1 |  1 |

✅ `19 = 10011₂`

This is much faster in written tests.

---

## 9. Common Mistakes ❌

* Reading remainders top-to-bottom

  Always read bottom → top.

* Using decimal weights in binary

  Use `1, 2, 4, 8, 16, ...` not `1, 10, 100`.

* Ignoring leading zeros

  `0011₂` and `11₂` are numerically equal.

---

## 10. Placement Interview Questions ⭐

### Q1. Why is binary preferred over decimal in digital circuits?

**Answer:** Easier to implement using two stable voltage levels, better noise immunity, simpler hardware.

### Q2. What is the largest decimal number represented by 8 bits?

For unsigned:

```text
2⁸ − 1 = 255
```

### Q3. How many bits are required to represent 1000?

Find smallest `n` such that:

```text
2ⁿ > 1000
```

```text
2¹⁰ = 1024
```

✅ **10 bits**

---

## 11. MCQs

### Q1. `1010₂` equals?

* A) 8
* B) 10 ✅
* C) 12
* D) 14

### Q2. `13₁₀` in binary is?

* A) 1011
* B) 1101 ✅
* C) 1110
* D) 1001

### Q3. Number of values represented by 4 bits?

* A) 4
* B) 8
* C) 16 ✅
* D) 32

---

## 12. Numerical Problems

### Easy

Convert `1001₂` to decimal.

```text
8 + 1 = 9
```

✅ **9**

### Medium

Convert `11101₂` to decimal.

```text
16 + 8 + 4 + 1 = 29
```

✅ **29**

### Placement Level ⭐

Convert `173₁₀` to binary.

Largest powers:

* 128 → 1
* 64 → 0
* 32 → 1
* 16 → 0
* 8 → 1
* 4 → 1
* 2 → 0
* 1 → 1

✅ `10101101₂`

---

## 13. Verilog Relevance ⭐⭐⭐

In Verilog:

```verilog
8'b10101101
```

means:

* 8 bits
* binary
* value `10101101`

Other forms:

```verilog
8'd173   // decimal
8'hAD    // hexadecimal
8'o255   // octal
```

Interview favorite: **“Are these equal?”**

```verilog
8'd10 == 8'b1010 == 8'h0A
```

✅ Yes

---

## 14. One-Page Quick Revision

### Base

`2`

### Digits

`0, 1`

### Weights

```text
1  2  4  8  16  32  64  128
```

### Binary → Decimal

Multiply by weights and add.

```text
10110 = 16 + 4 + 2 = 22
```

### Decimal → Binary

Repeated divide by 2.

Read remainders bottom ↑ top.

### 8-bit unsigned range ⭐

```text
0 to 255
```

Formula:

```text
2ⁿ − 1
```

### Bits required ⭐

Smallest `n` such that:

```text
2ⁿ > number
```
