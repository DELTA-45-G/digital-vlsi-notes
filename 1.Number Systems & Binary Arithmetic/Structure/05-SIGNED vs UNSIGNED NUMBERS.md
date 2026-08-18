# SIGNED vs UNSIGNED NUMBERS ⭐⭐⭐

## 1. What is the difference?

Imagine an 8-bit number:

**Unsigned**

Only positive

**Signed (2’s complement)**

Positive and negative

The same bit pattern can mean different values.

---

## 2. Example ⭐

Bit pattern: `11111111`

**As unsigned**

`255`

**As signed**

`−1`

🚨 Interview favorite: **“What is the value of 0xFF?”**

Correct answer: **Depends on signedness.**

---

## 3. Why do we need signed numbers?

Real systems need:

* Temperatures
* Sensor errors
* Velocity
* Audio samples
* Arithmetic results

Negative values are essential.

---

## 4. Unsigned Representation

For n bits:

**Minimum**

`000`

**Maximum**

`2ⁿ−1`

### 4-bit unsigned

| Binary | Value |
| ------ | ----: |
| `0000` |     0 |
| `0001` |     1 |
| `0010` |     2 |
| `0011` |     3 |
| `0100` |     4 |
| `0101` |     5 |
| `0110` |     6 |
| `0111` |     7 |
| `1000` |     8 |
| `1001` |     9 |
| `1010` |    10 |
| `1011` |    11 |
| `1100` |    12 |
| `1101` |    13 |
| `1110` |    14 |
| `1111` |    15 |

Range:

### `0 to 15`

---

## 5. Signed (2’s Complement) Representation ⭐⭐⭐

Same 4 bits:

| Binary | Value |
| ------ | ----: |
| `0000` |     0 |
| `0001` |     1 |
| `0010` |     2 |
| `0011` |     3 |
| `0100` |     4 |
| `0101` |     5 |
| `0110` |     6 |
| `0111` |     7 |
| `1000` |    −8 |
| `1001` |    −7 |
| `1010` |    −6 |
| `1011` |    −5 |
| `1100` |    −4 |
| `1101` |    −3 |
| `1110` |    −2 |
| `1111` |    −1 |

Range:

### `−8 to +7`

---

## 6. The Most Important Bit: MSB ⭐⭐⭐

**MSB**

**Sign bit**

| MSB    | Meaning  |
| ------ | -------- |
| `0xxx` | Positive |
| `1xxx` | Negative |

Examples:

* `0110` → +6
* `1110` → −2

---

## 7. How to Decode a Signed Number ⭐⭐⭐

### Example: `11101011`

**Step 1:** MSB = 1 → negative

**Step 2:** Take 2’s complement

```text
11101011
00010101
```

**Step 3:** Decimal = 21

Answer:

### `−21`

---

## 8. Compare Signed vs Unsigned ⭐⭐⭐

Bit pattern: `10000001`

**Unsigned**

`129`

**Signed**

`−127`

This is a classic interview trap.

---

## 9. Addition: Unsigned

Example:

```text
1111 (15)
+0001 (1)
----------
1 0000
```

Discard carry:

```text
0000
```

Result = 0 with carry = 1

✅ **Unsigned overflow occurred**

---

## 10. Addition: Signed ⭐⭐⭐

```text
0111 (+7)
+0001 (+1)
-----------
1000
```

Result = −8

Carry exists? No

Overflow? Yes

👉 This proves:

### Carry ≠ Overflow

They are completely different concepts.

---

## 11. Carry vs Overflow Table ⭐⭐⭐

| Arithmetic        | Check     |
| ----------------- | --------- |
| Unsigned addition | Carry out |
| Signed addition   | Overflow  |

---

## 12. Interview Trick: Detect Overflow Fast ⭐⭐⭐

Only look at sign bits.

### Case 1

```text
0101 + 0011
-------------
1000
```

**+ + → − ⇒ Overflow**

### Case 2

```text
1011 + 1100
-------------
0111
```

**− − → + ⇒ Overflow**

### Case 3

```text
0101 + 1100
-------------
0001
```

Different signs ⇒ **No overflow**

---

## 13. Sign Extension ⭐⭐⭐

Very important for Verilog and VLSI.

Convert 4-bit −3 to 8 bits.

4-bit:

```text
1101
```

Extend by repeating the sign bit (1):

```text
11111101
```

Value remains −3.

### Rule ⭐

Positive → fill with 0

Negative → fill with 1

---

## 14. Common Mistakes ❌

* Treating `11111111` as always 255
* Using carry to detect signed overflow
* Forgetting sign extension
* Thinking MSB has positive weight in signed numbers

---

## 15. Placement Interview Questions ⭐⭐⭐

### Q1. What is the difference between carry and overflow?

**Answer:** Carry is for unsigned arithmetic; overflow is for signed arithmetic.

### Q2. What is sign extension?

Copying the sign bit into higher bits when increasing width.

### Q3. Interpret `8'h80` as signed and unsigned.

* Unsigned = 128
* Signed = −128

### Q4. Why is 2’s complement asymmetric?

Because one pattern is used for −2ⁿ⁻¹.

For 8 bits:

* −128 to +127

Negative side has one extra value.

---

## 16. MCQs

### Q1. `11111111` as signed 8-bit is:

* A) 255
* B) −1 ✅
* C) 127
* D) −128

### Q2. Sign extension of `1010` to 8 bits:

* A) `00001010`
* B) `11111010` ✅
* C) `10100000`
* D) `11110100`

### Q3. Overflow occurs in:

* A) +5 + (−3)
* B) −2 + 1
* C) +6 + +3 (4-bit signed) ✅
* D) −1 + +1

---

## 17. Numerical Problems

### Easy

Interpret `1110` as signed 4-bit.

2’s complement → `0010` = 2

Answer: **−2**

### Medium

Sign-extend `0101` to 8 bits.

✅ `00000101`

### Placement Level ⭐⭐⭐

Interpret `10010110`.

* Unsigned = 150
* Signed:

  * 2’s complement → `01101010` = 106
  * Answer = −106

---

## 18. Verilog Relevance ⭐⭐⭐

```verilog
reg [7:0] u;         // unsigned
reg signed [7:0] s;  // signed
```

```verilog
u = 8'hFF;  // 255
s = 8'hFF;  // -1
```

🚨 This is a very common Verilog interview question.

---

## 19. One-Page Quick Revision

### Unsigned range

`0 to 2ⁿ−1`

### Signed range

`−2ⁿ⁻¹ to 2ⁿ⁻¹−1`

### MSB=0

Positive

### MSB=1

Negative

### Carry

Unsigned

### Overflow

Signed

### Overflow rule ⭐

```text
+ + → − #overflow
− − → + #overflow
```

### Sign extension ⭐

```text
0 → fill 0
1 → fill 1
The Rule:If the number starts with 1, fill the left side with 1s.
If the number starts with 0, fill the left side with 0s.
```
